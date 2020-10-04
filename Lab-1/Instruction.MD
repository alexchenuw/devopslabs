This lab is to deploy a Ubuntu 16.04 LTS instance at Google Cloud and set up the SSH key access to it.

Part 1: Deploy a Ubuntu 16.04 LTS instance at Google Cloud.

1, log in with your UW email at https://cloud.google.com

2, at the cloud console, top left, click navigation menu, compute engine -> VM instances, and Create instance"

3, specify the instance name as instance-1-yourNETID, change the boot Disk as Ubuntu 16.04 and the disk size to 100G

4, check "allow http traffic" and "allow https traffic" then "create"

5, you should find the instance is being created and running shortly.


Part 2: set up ssh key authentication for yourself to the instance

1, generate a ssh key pair on your local computer/laptop by running "sshkey-gen" under Windows Powershell or MacOS terminal

2, keep all default settings and find where the generated file (.ssh/id_rsa.pub). and copy the text content of the file.

3, go back to Google Cloud console, find your instance, choose the SSH dropdown "view gcloud command" option then run it

4, choose "run in cloud cli", unaswer yes and authorize cloud shell requests until the user and .ssh/id_rsa.pub file is created at the instance and the prompt should be something like: xxxx@instance-1-xxxx:~$

5, get into .ssh directory under your home direcory, edit authorized_keys file, in a new line, paste the key context you copied from step 2 above, save and exit

6, on your local computer/laptop, run "ssh your-netid@the-ip-of-your-instance", you should be able to get into the VM without a password
