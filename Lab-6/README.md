## Lab 6. Build your customized NGINX image with Dockerfile
___

This lab is to build a customized NGINX image that has a defined index.html file
* Create an index.html at current folder
```bash
echo " This is a customized web page by XXX" > index.html
```
* Create a Dockerfile that copies the index.html to the container image to replace the default one
```bash
FROM nginx
COPY index.html /usr/share/nginx/html/index.html
```
* Build a docker image from the Dockerfile
```bash
docker build . -t mynginx
```
* Start a container from the newly built image
```bash
docker run -d -p 32321:80 mynginx
```
* check the container web page, you should get the customized text
```bash
curl http://host_ip:32321
```
