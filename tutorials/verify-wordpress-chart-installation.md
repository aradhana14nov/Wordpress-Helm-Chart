---
title: Verify WordPress Chart Installation
description: This tutorial explains how to verify that WordPress chart installed successfully
---


Once the helm chart installation done we need to verify all the pods and services are up and running.

Execute below command to check status of pods and services: 

### Check the pod status


```execute
kubectl get pods --namespace wordpress
```

You will see similar to this output:

```
NAME                         READY   STATUS    RESTARTS   AGE
wordpress-78d64d86d6-8pljh   1/1     Running   9          35m
wordpress-mariadb-0          1/1     Running   0          35m
```

Once the wordpress POD is up and running , your wordpress is ready to use



### Check all the Kubernetes resources status

You can run the following command to know status of all the deployed resources inside the namespace wordpress


```execute
kubectl get all --namespace wordpress
```

All the deployment and service status should be Running.

```
NAME                             READY   STATUS    RESTARTS   AGE
pod/wordpress-78d64d86d6-8pljh   1/1     Running   9          37m
pod/wordpress-mariadb-0          1/1     Running   0          37m

NAME                        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
service/wordpress           NodePort    10.98.117.238   <none>        80:30414/TCP,443:30121/TCP   37m
service/wordpress-mariadb   ClusterIP   10.100.10.45    <none>        3306/TCP                     37m

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/wordpress   1/1     1            1           37m

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/wordpress-78d64d86d6   1         1         1       37m

NAME                                 READY   AGE
statefulset.apps/wordpress-mariadb   1/1     37m
```
