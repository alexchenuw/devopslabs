## Install and Config a Jenkins server 
___


sudo docker network create --driver=bridge --subnet=10.235.1.0/24 br0
sudo docker pull jenkins/jenkins:latest
sudo docker run -itd --network=br0 -p 8080:8080 jenkins/jenkins

cat /var/jenkins_home/secrets/initialAdminPassword
