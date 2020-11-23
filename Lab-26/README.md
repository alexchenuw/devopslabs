## Lab 26. Create a k8s cluster in GKE and deploy an application into the cluster
___

*  Follow the instruction to create a k8s cluster

*  Get on to gcloud Cli console 

```
kubectl get pod --all-namespaces
kubectl get node
```

> deploy the application into the cluster

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: gkewebdemo
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
* show the service created by the yaml
```
kubectl get svc
```
_do you realize there is a new service type LoadBalancer and a new IP is assigned to it?_

*  find the defined service and access from external (laptop)

access the IP address from your laptop browser http://loadbalanceripaddress

