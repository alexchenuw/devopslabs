## Lab 19. Create a deployment and expose its service using NodePort
___

_With Lab 19, we will be creating a deployment and then expose the deployment as a service for external users as NodePort, this will be a very typical application deployment scenario_
_we will also experience how a replicaset plays its role to maintain a desired number of pods_

> create a deployment with a yaml file

cat lab19_deployment.yaml
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
```
* create the deployment
```
kubectl create -f lab19_deployment.yaml
```
* check how many pods have been created by the deployment
```
kubectl get deployment achenwebdemo
```
* show the replicaset 
```
kubectl get replicaset 
kubectl describe replicaset achenwebdemo
```
* show the pods created by this deployment
```
kubectl get pod -l app=nginxwebpod
```
* try to manually delete the pods, you should be able to see another set of pods created to meet replicas=4
```
kubectl delete pod -l app=nginxwebpod
```

> Expose the deployment to an external service using NodePort

* create a service that expose the deployment to external using NodePort

cat lab19_service.yaml
```yaml
apiVersion: v1 
kind: Service 
metadata: 
    name: lab19external 
spec: 
   selector: 
     app: nginxwebpod 
   type: NodePort
   ports: 
        - protocol: TCP 
          port: 80 
          targetPort: 80
```
* create the service
```
kubectl create -f lab19_service.yaml
```
* show the service
```
kubectl get svc lab19external
```
* find the external port number and try to access the service from your laptop

> ## in fact, you can combine the yaml with a "---"

so the combined deployment and service yaml file is like:

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
   type: NodePort
   ports: 
        - protocol: TCP 
          port: 80 
          targetPort: 80
```


