### WordPress Console


### Access application URL for WordPress


Your WordPress site can be accessed through the following DNS name from within your cluster:

```
 wordpress.nswordpress.svc.cluster.local (port 80)
```

To access your WordPress site from outside the cluster follow the steps below:


1. Get the WordPress URL by running these commands:


```execute
   export NODE_PORT=$(kubectl get --namespace nswordpress -o jsonpath="{.spec.ports[0].nodePort}" services wordpress)
   export NODE_IP=$(kubectl get nodes --namespace nswordpress -o jsonpath="{.items[0].status.addresses[0].address}")
   echo "WordPress URL: http://$NODE_IP:$NODE_PORT/"
   echo "WordPress Admin URL: http://$NODE_IP:$NODE_PORT/admin"
```


2. Open a browser and access WordPress using the obtained URL.
```
http://$NODE_IP:$NODE_PORT/
```
3. Login with the following credentials below to see your blog:

To get your wordpress admin password run

root@kube-master:# kubectl get secret --namespace default wordpress-wordpress -o jsonpath="{.data.wordpress-password}" | base64 --decode


echo Username: jhooq
  echo Password: $(kubectl get secret --namespace nswordpress wordpress -o jsonpath="{.data.wordpress-password}" | base64 --decode)


And you can use the username and password for accessing the WordPress.
Navigate to the "Plugins" section and check that the plugin is also installed and activated.



## On successful login you will be seeing the dashbaord page.