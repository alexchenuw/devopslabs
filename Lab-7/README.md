## Lab 7. Run a multi-containers application with Docker-compose
___

> Install Docker-compose into your VM

* install docker-compose

```shell
sudo apt-get update -y
sudo apt-get install docker-compose -y
```

* confirm that docker compose is installed, you should see details about the version installed.

```shell
docker-compose -version
```

>run a multi-container application with docker-compose 

Complete this work in the folder "lab-6" as the docker-compose.yaml file assumes there is a Dockerfile in the same directory.

* create a docker-compose.yaml file
```
version: '2'
services:
  web:
    build: .
    ports:
      - "8080:80"
  redis:
    image: "redis:alpine"
```
* now run the app with command
```
docker-compose up
```
> Note: you should still have the game app running, but it is running now on port 8080 in addtion to port 80.

> Note: this is just a simulation on redis, you will need code change to actually use redis to record the game scores_
