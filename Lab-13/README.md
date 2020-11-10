## Lab 13. using Nodeselector to select a specified node for a pod
____

> Label a node with a customized label, here we are creating a label based on your User Id and setting the value to "amd"
* Label a work node with label nodecpu-$USER=amd

```bash
kubectl label node k8snode2 nodecpu-$USER=amd
```
* show the labels on k8s nodes
```
kubectl get node --show-labels
```

If you want to remove a label replace the label value with "-" as shown in this example.

```bash
# kubectl label node k8snode2 nodecpu-$USER-
```

> Create a pod and have k8s schedule the pod to k8snode2 using nodeselector

* create the pod definition yaml file called `nodeselectorpod.yaml`.  
>Note: replace $USER with your UW-NetID to match the label created in the previous steps.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nodeselectpod
spec:
  containers:
    - name: hello
      image: busybox
      command: ['sh', '-c', 'echo "Hello, Kubernetes!" && sleep 3600']
  nodeSelector:
      nodecpu-$USER: amd
```
* create the pod

```bash
kubectl create -f nodeselectorpod.yaml
```
* verify the pod has been created and scheduled to k8snode2 and review the pod events using "pod describe".

```bash
kubectl get pod -o wide
kubectl describe po/nodeselectpod
```
you should find your pod has been created and is running on k8snode2

