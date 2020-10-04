1, login to your VM through SSH

2, update the apt-get install package list: sudo apt-get update -y

3, install docker engine: sudo apt-get install docker.io

4, add yourself to the docker group "sudo usermod -aG docker your-user-name"

5, log out to the box and log back in.

6, run command "docker version", it should show the docker version if docker has been successfully installed
