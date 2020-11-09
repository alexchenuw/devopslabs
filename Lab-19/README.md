## Lab 19. Create a deployment and expose its service using NodePort
___

_With Lab 19, we will be creating a deployment and then expose the deployment as a service for external users as NodePort, this will be a very typical application deployment scenario_
_we will also experience how a replicaset plays its role to maintain a desired number of pods_

> ## create a deployment with a yaml file

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

> ## Expose the deployment to an external service using NodePort

cover the replicaset coverage where when you delete/remove a pod manually, a new one will be spun up to meet the "desired" state

