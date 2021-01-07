---
title: How to Access WordPress site and WordPress Admin Console
description: This tutorial explains how to access WordPress site and WordPress Admin Console once chart installed successfully
---


***WordPress Console***


To obtain the application URL, wait until the pods are running.


Your WordPress site can be accessed through the following DNS name from within your cluster:

```
 wordpress.wordpress.svc.cluster.local (port 80)
```

To access your WordPress site from outside the cluster follow the steps below:


1. Get the WordPress URL by running below commands:


```execute
 export NODE_PORT=$(kubectl get --namespace wordpress -o jsonpath="{.spec.ports[0].nodePort}" services wordpress)
 export NODE_IP=$(kubectl get nodes --namespace wordpress -o jsonpath="{.items[0].status.addresses[0].address}")
 echo "WordPress URL: http://$NODE_IP:$NODE_PORT/"
 echo "WordPress Admin URL: http://$NODE_IP:$NODE_PORT/admin"
```


2. Open a browser and access WordPress Site using the obtained URL.

```execute
echo "WordPress URL: http://$NODE_IP:$NODE_PORT/"
```
You should see your WordPress site with the custom theme that you have included in your image already activated. 

Please see the below snapshot how it looks like :

![](_images/wordpress-site.PNG)

3. Access WordPress Admin Console:

```execute
echo "WordPress Admin URL: http://$NODE_IP:$NODE_PORT/admin"
```

Open WordPress Admin Url in browser. You will see following login page :

![](_images/login-console-final.PNG)

- Log in to WordPress admin login console with the credentials obtained from running below commands:

```execute
echo Username: jhooq
echo Password: $(kubectl get secret --namespace wordpress wordpress -o jsonpath="{.data.wordpress-password}" | base64 --decode)
```

![](_images/console-admin-final.PNG)

On successful login you will be see the following dashbaord page:

![](_images/dashboard-wordpress.PNG)

Navigate to the "Plugins" section and you can check what all plugin installed and activated as below snapshot:

![](_images/plugins.PNG)



