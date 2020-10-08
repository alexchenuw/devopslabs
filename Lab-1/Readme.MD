
## Lab 1. Deploying a VM instance into Google Cloud
____

This lab is to deploy a Ubuntu 16.04 LTS instance at Google Cloud and set up the SSH key access to it.
<!-- Blockquote -->
> Part 1: Deploy a Ubuntu 16.04 LTS instance at Google Cloud.

<!-- UL -->
* Log in with your UW email at https://cloud.google.com

* At the cloud console, top left, click navigation menu, compute engine -> VM instances, and Create instance"
  <!-- images -->
  ![Create a VM](https://github.com/alexchenuw/devopslabs/blob/main/Lab-1/lab1-1.png)

* Specify the instance name as instance-1-yourNETID, change the boot Disk as Ubuntu 16.04 and the disk size to 100G

* check "allow http traffic" and "allow https traffic" then "create"

* you should find the instance is being created and running shortly.
<!--Blockquote -->
>Part 2: set up ssh key authentication for yourself to the instance
<!-- UL -->
* generate a ssh key pair on your local computer/laptop by running "sshkey-gen" under Windows Powershell or MacOS terminal
  <!-- Code Blocks -->
  ```
  #sshkey-gen
  ```

* keep all default settings and find where the generated file (.ssh/id_rsa.pub). and copy the text content of the file.

* go back to Google Cloud console, find your instance, choose the SSH dropdown "view gcloud command" option then run it

* choose "run in cloud cli", unaswer yes and authorize cloud shell requests until the user and .ssh/id_rsa.pub file is created at the instance and the prompt should be something like: 

  ```
  xxxx@instance-1-xxxx:~$
  ```

* get into .ssh directory under your home direcory, edit authorized_keys file, in a new line, paste the key context you copied from step 2 above, save and exit

* on your local computer/laptop, run 
  <!-- Code Blocks -->
  ``` 
  ssh your-netid@the-ip-of-your-instance
  ```
* you should be able to get into the VM without a password
