## Lab 1. Deploying a VM instance into Google Cloud
____

This lab is to deploy a Ubuntu 16.04 LTS instance at Google Cloud and set up the SSH key access to it.

>Part 1: Grab the ssh public key from your local computer/laptop

* generate a ssh key pair on your local computer/laptop by running "sshkey-gen" under Windows Powershell or MacOS terminal
  
  ```
  #ssh-keygen -C "Your NetID"
  ```



* keep all default settings and find where the generated file (.ssh/id_rsa.pub). and copy the text content of the file.


> Part 2: Deploy a Ubuntu 18.04 LTS instance at Google Cloud.


* Log in with your UW email at https://console.cloud.google.com

* At the cloud console, top left, click navigation menu, compute engine -> VM instances, and Create instance"

  ![Create a VM](https://github.com/alexchenuw/devopslabs/blob/main/Lab-1/lab1-1.png)

* Specify the instance name as instance-1-yourNETID, change the boot Disk as Ubuntu 18.04 and the disk size to 30G
  ![instance name and disk and key](https://github.com/alexchenuw/devopslabs/blob/main/Lab-1/lab1-2.png)
  
  ![disk to ubuntu](https://github.com/alexchenuw/devopslabs/blob/main/Lab-1/lab1-3.png)
  ![key](https://github.com/alexchenuw/devopslabs/blob/main/Lab-1/lab1-4.png)

* At the main tab, under **Security** and **SSH Keys**, paste your ssh public key from part one to the box
![add ssh key](https://github.com/alexchenuw/devopslabs/blob/main/Lab-1/ssh-gcp-key.png)

* then create the instance, you should find the instance is being created and running shortly.

> finally, find the externalIP of your instance at Google cloud console

* log in to the instance from your laptop

```
  ssh your-netid@the-ip-of-your-instance
```
* you should be able to get into the VM without a password
