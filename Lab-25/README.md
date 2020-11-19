### Lab 25. Install NGINX ingress controller to your k8s cluster and expose an Ingress service
___

> Install NGINX ingress controller to your cluster

There are two maintained version of NGINX ingress controllers, one is maintained by k8s and the other is by NGINX, we will use the k8s version at this lab,

* Locate the installation guide at https://kubernetes.github.io/ingress-nginx/deploy/, since we are installing on our baremetal cluster therefore:
https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal

* we need make changes on the deployment yaml file so we download the deployment file first:
```
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
          image: k8s.gcr.io/ingress-nginx/controller:v0.41.2@sha256:1f4f402b9c14f3ae92b11ada1dfe9893a88f0faeb0b2f4b903e2c67a0c3bf0de
          imagePullPolicy: IfNotPresent
          
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

> create an ingress service

* Find the service you want to expose using Ingress

```
kubectl get svc
```
* Define an Ingress to expose a service named mywebservice

cat ingress_example.yaml

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: ingress-example
spec:
  rules:
    - host: www.ingress123.com 
      http:
        paths:
          - path: /
            backend:
              serviceName: mywebservice 
              servicePort: 80
```

* Display the Ingress detail info

```
kubectl get ingress
```

* Make changes on DNS setting to map the FQDN to the ingress IP address

Now, try access the FQDN from your browser


* now add a second service to the same Ingress
cat ingress_example.yaml
```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: ingress-example
spec:
  rules:
    - host: www.ingress123.com 
      http:
        paths:
          - path: /
            backend:
              serviceName: mywebservice 
              servicePort: 80
    
    - host: www.anotherweb.com 
      http:
        paths:
          - path: /
            backend:
              serviceName: nginxingress 
              servicePort: 8090
```
* make the update to the ingress then display it:

```
kubectl apply -f ingress_example.yaml
```
```
kubectl get ingress
```

* add the DNS record to map the second FQDN to the ingress on your laptop

* access both FQDN from your browser 

