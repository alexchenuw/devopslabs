## Lab. Install a single node k3s cluster
___
> ### Provision the VM environment by creating 1 VM

1. Create 1 vm instances as describle in [lab 1](https://github.com/alexchenuw/devopslabs/tree/main/Lab-1), name the VM as k3sserver-netid

2. Install k3s to the ubuntu vm instance

```bash
curl -sfL https://get.k3s.io | sh -
```
3. show the k3s cluser by running the kubectl command

```bash
sudo kubectl get node
```
4. deploy an application to your k8s cluster, for example, the application you deployed at lab19
```bash
sudo vi lab19_on_k3s.yaml
```
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
```bash
sudo kubectl create -f lab19_on_k3s.yaml
```
5. check on the deployment,pod and services on the k3s, and verify the application by access to the nodeport service from your laptop


```bash
sudo kubectl get node
sudo kubectl get svc
sudo kubectl get deployment
sudo kubectl get pod
```
