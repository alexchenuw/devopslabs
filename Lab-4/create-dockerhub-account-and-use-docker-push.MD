## Lab 4. Create a docker hub repository and push docker images to it
___
This lab includes two parts, part one is to create a dockerhub account and repository and part two is to push a customized docker image to the newly created docker repository.

> Part one: create a dockerhub account and repository
* sign up an account at https://hub.docker.com

![Docker Hub](https://github.com/alexchenuw/devopslabs/blob/main/Lab-4/lab4-1.png)

* create a public repository

![Docker Repository](https://github.com/alexchenuw/devopslabs/blob/main/Lab-4/lab4-2.png)

> Part two: build and push a customized image to dockerhub repository

* use docker commit command to build a customized docker image

* tag the image with required username/repository format "docker tag image-id username/repository:tag"

* docker login with registered credentials "docker login"

* publish the customized image with "docker push" command "docker push username/repository:tag"

* check if the image shows up on your dockerhub registory
