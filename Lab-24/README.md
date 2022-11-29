### Lab 24. Install NGINX ingress controller to your k8s cluster and expose an Ingress service
___

> ### Install NGINX ingress controller to your cluster

There are two maintained version of NGINX ingress controllers, one is maintained by k8s and the other is by NGINX, we will use the k8s version at this lab,

* Locate the installation guide at https://kubernetes.github.io/ingress-nginx/deploy/, since we are installing on our baremetal cluster therefore:
https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal-clusters

* we will need to make changes in the deployment yaml file, so using wget copy the nginx deploy.yaml file locally first.

```bash
wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.5.1/deploy/static/provider/cloud/deploy.yaml
```

* Modify the deployment definition to add a line of "hostNetwork: true" to the ingress controller so that the NGINX pod can access to hostnetwork:
```bash
vi deploy.yaml
```

```yaml
        volumeMounts:
        - mountPath: /usr/local/certificates/
          name: webhook-cert
          readOnly: true
      dnsPolicy: ClusterFirst
      hostNetwork: true <-----add this one line only
      nodeSelector:
        kubernetes.io/os: linux
      serviceAccountName: ingress-nginx
      terminationGracePeriodSeconds: 300
      volumes:
      - name: webhook-cert
        secret:
          secretName: ingress-nginx-admission
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

The above pods and their status indicate the ingress controller has been installed properly. You can also tell which node the ingress controller is running on. (also here please tell the instructor your ingress-controller ip as he will need to update the DNS record for your future usage, in this example, ingress controller ip is 10.128.0.35)

> ### now define an ingress service

* create a pod and expose it as a service

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginxwebpod
  labels:
    web: nginxweb 
spec:
  containers:
    - name: nginxweb
      image: nginx

---
apiVersion: v1 
kind: Service 
metadata: 
    name: nginxwebservice 
spec: 
   selector: 
     web: nginxweb 
   type: NodePort
   ports: 
        - protocol: TCP 
          port: 80 
          targetPort: 80

```
```bash
kubectl get svc
```
* Create an Ingress yaml file called `ingress_example.yaml` based on the configuration example provided below.  This should expose a service named myfirst-ingress

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myfirst-ingress
spec:
  ingressClassName: nginx
  rules:
  - host: your-netid.alexchen.me
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: nginxwebservice
            port:
              number: 80

```

* Now create and display Ingress details.

```bash
kubectl create -f ingress_example.yaml
kubectl get ingress
kubectl describe ingress
```
![ingress controller](https://github.com/alexchenuw/devopslabs/blob/main/Lab-24/ingress-lab24-1.png)


Now, try access the FQDN from your browser, you should be able to see the default nginx webpage with your browser


___
* now add a second service to the same Ingress
cat ingress_example.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginxwebpod
  labels:
    web: nginxweb 
spec:
  containers:
    - name: nginxweb
      image: nginx

---
apiVersion: v1
kind: Pod
metadata:
  name: nginxapple
  labels:
    web: nginxapple
spec:
      containers:
      containers:
        - name: apple-web
          image: hashicorp/http-echo
          args:
            - "-text=apple"
---
apiVersion: v1 
kind: Service 
metadata: 
    name: nginxwebservice 
spec: 
   selector: 
     web: nginxweb 
   type: NodePort
   ports: 
        - protocol: TCP 
          port: 80 
          targetPort: 80
---
apiVersion: v1
kind: Service
metadata:
    name: nginxapplesvc
spec:
   selector:
     web: nginxapple
   type: NodePort
   ports:
        - protocol: TCP
          port: 5678
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myfirst-ingress
spec:
  ingressClassName: nginx
  rules:
  - host: lab24.alexchen.me
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: nginxwebservice
            port:
              number: 80
      - path: /apple
        pathType: Prefix
        backend:
          service:
            name: nginxapplesvc
            port:
              number: 5678
```
* make the update to the ingress then display it:

```
kubectl apply -f ingress_example.yaml
```
```
kubectl get ingress
```

*  access FQDN from your browser 

http://your-netid.alexchen.me

http://your-netid.alexchen.me/apple


