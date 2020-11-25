## Lab 23. Deploy a static pod to the k8s cluster
___

_In this lab, we will learn how to deploy a pod into an k8s cluster node so that it will always be running as a system service_  

The three key steps are:
  1. create a yaml file defining your pod
  2. find the static pod folder location
  3. copy the pod yaml file into the folder
  
* Create a yaml file called `static_logging_pod.yaml` defining the pod

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

* Find the static pod folder location

The static pod will run on the node where you create the static pod yaml file.  This could be your master or any of workder nodes.  Now login to the node where you want to install this static pod.  Once you have logged into your target host we need to locate the kubectl config.yaml file.  The output from the following command should point to this file.  

```bash
sudo systemctl status kubelet |grep config
```
> If you are struggling to find the file look for `--config` and something similar to `/var/lib/kubelet/config.yaml`.

Now open this file and search for the line that maps the `staticPodPath` to a diretory.  It probably looks similar to the example show below.

```shell
staticPodPath: /etc/kubernetes/manifests
```

This directory is where we will copy our `static_logging_pod.yaml` file, you may also notice some other yaml files if you are doing this on your master node.  

* Copy your defined yaml file into the folder

```
sudo cp static_logging_pod.yaml /etc/kubernetes/manifests/static_logging_pod.yaml
```
Restart the kubelet service and check if the pod is now running on the node

```
sudo systemctl restart kubelet
kubectl get pod
```
Try to delete the pod and see what happens:

```
kubectl delete pod static-logging-xxx
kubectl get pod
```
(you should see the pod is recreated again)
