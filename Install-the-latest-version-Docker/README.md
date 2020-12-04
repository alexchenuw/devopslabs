
### Upgrade Docker from 18.09 to 19.03 on Ubuntu 16.04
---

> purge the current version of Docker

```
sudo apt-get purge docker.io
```
> add the GPG key for the official Docker repository to your system

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
> add Docker repository to APT source

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
> update the package database

```
sudo apt-get update -y
```
>install the most recent version of Docker

```
sudo apt-get install -y docker-ce
```
