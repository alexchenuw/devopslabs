## Lab 3. Create multiple NGINX web server containers
____

This lab is to create two NGINX web server containers and map both web servers to different ports on the Docker host.
> Part one: create containers

* create the first container
```bash
sudo docker run --name firstcontainer -d -p 5688:80 nginx
```
* create the second container 
```bash
sudo docker run --name secondcontainer -d -p 5699:80 nginx
```
* test web server homepage on both servers
```bash
curl http://docker-host-ip:5688/
curl http://docker-host-ip:5699/
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
sudo docker cp index1.html firstcontainer:/usr/share/nginx/html/index.html
```
* use docker cp to copy the index2.html file into the second container:
```bash
sudo docker cp index2.html secondcontainer:/usr/share/nginx/html/index.html
```
* check the web server home pages on the first container and second container
```bash
curl http://docker-host-ip:5688/
curl http://docker-host-ip:5699/
```
> Part two: run the rest Docker commandsas practice
```bash
sudo docker ps -a
sudo docker image ls
sudo docker inspect container_id
sudo docker exec -it container_id bash
```
