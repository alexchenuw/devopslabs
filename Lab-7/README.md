## Lab 7. Run a multi-containers application with Docker-compose
___

> Install Docker-compose into your VM
* install docker-compose
```shell
sudo apt-get update -y
sudo apt-get install docker-compose -y
```
* check if it is installed properly
```shell
docker-compose version
```
you should see the version info

> run a multi-container application with docker-compose 

* create a docker-compose.yaml file
```
version: '3'
services:
  web:
    build: .
    ports:
      - ”8080:80"
  redis:
    image: "redis:alpine”

```
* now run the app with command
```
docker-compose up
```
_you should still have the game app running, but it is on port 8080 now_

_this is just a simulation on redis, you will need code change to actually use redis to record the game scores_
