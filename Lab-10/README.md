## Lab 10. Deploy a NGINX pod in the k8s environment

* deploy a nginx pod, choose a name with your netid as the pod name so it is unique with pods created by other students
```bash
kubectl run myfirstpod-achen --image=nginx
```

* run a few commands to get to know more about the pod

```
kubectl get pod myfirstpod-achen
kubectl get pod myfirstpod-achen -o wide
kubectl describe pod myfirstpod-achen
kubectl logs myfirstpod-achen
```
