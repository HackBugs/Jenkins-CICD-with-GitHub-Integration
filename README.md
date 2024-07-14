# Jenkins-CICD-with-GitHub-Integration

Author : HackBugs - Shahnwaj Aalam
App name : node-todo-cicd

## - First requrement 
-------------------------
- Github code of doveloper
- AWS EC2 create instance / give name of instance and select OC which you want to like Ubuntu and also create Key-pair-name 
if you using linux than select .pem and for windows .ppk and select security group
-Docker 
- Jenkins CI / CD

## - Install jenkins on AWS
Step - 1 Install Java
Update your system
  sudo apt update
Install java
  sudo apt install openjdk-11-jre
Validate Installation
 java -version
It should look something like this
  openjdk version "11.0.12" 2021-07-20 OpenJDK Runtime Environment (build 11.0.12+7-post-Debian-2) OpenJDK 64-Bit Server VM (build 11.0.12+7-post-Debian-2, mixed mode, sharing)
Step - 2 Install Jenkins
Just copy these commands and paste them onto your terminal.
  curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \   /usr/share/keyrings/jenkins-keyring.asc > /dev/null 
  echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \   https://pkg.jenkins.io/debian binary/ | sudo tee \   /etc/apt/sources.list.d/jenkins.list > /dev/null
  sudo apt-get update 
  sudo apt-get install jenkins
Step -3 Start jenkins
  sudo systemctl enable jenkins
  sudo systemctl start jenkins
  sudo systemctl status jenkins
 Step - 4 Open port 8080 from AWS Console:

 ### instnce security > Security gorup > give the access of "custom TCP" prot of 8080
 ### Now with this prot you open your jenkins homepage on you brouser tab - and copy the password path and on AWS instace CLI - Paste like cd path 
 and read path cat path now copy password paste browser tab jenkins box and enter now choose "install suggested plugins"
 ### Now on jenkins "create first admin user" and choose which requremnt details done! now jenkins ready to use

 ### Create on jenins "New item name" write discription and give project URL and for password generate/create from AWS instance cli - cmd =  ssh-keygen (private key/public key)
 go github setting > SSH Keys - and now add here "public key" in jenkins select github and paste "private key"
 ### on jenkins click "Build now" now git code deply on AWS Ubuntu instance copy path and check after build

 user sudo apt and pkg name whatever you want to install
 Now install node Js
 sudo apt install nodejs
 sudo apt install npm

 ### Now install Docker to make container
 ### if you want to remove existing docker file use this cmd - sudo rm dockerfile

 install docker AWS instance cmd - sudo apt install docker.io
 go on path where you want to make "dockerfile" cmd - sudo vi dockerfile
 ### use this script
 
 FROM node:12.2.0-alpine
 WORKDIR app
 COPY . .
 RUN npm install
 EXPOSE 8000
 CMD ["node","app.js"]

 ## after create docker file now turn to "build" make a "image" and make docker container 
 ## cmd - sudo usermod -a -G docker $USER
 ## cmd - sudo reboot
 ## cmd - docker build . -t container 

 ### after Build container use cmd - docke run -d --name container-name -p 8000:8000 container-name
 Now run application by docker on webpage with ip address and port no

 ## Automate pipeline
 Jenkins build steps > Excute shell, Paste in shell box your shell excutable code

 docker build . -t node-app-todo
 sudo usermod -a -G docker $USER
 docker run -d --name node-todo-container -p 8000:8000 todo-node-app
 
 ### Before click on Build now run this cmd on AWS instance cli -  sudo systemctl restart jenkins now click on build now
 ### before use web-hooks do some setting on github repo setting > webhooks > payload URL > paste jenkins ip addres and port which you using to access
 when you add any new URL for access make sure you in EC2 instance > securities add access port number 
 ### jenkins-plugin-name = github intigration, we known as also web-hooks plugin use in between "github and jenkins" for when developer change any code on github than on jenkins 
 ############################################ Done ################################################
 
--------------------------------------------------------------------------------------------------------------
Create AWS EC2 instance / Now cleck on connect to get CLI of AWS instance
sudo apt update
    3  sudo apt install openjdk-11-jre
    4  java -version
    5  curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \   /usr/share/keyrings/jenkins-keyring.asc > /dev/null 
    6  echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \   https://pkg.jenkins.io/debian binary/ | sudo tee \   /etc/apt/sources.list.d/jenkins.list > /dev/null
    7  sudo apt-get update 
    8  sudo apt-get install jenkins
    9  sudo systemctl enable jenkins
   10  sudo systemctl start jenkins
   11  sudo systemctl status jenkins
   12  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   13  history

Got to jenkins job
Execute shell 
docker build . -t node-app-todo
docker run -d --name node-app-container -p 8000:8000 node-app-todo
--------------------------------------------------------------------------------------------------


