## Lab 9. Install kubectl on your vm and connect it to the class kubernetes cluster
____

> Install kubectl to your Ubuntu vm

* adding the signing key to apt-get
```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
```
* Kubernetes packages are not included in the default repositories. To add them, enter the following:
```
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
```
* now install the kubectl tool to your Ubuntu instance
```
sudo apt-get update -y
sudo apt-get install kubectl -y
```
> Connect your kubectl to the class k8s cluster

* create a directory for the cluster
```
mkdir -p $HOME/.kube
```
* copy the cluster admin configure file to your .kube directory as "config" file, password (uwdevops)
```
scp devops@10.168.0.4:/etc/Kubernetes/admin.conf $HOME/.kube/config
```
* your kubectl should be able to connect to the k8s cluster

```
kubectl get node
```
