## Lab 26. Create a k8s cluster in GKE and deploy an application to it
___

* 1. follow the instruction to create a k8s cluster

* 2. get on to gcloud Cli console 

> deploy the application into the cluster

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: achenwebdemo
  labels:
    app: webnginx
spec:
  replicas: 4
  selector:
    matchLabels:
      app: nginxwebpod
  template:
    metadata:
      labels:
        app: nginxwebpod
    spec:
      containers:
      - name: nginx
        image: nginx:1.18.0
      - name: redis
        image: redis
        
---
apiVersion: v1 
kind: Service 
metadata: 
    name: lab19external 
spec: 
   selector: 
     app: nginxwebpod 
   type: LoadBalancer
   ports: 
        - protocol: TCP 
          port: 80 
          targetPort: 80
```

* find the defined service and access from external (laptop)


