## Lab 4. Create a docker hub repository and push docker images to it
___
This lab includes two parts, part one is to create a dockerhub account and repository and part two is to push a customized docker image to the newly created docker repository.

> Part one: create a dockerhub account and repository
* sign up an account at https://hub.docker.com

![Docker Hub](https://github.com/alexchenuw/devopslabs/blob/main/Lab-4/lab4-1.png)

* create a public repository

![Docker Repository](https://github.com/alexchenuw/devopslabs/blob/main/Lab-4/lab4-2.png)

> Part two: build and push a customized image to dockerhub repository

* Now we are going to create a simple nginx based image using the following **Dockerfile**.  Login to your linux host and create a folder called lab4, in this folder we will create the Dockerfile file.

```shell
FROM nginx:latest
COPY ./index.html /usr/share/nginx/html/index.html
```

* next we are going to create a simple html file for our image, build the image and tag the image.  Then we will create an instance of our image and call it **web1**. Finally we will get a quick look at the logs for our new docker container instance.

```bash
echo "This is my sample nginx web container" > index.html
docker build . -t static-site
docker images | grep static-site
docker run -d -p 8080:80 --name web1 static-site
curl localhost:8080
docker tag static-site:latest static-site:v0.0.1
docker images | grep static-site
docker inspect web1
docker container logs web1
```

![Docker Hub](https://github.com/alexchenuw/devopslabs/blob/main/Lab-4/docker-tag.png)

* Next we are going to tag our custom image with with our docker repository userid and version details. In this example replace **D_USER** with your Docker UserID and **D_REPO** with your Docker Repository name.  Notice the Docker image ID values do you see any difference in the values provided between latest, v0.0.1 and your Docker hub tagged image?

```bash
docker tag static-site:v0.0.1 D_USER/D_REPO:v0.0.1
docker images
```

* Finally we want to push our new image to the dockerhub.  To do this we will need to login and then push the image.

```bash
docker login
docker push username/repository:tag
```

* check if the image shows up on your dockerhub registory
