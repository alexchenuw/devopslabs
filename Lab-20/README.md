## Lab 20. Scale out/in a deployment, roll update a deployment
___

_This lab we will be simulating a couple of application administration scenarios: scale out and in the traffic processing capacity, upgrade/downgrade the container images and rolling back from the upgrade/downgrade_

* create the deployment from lab 19 again if it has been deleted/removed
```
kubectl create -f lab19_combined.yaml
```
* check the current traffic processing capacity of the application(deployment) and you should see 4 pods
```
kubectl get pod -l app=nginxwebpod
````
or
```
kubectl get replicaset
```

> scale out/in number of pods for the deployment

* scale the deployment to 10 pods from 4 pods

```
kubectl scale deployment achenwebdemo --replicas=10
kubectl get deployment achenwebdemo
kubectl get pod
```
* scale the deployment to any number you like


> ### upgrade/downgrade the nginx container image to the [AienInvasion image](https://github.com/alexchenuw/devopslabs/tree/main/Lab-6) you have created earlier, in my case it is alexchen2015/alex001:mypersonalnginx
[lab 4 push an image to dockerhub](https://github.com/alexchenuw/devopslabs/blob/main/Lab-4/README.md)

* upgrade the nginx image in the deplpoyment to my version
```
kubectl set image deployment/achenwebdemo nginx=alexchen2015/alex001:mypersonalnginx --record
```
* track the upgrade status
```
kubectl rollout status deployment achenwebdemo
```
* check the deployment or pods
```
kubectl describe deployment achenwebdemo
kubectl get pod
```
* browse the service with your browser on the following port 

```
kubectl get svc
```

* now roll back to original nginx container version
```
kubectl rollout undo deployment achenwebdemo
```

* browse the service again, the application should have been reverted

