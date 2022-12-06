## Lab 27. Prep lab for lab 28
___
> This lab include 4 mini labs and they are the build blocks for lab 28, everyone should be able to finish these 4 mini labs as these are labs we did earlier. this lab will manually get all these steps done and at our lab28, we will use a tool (Jenkins)to stitch them together so that these steps can be run in an automation fashion


* >lab 27-1: Create a Dockfile to build a nginx image with a customized index.html
start with a new folder on your VM
```
mkdir lab_27 && cd lab_27
```
create an index.html file with the following content
```html
<!DOCTYPE HTML> 
<html> 
<head> 
<title>This is version 1.0</title> 
</head> 
 
<body> <center>
<div style="width:300px; height: 200px; background-color:green">;
<center><br><br><h1>This is version 1.0</h1></center>
</div> 
</center>
</body> 
</html> 
```
create a Dockerfile with the content
```yaml
FROM nginx
COPY index.html /usr/share/nginx/html
```

* >lab 27-2: Build your nginx image with the Dockerfile and push to dockerhub.com

```
docker build . -t your_dockerhub_repository:1.0.0
```
log on to dockerhub

```
docker login
```
push the image to your dockerhub repository

```
docker push your_dockerhub_repository:1.0.0
```

* >lab 27-3: create a github repository and publish your application 1.0.0 to it

Create a new repository at your github account

Clone this repo to your current folder (lab_27) it should have the Dockerfile and index.html files.

Now, push the these two files to your new github repository.  

> Note: See [lab 8](https://github.com/alexchenuw/devopslabs/tree/main/Lab-8) for additional tips

* >lab 27-4: create a deployment that uses your docker image at dockerhub

cat deployment_lab27_4.yaml

```shell
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mylab27
  labels:
    app: webnginx
spec:
  replicas: 4
  selector:
    matchLabels:
      app: mynginxwebpod
  template:
    metadata:
      labels:
        app: mynginxwebpod
    spec:
      containers:
      - name: nginx
        image: your_dockerhub_repository:1.0.0. <----modify this to your docker image name
        imagePullPolicy: Always 
---
apiVersion: v1 
kind: Service 
metadata: 
    name: mylab27 
spec: 
   selector: 
     app: mynginxwebpod 
   type: NodePort
   ports: 
        - protocol: TCP 
          port: 80 
          targetPort: 80 
```

now, create the deployment and access the application from your laptop

```
kubectl create -f deployment_lab27_4.yaml
```
find the nodeport service port
```
kubectl get svc
```
access your app from external (for example your laptop) via your browser:

http://the-node-public-ip:nodeport


* >lab 27-5. now switch your kubectl to connect the instructor's k8s cluster by copying the kube config file over and override your current one

on your gcp vm workstation:  use uwdevops as the password here.

```
scp devops@10.128.0.23:/etc/kubernetes/admin.conf $HOME/.kube/config
```

your kubectl get node should show you are on the instructor cluster now
```
chenalex@instance-2-achen:~$ kubectl get node
NAME        STATUS   ROLES           AGE   VERSION
k8smaster   Ready    control-plane   35d   v1.25.3
k8snode1    Ready    <none>          35d   v1.25.3
k8snode2    Ready    <none>          35d   v1.25.3
```
and set your kubectl to point to your namespace you created a few weeks back at lab9 on the cluster

```
kubectl config set-context --current --namespace=YOUR_NAME_SAPCE
```

now deploy the lab27_4 deployment again and get the node port service port:
```
kubectl create -f deployment_lab27_4.yaml
```
find the nodeport service port
```
kubectl get svc
```
access your app from external (for example your laptop) via your browser:

http://104.154.96.165:nodeport

****---*** now you are ready for Lab 28!***----***

