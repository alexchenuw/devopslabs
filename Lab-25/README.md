## Lab 25. Install UI dashboard for k8s cluster (optional)
___

_This lab will be designated as a homework_

a couple of key points are at https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/


* deploy the application into the cluster
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
```

* create a service account and a cluster role to get the token
cat create_user_token.yaml
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
  
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
```
get the token from the user:
```
kubectl create -f create_user_token.yaml
```
get the token:

```
kubectl -n kubernetes-dashboard describe secret admin-user
```

* start the dashboard with
```
kubectl proxy
```
## on your laptop:
* since the proxy is at the VM you are running and you want to access from your local laptop, you need run a SSL forward on your laptop:
```
ssh -L 8001:127.0.0.1:8001 public-ip-of-your-vm
```

* access the UI on your laptop by access 
 http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
 
* Paste the token from earlier step and get authenticated

![dashboard](https://github.com/alexchenuw/devopslabs/blob/main/Lab-25/k8sdashboard.png)

