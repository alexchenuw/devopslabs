### Lab 24. Install NGINX ingress controller to your k8s cluster and expose an Ingress service
___

> ### Install NGINX ingress controller to your cluster

There are two maintained version of NGINX ingress controllers, one is maintained by k8s and the other is by NGINX, we will use the k8s version at this lab,

* Locate the installation guide at https://kubernetes.github.io/ingress-nginx/deploy/, since we are installing on our baremetal cluster therefore:
https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal

* we will need to make changes in the deployment yaml file, so using wget copy the nginx deploy.yaml file locally first.

```bash
wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.41.2/deploy/static/provider/baremetal/deploy.yaml
```

* Modify the deployment file to add a line of "hostNetwork: true" so that the NGINX pod can access to hostnetwork:

```yaml
 template:
    metadata:
      labels:
        app.kubernetes.io/name: ingress-nginx
        app.kubernetes.io/instance: ingress-nginx
        app.kubernetes.io/component: controller
    spec:
      dnsPolicy: ClusterFirst
      hostNetwork: true
      containers:
        - name: controller          
``` 

* Now install the NGINX ingress controller by applying the deployment yaml file:
```
kubectl create -f deploy.yaml
```
* Verify if the ingress controller has been installed properly:

```
kubectl get pod -n ingress-nginx
NAME                                       READY   STATUS      RESTARTS   AGE
ingress-nginx-admission-create-qgdfx       0/1     Completed   0          47h
ingress-nginx-admission-patch-v7j9b        0/1     Completed   1          47h
ingress-nginx-controller-cf9756865-c8gx7   1/1     Running     0          47h
```

The above pods and their status indicate the ingress controller has been installed properly.

> ### now define an ingress service

* Find the service you want to expose using Ingress

```
kubectl get svc
```
* Create an Ingress yaml file called `ingress_example.yaml` based on the configuration example provided below.  This should expose a service named myfirst-ingress

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myfirst-ingress
spec:
  rules:
  - host: yournet-id.alexchen.me
    http:
      paths:
      - path: /
        pathType: Prefix        
        backend:
          service:
            name: lab19external
            port:
              number: 80
```

* Now create and display Ingress details.

```bash
kubectl create -f ingress_example.yaml
kubectl get ingress
kubectl describe ingress
```

* Make changes on DNS setting to map the FQDN to the ingress IP address

Now, try access the FQDN from your browser


* now add a second service to the same Ingress
cat ingress_example.yaml
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myfirst-ingress
spec:
  rules:
  - host: younetid.alexchen.me
    http:
      paths:
      - path: /
        pathType: Prefix        
        backend:
          service:
            name: lab19external
            port:
              number: 80
  - host: mynetid.alexchen.me
    http:
      paths:
      - path: /
        pathType: Prefix        
        backend:
          service:
            name: secondservice
            port:
              number: 80

```
* make the update to the ingress then display it:

```
kubectl apply -f ingress_example.yaml
```
```
kubectl get ingress
```
![ingress controller](https://github.com/alexchenuw/devopslabs/blob/main/Lab-24/ingress-lab24.png)

* now tell Instructor Alex the ip address to add the DNS resource record

* access both FQDN from your browser 

