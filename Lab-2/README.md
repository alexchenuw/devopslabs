## Lab 2. Installing Docker engine to your Ubuntu VM
___

This lab will walk you through installing the current version of Docker engine on your Ubuntu 16.04 instance in Google Cloud.  In this example we are installing Docker from the default Ubuntu repositories. It is possible to add the official docker repositories to your host and install addtional versions of docker.  See [docs.docker.com for details](https://docs.docker.com/engine/install/ubuntu/)

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
sudo usermod -aG docker $USER
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

This should show the docker version if it has been successfully installed.
___
To see the availalbe versions of docker to install use

```bash
sudo apt-cache madison docker.io
```

