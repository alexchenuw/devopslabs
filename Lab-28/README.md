## Lab 28. Building a simple CI and CD pipeline with Jenkins
___

Follow along lab

## * At github respository:

> 1. Setup a github webhook for your github repository

![webhook](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab28-1-webook.png)

## * now logon to Jenkins:

> 2. once logged in, create a freestyle job and name it with your netID, for example, achen-CI

![cd-1](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab28-ci-1.png)


> 3. Specify your git repository, the example shows instructor's github repo but you need specify yours

![cd-2](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab-28-ci-2.png)


> 4. Specify trigger as github webhook

![cd-3](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab-28-ci-3.png)

> 5. Choose Build via shell command

![cd-35](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab-28-ci-35.png)


> 6. Put in docker commands and dockerhub login info to your repository

![cd-4](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab-28-ci-4.png)



** Now try to build now to verify Jenkins can build the image and publish it to dockerhub for you

![ci-build](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab-28-ci-build.png)

you can also check the console log for details/troubleshooting

![ci-console](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab-28-ci-console.png)

if everything is successfull, you should find the image has been published at your dockerhub repository, go and verify
This finishes the continunous Integration lab


## * now continue on Continuous Delivery lab

> 7. choose to configure the project and at the after build actions

![cd-ssh](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab-28-cd-shell.png)

> 8. Setup the SSH plugin to login to kubernetes kubectl to rollout the deplpoyment with the new image

![cd-ssh](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab-28-cd-ssh.png)
