## Lab 10. Deploy a NGINX pod in the k8s environment

* deploy a nginx pod
```bash
kubectl run myfirstpod --image=nginx
```

* run a few commands to get to know more about the pod

```
kubectl get pod myfirstpod
kubectl get pod myfirstpod -o wide
kubectl describe pod myfirstpod
kubectl logs myfirstpod
```
