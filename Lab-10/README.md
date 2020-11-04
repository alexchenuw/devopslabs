## Lab 10. Deploy a NGINX pod in the k8s environment

* deploy a nginx pod using your netid in the name.  This will ensure we have unique pods created in the lab.  

>Note: Replace $USER with your uw netID.  If you don't replace $USER with your netID your linux host will replace that variable with the userid used to login to your linux host.

```bash
kubectl run myfirstpod-$USER --image=nginx
```

* Now run the following commands to extract details from your pod.  See if you can answer these questions.

1. What is the status of your pod?
1. What is the IP address assigned to your pod? 
1. What node is your pod running on? 
1. What is your pod container ID?

```bash
kubectl get pod myfirstpod-$USER
kubectl get pod myfirstpod-$USER -o wide
kubectl describe pod myfirstpod-$USER
kubectl logs myfirstpod-$USER
```
