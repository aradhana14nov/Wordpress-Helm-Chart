---
title: WordPress Bitnami Helm Chart Installation Tutorial
description: This tutorial explains how to Install WordPress Bitnami Helm Chart
---



```
sudo mkdir -p /bitnami/mariadb/data
sudo chown -R 1001:1001 /bitnami/mariadb/data
sudo mkdir -p /bitnami/wordpress/wp-content
sudo chown -R 1001:1001 /bitnami/wordpress/wp-content
sudo mkdir /data 
sudo chown -R 1001:1001 /data
```


### Add ‘bitnami/wordpress’ to your repo list of Helm Chart

Add bitnami/wordpress to your repo list :

```
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Once you add it successfully then you should see the following message:

```
"bitnami" has been added to your repositories
```



### Install the WordPress helm chart

Now we have completed all the pre-requisites for the installation. Let’s start installing the WordPress helm chart

** Create a namespace - wordpress **

```execute
kubectl create namespace wordpress
```


** Define the PersistentVolume for mariadb-pv where the mariadb data to be stored. The hostPath tells the mysql directory is in /bitnami/mariadb location

```
cat <<'EOF' > mariadbpv.yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mariadbpv
  labels:
    app: wordpress
spec:
  storageClassName: manual
  capacity:
    storage: 50Gi
  accessModes:
    - ReadWriteOnce
  claimRef:
     namespace: wordpress
     name: data-wordpress-mariadb-0
  hostPath:
    path: "/bitnami/mariadb"
EOF
```
Execute below command to create mariadb PV :

```
kubectl create -f  mariadbpv.yaml
```

- Define the PersistentVolume for wordpress-pv where the wordpress site data to be stored. The hostPath tells the mysql directory is in /data location

```
cat <<'EOF' > wordpresspv.yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: wordpresspv
  labels:
    app: wordpress
spec:
  storageClassName: manual
  capacity:
    storage: 50Gi
  accessModes:
    - ReadWriteOnce
  claimRef:
     namespace: wordpress
     name: wordpress
  hostPath:
    path: "/data"
EOF
```


Execute below command to create wordpress PV:


```
kubectl create -f  wordpresspv.yaml
```

### Setup User account along with Username and Password for WordPress

As Wordpress is CMS, so we need to have a user account to access it.

Create below yaml file to Setup WordPress User account along with Username and Password:

```
cat <<'EOF' > wordpress-values.yaml
wordpressUsername: admin
wordpressPassword: password
wordpressEmail: contact@example.com
wordpressBlogName: example.com
service: 
  type: NodePort
EOF
```



Run the following command for installation:

```
helm install wordpress bitnami/wordpress --values=wordpress-values.yaml --namespace wordpress 
```

output:

```
NAME: wordpress
LAST DEPLOYED: Mon Jan  4 02:59:22 2021
NAMESPACE: nswordpress
STATUS: deployed
REVISION: 1
NOTES:
** Please be patient while the chart is being deployed **

Your WordPress site can be accessed through the following DNS name from within your cluster:

    wordpress.nswordpress.svc.cluster.local (port 80)

To access your WordPress site from outside the cluster follow the steps below:

1. Get the WordPress URL by running these commands:

  NOTE: It may take a few minutes for the LoadBalancer IP to be available.
        Watch the status with: 'kubectl get svc --namespace nswordpress -w wordpress'

   export SERVICE_IP=$(kubectl get svc --namespace nswordpress wordpress --template "{{ range (index .status.loadBalancer.ingress 0) }}{{.}}{{ end }}")
   echo "WordPress URL: http://$SERVICE_IP/"
   echo "WordPress Admin URL: http://$SERVICE_IP/admin"

2. Open a browser and access WordPress using the obtained URL.

3. Login with the following credentials below to see your blog:

  echo Username: jhooq
  echo Password: $(kubectl get secret --namespace nswordpress wordpress -o jsonpath="{.data.wordpress-password}" | base64 --decode)
```




