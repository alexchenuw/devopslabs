## Lab 15. Create a DaemonSet to run a fluentd pod on all k8s working nodes
___

* create a yaml file to run a fluentd pod on each k8s node (do not include the master node) called `fluentd-daemonset.yaml`
> Note: Change $USER to reflect your UW NetID

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: $USER-fluentd
  namespace: kube-system
  labels:
    k8sapp: my-fluentd-logging
spec:
  selector:
    matchLabels:
      name: my-fluentd
  template:
    metadata:
      labels:
        name: my-fluentd
    spec:
      containers:
      - name: my-fluentd-container
        image: fluentd
```
* create the daemonSet
```
kubectl create -f fluentd-daemonset.yaml
```
* check if a fluentd pod is running on each working node
```
kubectl get pods -n kube-system -o wide
```

> Question: Why do you see two instances of fluentd deployed to the kube-system namespace?
