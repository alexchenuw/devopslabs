## Lab 3. Create multiple NGINX web server containers
____

This lab is to create two NGINX web server containers and map both web servers to different ports on the Docker host.
> Part one: create containers

* create the first container
```bash
docker run --name firstcontainer -d -p 8688:80 nginx
```
* create the second container 
```bash
docker run --name secondcontainer -d -p 8699:80 nginx
```
* test web server homepage on both servers
```bash
curl http://docker-host-ip:8688/
curl http://docker-host-ip:8699/
```
_you will need also update your VM's firewall rules to allow tcp 8080 to you vm_ 

* create the first index1.html file with the content: This is container one web server.
```bash
echo "This is container one web server" >index1.html
```
* create the second index2.html file with the content: This is container two web server.
```bash
echo "This is container two web server" >index2.html
```
* use docker cp to copy the index1.html file into the first container: 
```bash
docker cp index1.html firstcontainer:/usr/share/nginx/html/index.html
```
* use docker cp to copy the index2.html file into the second container:
```bash
docker cp index2.html secondcontainer:/usr/share/nginx/html/index.html
```
* check the web server home pages on the first container and second container
```bash
curl ifconfig.io
export MYIP=`curl ifconfig.io`
curl http://${MYIP}:8688/
curl http://${MYIP}:8699/
```
> Part two: run these Docker commands to examine your docker container details.  Notice how using $(docker ps -q -a) we are able to proivde the docker image id in one line.

```bash
docker ps -a
docker image ls
docker ps -a -q
docker inspect container_id
docker inspect $(docker ps -a -q)
docker exec -it container_id bash
```
