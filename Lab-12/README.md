## Lab 12. Create your own namespace and set it as your work namespace
___
> create your own namespace

* create a namespace for yourself on the cluster
```
kubectl create namespace <name of your namespace, use your netid here>
```
you can also create the namespace from a yaml file
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
* set the namespace you just created as your working namespace 
```
kubectl config set-context --current--namespace=yournamespace
```

* verify you are on your namespace
```
kubectl get pod

kubectl run mynewpod --image=nginx
```

create a pod 
