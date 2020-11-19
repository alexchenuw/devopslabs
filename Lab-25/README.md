Lab 25. install NGINX ingress controller to your k8s cluster
___

locate the installation guide at https://kubernetes.github.io/ingress-nginx/deploy/

since we are installing on our baremetal cluster:
https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal

wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.41.2/deploy/static/provider/baremetal/deploy.yaml

* modify the deployment to add a line of "hostNetwork: true"

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

* install the NGINX ingress controller
```
kubectl create -f deploy.yaml
```
* verify if the ingress controller has been installed properly

```
kubectl get pod -n ingress-nginx
NAME                                       READY   STATUS      RESTARTS   AGE
ingress-nginx-admission-create-qgdfx       0/1     Completed   0          47h
ingress-nginx-admission-patch-v7j9b        0/1     Completed   1          47h
ingress-nginx-controller-cf9756865-c8gx7   1/1     Running     0          47h
```


