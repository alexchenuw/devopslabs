## Lab 12. Create a new namespace and set it as your default namespace
___
> create a new namespace based on your NetID

* create a new namespace on the cluster
>Note: Replace $USER with your UW NetID.

```bash
kubectl create namespace $USER
```
_you can also create the namespace from a yaml file as the following, it will get you the same result_

```yaml
apiVersion: v1
kind: Namespace
metadata:
   name: $USER
```
Assuming your namespace file is called namespace.yaml run the following command

```bash
kubectl create -f namespace.yaml 
```

> set the new namespace as your default working namespace

* show the namespace you just created

```bash
kubectl get namespace
```

* set the namespace you just created as your default working namespace

>Note: Replace $USER with your UW NetID

```bash
kubectl config set-context --current --namespace=$USER
```

* verify you are on your namespace by creating a pod and display the pod
```
kubectl get pod
kubectl run mynewpod --image=nginx
kubectl get pod
kubectl get pod -o wide
kubectl get pod --all-namespaces
```

you should see the pod now resides in your default namespace now

> Question: Where is your default namespace value stored?  hint check the configuration file under .kube
