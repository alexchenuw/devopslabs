## Lab 21. Install a k8s cluster with 3 nodes
___
> ### Provision the VM environment by creating 3 VMs

1. Create 3 vm instances as describle in [lab 1](https://github.com/alexchenuw/devopslabs/tree/main/Lab-1)
use k8smaster-netid as the VM names, follow the format like k8smaster-chenalex, k8snode1-chenalex and k8snode2-chenalex

2. Install docker engine on all three instances as describle in lab 2

```bash
sudo apt-get update -y
sudo apt-get install docker.io -y
```

3. Make the system run docker automatically after reboot

```bash
sudo systemctl enable docker
```

> ### Install k8s components to all three instances
4. add the sign key

 ```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
```

5. Add the repository and update the repository list again

```bash
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt-get update -y
```

6. now install k8s components:

```bash
sudo apt-get install kubeadm kubelet kubectl -y
```

7. turn swap off (k8s won't start with swap on)

```bash
sudo swapoff -a
```

8. set hostnames on three instances according to their roles

```bash
sudo hostnamectl set-hostname k8smaster-chenalex
```

or

```bash
sudo hostnamectl set-hostname k8snode1-chenalex
```

9. find the ip address of the three VMs on the console and edit /etc/hosts file on three instances and add three lines

```bash
sudo vi /etc/hosts
```

```bash
10.1xx.0.4    k8smaster-chenalex
10.1xx.0.5    k8snode1-chenalex
10.1xx.0.7    k8snode2-chenalex
```

> ### Now on the master node:
10. Initial the cluster setup by running

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

11. copy the last log showing something like "kubeadm join 10.168.0.4..." to the end of the message, we will use this message later

12. create the k8s kubectl directory

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

13. deploy the flannel network pod

```bash
sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

14. show all the running system pod

```
kubectl get pod --all-namespaces
```

>  ### now run the following command on each of the two node VMs:

15. paste in the message copied earlier from step 11:
```
sudo kubeadm join 10.168.0.4:6443 --token v7ylqj --discovery-token-ca-cert-hash sha256:3f5b65334.cde43
```

16. Get back to the master node, show the cluster

```bash
kubectl get node
```

17. set the kubectl on your workstation VM to point to the cluster created here
    ## Still remember how to do this? refer to lab 9, last two steps




