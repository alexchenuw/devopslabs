## Lab 25. Install UI dashboard for k8s cluster
___

_This lab will be designated as a homework_

a couple of key points are at https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/


* deploy the application into the cluster
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
```

* create a service account and a cluster role to get the token

https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md

* start the dashboard with
```
kubectl proxy
```

* since the proxy is at the VM you are running and you want to access from your local laptop, you need a SSL forward
```
ssh -L 8001:127.0.0.1:8001 public-ip-of-your-vm
```

* access the UI on your laptop by access 
 http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
 
* Paste the token from earlier step and get authenticated

![dashboard](https://github.com/alexchenuw/devopslabs/blob/main/Lab-25/k8sdashboard.png)

