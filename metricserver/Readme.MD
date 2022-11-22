### Lab K8S Metrics Server installation
___

> ### Install Metrics Server to your cluster

* Locate the installation guide at https://github.com/kubernetes-sigs/metrics-server#installation

* we will need to make changes in the deployment yaml file, so using wget copy the Metric Server deployment file locally first.

```bash
wget https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

* Modify the deployment definition to add a line of "hostNetwork: true" to the ingress controller so that the NGINX pod can access to hostnetwork:
```bash
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
* Verify if the ingress controller has been installed properly:

```
kubectl get pod -A |grep metrics
kube-system     metrics-server-7554578fc-zp6zj              1/1     Running            0                  57s
```

The above pods and their status indicate the ingress controller has been installed properly. You can also tell which node the ingress controller is running on. (also here please tell the instructor your ingress-controller ip as he will need to update the DNS record for your future usage, in this example, ingress controller ip is 10.128.0.35)

> ### now define an ingress service

* create a pod and expose it as a service

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

