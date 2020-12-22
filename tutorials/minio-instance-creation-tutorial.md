---
title: MinIO Instance Creation tutorial
description: This tutorial explains how create Instances for your MinIO Operator.
---

### Create below yaml file to create MinIO Operator Instance:

```execute
cat <<'EOF' > MinioInstance.yaml
apiVersion: miniocontroller.min.io/v1beta1
kind: MinIOInstance
metadata:
  name: minio
spec:
  replicas: 4
  credsSecret:
    name: minio-creds-secret
  requestAutoCert: false
EOF
```

Execute below command to create MinIO Operator instance

```execute
kubectl create -f MinioInstance.yaml -n my-minio-operator
```
You will see the following resources to be created:

```output

```

Get the associated Pods:

```execute
kubectl get pods -n my-minio-operator
```

You will be able to see the below output:

```output

```

### Create this for MinIO Service of type NodePort

```execute
cat <<'EOF' > MinioService.yaml
apiVersion: v1
kind: Service
metadata:
  name: minio-service
spec:
  type: ClusterIP
  ports:
    - port: 9000
      targetPort: 9000
      protocol: TCP
  selector:
    app: minio
EOF
```

Execute below command to create Grafana Service

```execute
kubectl create -f MinioService.yaml -n my-minio-operator
```

Click on the <a href="http://##DNS.ip##:30300" target="_blank">http://##DNS.ip##:30200</a> to access MinIO Pod from your browser.


