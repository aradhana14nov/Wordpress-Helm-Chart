---
title: Verify WordPress Chart Installation
description: This tutorial explains how to verify that WordPress chart installed successfully
---


Once the helm chart installation done we need to verify all the pods and services are up and running.

Execute below command to check status of pods and services: 

### Check the pod status:


```execute
kubectl get pods --namespace wordpress
```

You will see similar to this output:

```
NAME                             READY   STATUS              RESTARTS   AGE
pod/wordpress-7d656dbb79-8x5m8   1/1     Running   0          10s
pod/wordpress-mariadb-0          1/1     Running   0          10s
```

Once the wordpress POD is up and running , your wordpress is ready to use



### Check all the Kubernetes resources status

You can run the following command to know status of all the deployed resources inside the namespace wordpress


```execute
kubectl get all --namespace wordpress
```

All the deployment and service status should be Running.

```
NAME                             READY   STATUS              RESTARTS   AGE
pod/wordpress-7d656dbb79-8x5m8   1/1     Running   0          10s
pod/wordpress-mariadb-0          1/1     Running   0          10s

NAME                        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
service/wordpress           NodePort    10.102.88.36    <none>        80:31205/TCP,443:32736/TCP   10s
service/wordpress-mariadb   ClusterIP   10.101.172.14   <none>        3306/TCP                     10s

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/wordpress   1/1     1            0           10s

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/wordpress-7d656dbb79   1         1         0       10s

NAME                                 READY   AGE
statefulset.apps/wordpress-mariadb   1/1     10s  
```
