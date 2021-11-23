### Lab 24. Install NGINX ingress controller to your k8s cluster and expose an Ingress service
___

> ### Install NGINX ingress controller to your cluster

There are two maintained version of NGINX ingress controllers, one is maintained by k8s and the other is by NGINX, we will use the k8s version at this lab,

* Locate the installation guide at https://kubernetes.github.io/ingress-nginx/deploy/, since we are installing on our baremetal cluster therefore:
https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal-clusters

* we will need to make changes in the deployment yaml file, so using wget copy the nginx deploy.yaml file locally first.

```bash
wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.0.5/deploy/static/provider/baremetal/deploy.yaml
```

* Modify the deployment definition to add a line of "hostNetwork: true" to the ingress controller so that the NGINX pod can access to hostnetwork:
```bash
vi deploy.yaml
```

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
          image: k8s.gcr.io/ingress-nginx/controller:v1.0.5@sha256:55a1fcda5b7657c372515fe402c3e39ad93aa59f6e4378e82acd99912fe6028d
          imagePullPolicy: IfNotPresent   
``` 

* Now install the NGINX ingress controller by applying the deployment yaml file:
```
kubectl create -f deploy.yaml
```
* Verify if the ingress controller has been installed properly:

```
kubectl get pod -n ingress-nginx -o wide
NAME                                       READY   STATUS      RESTARTS   AGE   IP            NODE         NOMINATED NODE   READINESS GATES
ingress-nginx-admission-create--1-7glmr    0/1     Completed   0          11m   10.244.1.37   achen-node   <none>           <none>
ingress-nginx-admission-patch--1-b6tfm     0/1     Completed   0          11m   10.244.1.38   achen-node   <none>           <none>
ingress-nginx-controller-75f465cc7-5882c   1/1     Running     0          11m   10.128.0.35   achen-node   <none>           <none>
```

The above pods and their status indicate the ingress controller has been installed properly. You can also tell which node the ingress controller is running on.

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
![ingress controller](https://github.com/alexchenuw/devopslabs/blob/main/Lab-24/ingress-lab24.png)

* Tell Instructor the ip address of your ingress and he will make changes on DNS setting to map the FQDN to the ingress IP address

Now, try access the FQDN from your browser


___
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
        - path: /orange
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

*  access both FQDN from your browser 

