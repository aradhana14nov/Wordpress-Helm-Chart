Once the helm chart installation done we need to verify all the pods and services are up and running.

Execute below command to check status of pods and services: 

### Check the pod status:

```execute
kubectl get pods --namespace wordpress
```


You will get a list of running pods:

```
```

### Check all the Kubernetes resources status

You can run the following command to know status of all the deployed resources inside the namespace wordpress


```execute
kubectl get all --namespace wordpress
```

All the deployment and service status should be Running
