
### Upgrade Docker from 18.09 to 19.03 on Ubuntu 16.04
---
_Docker 18.09 has a known issue where it does not work well with k8s v1.19 that sometimes it does not report the pod metrics to metrics server, the resolution is to upgrade the docker version to 19.03_

> 1. purge the current version of Docker

```
sudo apt-get purge docker.io
```
> 2. add the GPG key for the official Docker repository to your system

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
> 3. add Docker repository to APT source

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
> 4. update the package database

```
sudo apt-get update -y
```
> 5. install the most recent version of Docker

```
sudo apt-get install -y docker-ce
```
> 6. add user to docker group so no "sudo" is needed to run Docker

```
sudo usermod -aG docker $USER
```
