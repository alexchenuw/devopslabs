## Lab 5. Build a customized NGINX Docker image with Dockerfile
___
This lab is to create a customized docker image with a self-defined Dockerfile, the customization needs to have a webpage to have the student name

* create a local file index.html with the student's name in the content
```bash
echo "This is XXX's web server" > index.html
```
* create a Dockerfile that builds a image from NGINX base image and have the index.html replaced with the one just created.
```
FROM NGINX
COPY index.html /var/www/index.html
```
* build the customized image with docker build command
```bash
docker build . -t XXXnginx
```
* create a container with the created image and check if the default webpage includes the student's info
```bash
docker run -d -p 6788:80 XXXnginx
```
```bash
curl http://docker-host-ip:6788/
```
