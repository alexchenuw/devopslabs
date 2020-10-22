## Lab 12. Create a new namespace and set it as your default namespace
___
> create a new namespace

* create a new namespace on the cluster
```
kubectl create namespace <name of your namespace, use your netid here>
```
_you can also create the namespace from a yaml file as the following, it will get you the same result_
```yaml
apiVersion: v1
kind: Namespace
metadata:
   name: <name of your namespace, use your netid as the name here>
```

> set the new namespace as your default working namespace

* show the namespace you just created
```
kubectl get namespace
```
* set the namespace you just created as your default working namespace 
```
kubectl config set-context --current--namespace=yournamespace
```

* verify you are on your namespace by creating a pod and display the pod
```
kubectl get pod

kubectl run mynewpod --image=nginx

kubectl get pod

kubectl get pod --all-namespaces
```

you should see the pod now resides in your default namespace now
