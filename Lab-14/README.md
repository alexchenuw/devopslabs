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

```bash
kubectl create -f nginxwebpod.yaml
kubectl get pod/nginxwebpod -o wide
```

> expose the pod to external clients using a NodePort

* create a yaml file that defines the service called nginxwebservice.yaml

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

```bash
kubectl create -f nginxwebservice.yaml
```

* check the service

```bash
kubectl get svc
kubectl get service -o wide
```

The service should show the NodePort on the k8s nodes, try to access the service from the command line and using the browser on your local laptop.  You will need an IP address from one of the nodes and then you will need the kubernetes assigned node port.

```bash
kubectl get nodes -o wide
kubectl get service nginxwebexternal
curl http://{kubernetes node ip}:{kubernetes nodeport}
```

>Note: you will need to find a public k8s node IP address in the [Google web console](https://console.cloud.google.com)
http://k8snode-public-ip-address:nodeport 

you should be able to access to the default nginx web page on your browser 

> Question: If you have two nodes but have only deployed your pod to ONE node can you send a request to the nodeport on EITHER node and recieve the same results?
