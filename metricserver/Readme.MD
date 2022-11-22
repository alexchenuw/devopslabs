### Lab K8S Metrics Server installation
___

> ### Install Metrics Server to your cluster

* Locate the installation guide at https://github.com/kubernetes-sigs/metrics-server#installation

* we will need to make changes in the deployment yaml file, therefore using wget to download the Metric Server deployment file to local first.

```bash
wget https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

* Modify the deployment file and add one line as "- --kubelet-insecure-tls" and also modify the other line to set the preferred-address as internalIP:
vi components.yaml
```

```yaml
    - --kubelet-insecure-tls
    - --kubelet-preferred-address-types=InternalIP
``` 

* Now install the metric server by applying the deployment yaml file:
```
kubectl create -f components.yaml
```
* Verify if the metrics server has been installed properly:

```
kubectl get pod -A |grep metrics
kube-system     metrics-server-7554578fc-zp6zj              1/1     Running            0                  57s
```

* now you can use kubectl top command to get the resource usage info on the node and pod level

```
kubectl top node
NAME        CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%   
k8smaster   134m         3%     1965Mi          12%       
k8snode1    215m         5%     2269Mi          14%       
k8snode2    311m         7%     2039Mi          12%       

```
```
kubectl top pod
NAME                  CPU(cores)   MEMORY(bytes)   
aaachen-pod-default   0m           6Mi             
liveness-exec         4m           1Mi             
nginxwebpod           0m           5Mi             
ssdpod                0m           0Mi   

```

