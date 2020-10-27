## Lab 6. Containerize a game app and push the image to Dockerhub
____
> install git

* Install git on your Google VM
```
sudo apt-get update -y
sudo apt-get install git 
```

> containerize a game app 

* create a the directory "lab-6" in your home directory and change to that directory.

```bash
cd
mkdir lab-6
cd lab-6
```

* download a github hosted game app from https://github.com/cykod/AlienInvasion

```
git clone https://github.com/cykod/AlienInvasion.git
```

* list out the directory name of the app, it should be ./AlienInvasion
```
ls -al AlienInvasion
```

* Create a Dockerfile with the following content for building a container image from NGINX base

```
FROM nginx
ADD /AlienInvasion /usr/share/nginx/html
```

* build a customized container image with the dockerfile

```
docker build . -t myaliengame
```
* start a container app with the newly built image

```
docker run -d -p 80:80 myaliengame

```
* bring up a chrome/firefox browser from your laptop and access to http://your-vm-public-ip and you should be able to see a game is up and running on your browser

_now the game app is running as a containerized app on your docker host_

> push the newly built game container image to your dockerhub repository

* push the new image to your dockerhub repository, follow the lab we did last week, Lab 4.  
