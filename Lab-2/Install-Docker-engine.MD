login to your VM through SSH
update the apt-get install package list: sudo apt-get update -y
install docker engine: sudo apt-get install docker.io
add yourself to the docker group "sudo usermod -aG docker your-user-name"
log out to the box and log back in.
run command "docker version", it should show the docker version if docker has been successfully installed
