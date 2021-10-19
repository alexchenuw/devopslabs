## Lab 4. Create a docker hub repository and push docker images to it
___
This lab includes two parts, part one is to create a dockerhub account and repository and part two is to push a customized docker image to the newly created docker repository.

> Part one: create a dockerhub account and repository
* sign up an account at https://hub.docker.com

![Docker Hub](https://github.com/alexchenuw/devopslabs/blob/main/Lab-4/lab4-1.png)

* create a public repository

![Docker Repository](https://github.com/alexchenuw/devopslabs/blob/main/Lab-4/lab4-2.png)

> Part two: build and push a customized image to dockerhub repository

* next we are going to create a nginx container, then customize it with a simple html file, build out a docker image and tag it.  Then we will create an instance of our image. Finally we will push the image to dockerhub so that it can be shared to others.

```bash
docker run -d -p 8989:80 nginx
curl http://localhost:8989
```
** start customization
```bash
echo "This is my sample nginx web container" > index.html
docker cp index.html containerid:/usr/share/nginx/html/index.html
curl http://localhost:8989
docker commit containerid
```
** try to create a new container using the image
```bash
docker run -d -p 9000:80 dockerimageid
curl http://localhost:9000
```

* Next we are going to tag our custom image with with our docker repository userid and version details. In this example replace **D_USER** with your Docker UserID and **D_REPO** with your Docker Repository name.  Notice the Docker image ID values do you see any difference in the values provided between latest, v0.0.1 and your Docker hub tagged image?

```bash
docker tag dockerimageid username/reproname:v0.1
docker image ls
```

* Finally we want to push our new image to the dockerhub.  To do this we will need to login and then push the image.

```bash
docker login
docker push username/reproname:v0.1
```

* check if the image shows up on your dockerhub registory
