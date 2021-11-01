## Lab 9. Install kubectl on your vm and connect it to the class kubernetes cluster
____

> Install kubectl to your Ubuntu vm

* adding the signing key using apt-get

```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
apt-key list
```
* Kubernetes packages are not included in the default repositories. To add them use apt-add-repository.  This will update your sources.list file.

```bash
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
tail /etc/apt/sources.list
```

* now install the kubectl tool on your Ubuntu instance.  Once installed you can confirm the location and version installed.
```
sudo apt-get update -y
sudo apt-get install kubectl -y
which kubectl
kubectl version
```
> Connect your kubectl to the class k8s cluster

* create a directory for the cluster configuration.  You will then copy the cluster configuration from a remote host to your .kube directory and rename the file "config". 

```bash
mkdir -p $HOME/.kube
```
* Now copy the cluster admin configure file to your .kube directory as "config" file.  Note the password for the remote user is **uwdevops**.  Once you have the file copied over locally review the contents of that file.

```bash
scp devops@10.128.0.29:/etc/kubernetes/admin.conf $HOME/.kube/config
cat $HOME/.kube/config
grep "cluster\|server" .kube/config
```
* your kubectl should now be able to connect to the shared k8s cluster.  Later in the course we will install and configure dedicated Kubernetes clusters but initially we are working with a shared running Kubernetes instance.

```
kubectl get node
kubectl cluster-info
```
