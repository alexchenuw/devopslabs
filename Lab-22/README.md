## Lab 22. Deploy an application to the k8s cluster
___

> Step 1, deploy the application to your cluster

* Follow the instructions from [Lab 19](https://github.com/alexchenuw/devopslabs/tree/main/Lab-19) to deploy an application to your k8s cluster you just built. Do you remember the [AlienInvasion game](https://github.com/alexchenuw/devopslabs/tree/main/Lab-8) you built and published to your dockerhub repository? that is the image this lab will use as the application

one tip:

```bash
replace the container image with the one you created and uploaded to Dockerhub. an example will be:

image: alexchen2015/alex001:mypersonalnginx

```
> Step 2, scale the application to larger capacity

* follow what you did in Lab 19 to scale the application, expose it as an external facing app and play the game from your browser on your laptop.

