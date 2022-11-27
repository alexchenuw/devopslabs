## Lab. Install a single node k3s cluster
___
> ### Provision the VM environment by creating 1 VM

1. Create 1 vm instances as describle in [lab 1](https://github.com/alexchenuw/devopslabs/tree/main/Lab-1), name the VM as k3sserver-netid

2. Install k3s to the ubuntu vm instance

```bash
curl -sfL https://get.k3s.io | sh -
```
3. show the k3s cluser by running the kubectl command

```bash
sudo kubectl get node
```
4. deploy an application to your k8s cluster
```bash
```
