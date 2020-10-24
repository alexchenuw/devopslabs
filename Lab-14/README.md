## Lab 14. Expose a pod service to external access
___

> Create a pod with a label

* create a yaml file that defines a pod and a label for the pod
nginxwebpod.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginxwebpod
  labels:
    web: nginx 
spec:
      containers:
      - name: nginxcontainer
        image: nginx
```
* create the pod in k8s
```
kubectl create -f nginxwebpod.yaml
```
> expose the pod to external using NodePort

* create a yaml file that defines the service
nginxwebservice.yaml
```yaml
apiVersion: v1 
kind: Service 
metadata: 
    name: nginxwebexternal 
spec: 
   selector: 
     web: nginx 
   type: NodePort
   ports: 
        - protocol: TCP 
          port: 80 
          targetPort: 80
```
* create the service
```
kubectl create -f nginxwebservice.yaml
```
* check the service

```
kubectl get svc
```
the service should show the NodePort on the k8s nodes, try to access the service with your browser on your local laptop

http://k8snode-public-ip-address:nodeport 

you should be able to access to the default nginx web page on your browser 
