## Lab 13. using Nodeselector to select a specified node for a pod
____

> Label a node with a customized label
* Label a work node with label nodecpu=amd
```
kubectl label node k8snode2 nodecpu=amd
```
* show the labels on k8s nodes
```
kubectl get node --show-labels
```

> Create a pod and have k8s schedule the pod to k8snode2 using nodeselector

* create the pod definition yaml file
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
      nodecpu: amd
```
* create the pod
```
kubectl create -f nodeselectorpod.yaml
```
* verify the pod has been created and scheduled to k8snode2
```
kubectl get pod -o wide
```
you should find your pod has been created and is running on k8snode2

