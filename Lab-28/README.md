## Lab 28.  In-Class Lab: Building a simple CI and CD pipeline with Jenkins
___

_This is an inclass lab where students will be following the instructor step by step to set up._
_This lab guide only covers the major steps/screencaptures for the lab, please do follow with instructor on the detail instruction_

## * At github respository:

> 1. Setup a github webhook for your github repository that hosts the code you have for creating the new app

![webhook](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab28_1.png)

once it is added correctly, you should see a green check mark

![cd-1](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab28_2.png)

## * now logon to Jenkins: http://34.121.19.249:8080/

> 2. once logged in, create a freestyle job and name it with your netID, for example, achen-CI

![cd-2](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab28_3.png)


> 3. Specify your git repository, the example shows instructor's github repo but you need specify yours

![cd-2](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab28_4.png)


> 4. Specify trigger as github webhook

![cd-3](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab28_5.png)

> 5. Choose Build via shell command and put in docker commands and dockerhub login info to your repository

![cd-35](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab28_6.png)


> 6. ** Now try to build now to verify Jenkins can build the image and publish it to dockerhub for you


![cd-4](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab28_7.png)

if everything is successfull, you should find the image has been published at your dockerhub repository, go and verify
This finishes the continunous Integration lab

> 7. ** now make change to your app file (index.html to indicate it is now version 1.0.1), and commit the change then push to github.

you should be able to see Jenkins project will automatically get notified on the update and it will build a new image for you and push the image to dockerhub.


## * now continue on Continuous Delivery lab

> 8. choose to configure the project and at the after build actions

![cd-start](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab28_cd_1.png)

> 8. Setup the SSH plugin to login to kubernetes kubectl to rollout the deplpoyment with the new image

![cd-ssh](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab28_cd_2.png)
![cd-ssh](https://github.com/alexchenuw/devopslabs/blob/main/Lab-28/lab28_cd_3.png)

