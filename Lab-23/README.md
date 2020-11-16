## Lab 23. Deploy a static pod to the k8s cluster
___

_At this lab, we will learn how to deploy a pod into k8s cluster node so that it will always be running as a system service_
Three key steps
  1. create a yaml file defining your pod
  2. find the static pod folder location
  3. copy the pod yaml file into the folder
  
* Create a yaml file defining the pod

cat static_logging_pod.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: static-logging
  labels:
    created_by: lab23
spec:
  containers:
    - name: logging-container
      image: fluentd
```

* find the static pod folder location

on the target node (could be master, node1 or node2 of your choice), ssh into the node then,
```
sudo systemctl status kubelet |grep config
```
you should be able to get the --config file is /var/lib/kubelet/config.yaml.

look into the file and find the line that defines staticpod, something like:

```
staticPodPath: /etc/kubernetes/manifests
```
that is the folder for the static pod.

* copy your defined yaml file into the folder

```
sudo cp static_logging_pod.yaml /etc/kubernetes/manifests/static_logging_pod.yaml
```
restart the kubelet service and check if the pod is already running on the node

```
sudo systemctl restart kubelet
kubectl get pod
```
try to delete the pod and see what happens:

```
kubectl delete pod static-logging-xxx
kubectl get pod
```
(you should see the pod is recreated again)
