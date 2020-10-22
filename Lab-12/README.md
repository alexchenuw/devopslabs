## Lab 12. Create your own namespace and set it as your default namespace
___
> create your own namespace

* create a namespace for yourself on the cluster
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

> set your namespace as your working namespace

* show the namespace you just created
```
kubectl get namespace
```
* set the namespace you just created as your default working namespace 
```
kubectl config set-context --current--namespace=yournamespace
```

* verify you are on your namespace by creating a pod in your new namespace
```
kubectl get pod

kubectl run mynewpod --image=nginx

kubectl get pod
```

you should see the pod now resides in your default namespace now
