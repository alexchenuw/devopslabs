## Lab 2. Installing Docker engine to your Ubuntu VM
___
This lab is to install the current version of Docker engine to your Ubuntu 16.04 instance in Google Cloud

* login to your VM through SSH
```bash
ssh yournetID@the-public-ip-address-of-your-VM
```
* update the apt-get install package list: 
```bash
sudo apt-get update -y
```
* install the current version of Docker engine: 
```bash
sudo apt-get install docker.io -y
```
* add yourself to the docker group 
```bash
sudo usermod -aG docker your-user-name
```
* log out to the VM and log back in.

```bash
exit
ssh yournetID@public-ip-of-ur-host
```

* run command 
```bash 
docker version
```
it should show the docker version if docker has been successfully installed
