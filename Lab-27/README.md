## Lab 27. Prep lab for lab 28
___
> This lab include 4 mini labs and they are the build blocks for lab 28, everyone should be able to finish these 4 mini labs as these are labs we did earlier.

* lab 27-1: Create a Dockfile to build a nginx image with a customized index.html
start with a new folder on your VM
```
mkdir lab_27 && cd lab_27
```
create an index.html file with the following content
```html
<center><h1>This is version 1.0.0</center>
```
create a Dockerfile with the content
```yaml
FROM nginx
COPY index.html /usr/share/nginx/html
```
