## Lab 21. Install a k8s cluster with 3 nodes
___
create 3 vm instances as describle in lab 1
Install docker engine on all three instances as describle in lab 2
```
sudo apt-get update -y
sudo apt-get install docker.io -y
```
make the system run docker automatically after reboot
```
sudo systemctl enable docker
```
> install k8s components to all three instances
 add the sign key
 ```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
```
add the repository and update the repository list again
```
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"

sudo apt-get update -y
```
now install k8s components:

```
sudo apt-get install kubeadm kubelet kubectl -y
```

turn swap off (k8s won't start with swap on)
```
sudo swapoff -a
```
set hostnames on three  instances according to their roles
```
sudo hostnamectl set-hostname k8smaster
```
or
```
sudo hostnamectl set-hostname k8snode1
```
edit /etc/hosts file on three instances and add three lines 
```
sudo vi /etc/hosts
```
```
10.168.0.4    k8smaster
10.168.0.5    k8snode1
10.168.0.7    k8snode2
````

now on the master node:

```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

copy the last log showing "kubeadm join 10.168.0.4..." to the end of the message 

create the k8s cluster directory
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

```

deploy the flannel network pod
```
sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

show all the running system pod

```
kubectl get pod --all-namespaces
```

> now on node

type in the copied message:
```
sudo kubeadm join 10.168.0.4:6443 --token v7ylqj --discovery-token-ca-cert-hash sha256:3f5b65334.cde43
```


on master node, show the cluster
```
kubectl get node
```





