## Lab 19. Create a deployment and expose its service using NodePort
___

_With Lab 19, we will be creating a deployment and then expose the deployment as a service for external users as NodePort, this will be a very typical application deployment scenario_
_we will also experience how a replicaset plays its role to maintain a desired number of pods_

> create a deployment file called `lab19_deployment.yaml` replace ${USER} with your userID

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ${USER}webdemo
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

* create the deployment adn check how many pods have been created by the deployment

```bash
kubectl create -f lab19_deployment.yaml
kubectl get deployment ${USER}nwebdemo
```

* show the replicaset 

```bash
kubectl get replicaset 
kubectl describe replicaset ${USER}:webdemo
```
* show the pods created by this deployment

```bash
kubectl get pod -l app=nginxwebpod
```
* try to manually delete the pods, you should be able to see another set of pods created to meet replicas=4

```bash
kubectl delete pod -l app=nginxwebpod
```

> Expose the deployment to an external service using NodePort

* create a service file called 'lab19_service.yaml` that expose the deployment to external using NodePort

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

* create the service and list the service

```bash
kubectl create -f lab19_service.yaml
kubectl get svc lab19external
```

* find the external port number and try to access the service from your laptop

> ## You can combine yaml files using a "---"  We can define the deployment and the service in the same file.  Create a new file called `lab19_combined.yaml`

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

* delete the earlier deployment and service first

```bash
kubectl delete -f lab19_service.yaml
kubectl delete -f lab19_deployment.yaml
```
* now run create the deployment and service together

```bash
kubectl create -f lab19_combined.yaml
```
* verify the deployment and service

