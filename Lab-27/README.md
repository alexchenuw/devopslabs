## Lab 27. Prep lab for lab 28
___
> This lab include 4 mini labs and they are the build blocks for lab 28, everyone should be able to finish these 4 mini labs as these are labs we did earlier.

* >lab 27-1: Create a Dockfile to build a nginx image with a customized index.html
start with a new folder on your VM
```
mkdir lab_27 && cd lab_27
```
create an index.html file with the following content
```html
<center><h1>This is version 1.0.0</center>
```
create a Dockerfile with the content
```yaml
FROM nginx
COPY index.html /usr/share/nginx/html
```

* lab 27-2: Build your nginx image with the Dockerfile and push to dockerhub.com

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

* lab 27-3: create a github repository and publish your application 1.0.0 to it

Create a new repository at your github account
Conduct git init in your current folder that has Dockerfile and index.html
Push the these two files to github repository as


* lab 27-4: create a deployment that uses your docker image at dockerhub

cat deployment_lab27_4.yaml
```
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
      app: nginxwebpod
  template:
    metadata:
      labels:
        app: nginxwebpod
    spec:
      containers:
      - name: nginx
        image: your_dockerhub_repository:1.0.0. <----modify this to your docker image name
        
---
apiVersion: v1 
kind: Service 
metadata: 
    name: mylab27 
spec: 
   selector: 
     app: nginxwebpod 
   type: NodePort
   ports: 
        - protocol: TCP 
          port: 80 
          targetPort: 80
          
```






