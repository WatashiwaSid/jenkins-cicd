# Jenkins Pipeline Project
An end-to-end pipeline for spring boot application.

![image](https://github.com/WatashiwaSid/jenkins-cicd/blob/2958b0a79b18d014da5f8a517c2efbd0d9999c97/jenkins.drawio.png)

## Introduction 
This is a basic Java application built with Spring Boot and managed using Maven. The project's dependencies are defined in the pom.xml file located in the root directory.
The application follows the MVC (Model-View-Controller) architecture, where controller returns a page with title and message attributes to the view.

## Local Setup
- Clone this repository
```
git clone https://github.com/WatashiwaSid/jenkins-cicd
cd jenkins-cicd
```

- Install Java and Maven
```
sudo apt update
sudo apt install openjdk-17-jre
sudo apt install maven
```

- Execute maven targets to generate the artifact
```
mvn clean package
```

# Build Pipeline 
Follow the steps to build a Jenkins pipeline for this project. 

## 1. Setup Apache Tomcat
```
cd /opt
sudo wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.65/bin/apache-tomcat-9.0.65.tar.gz
sudo tar -xvf apache-tomcat-9.0.65.tar.gz

sudo nano /opt/apache-tomcat-9.0.65/conf/tomcat-users.xml
#---add-below-line at the end (2nd-last line)----#
<user username="username" password="password" roles="admin-gui, manager-gui"/>

sudo nano /opt/apache-tomcat-9.0.65/webapps/manager/META-INF/context.xml
#---comment-following-line-like-this----#
<!-- Valve className="org.apache.catalina.valves.RemoteAddrValve"allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1"/> -->

sudo nano /opt/apache-tomcat-9.0.65/webapps/host-manager/META-INF/context.xml
#---comment-following-line-like-this----#
<!-- Valve className="org.apache.catalina.valves.RemoteAddrValve"allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1"/> -->

sudo stopTomcat
sudo startTomcat
```

## 2. Setup Pipeline
- Create a new pipeline project in Jenkins.
- Add your Sonarcube token in Jenkins Global Credentials.
- Copy the pipeline configuration from Jenkinsfile in this repository.
- Build Your Pipeline.

## Screenshots

### Pipeline Script
![script](https://github.com/WatashiwaSid/jenkins-cicd/blob/70796f152ff867934dfa6789b187ffa2de8db24d/uploads/script.png)

### Pipeline Status
![pipeline](https://github.com/WatashiwaSid/jenkins-cicd/blob/6c39dd6833bf08543fa2afca12e3f20f40b2c150/uploads/pipeline.png)

### Sonarcube Analysis Report
![sonarcube](https://github.com/WatashiwaSid/jenkins-cicd/blob/6c39dd6833bf08543fa2afca12e3f20f40b2c150/uploads/sonar.png)

### Apache Tomcat Server
![tomcat](https://github.com/WatashiwaSid/jenkins-cicd/blob/6c39dd6833bf08543fa2afca12e3f20f40b2c150/uploads/tomcat.png)

### Artificat Deployment
![deployment](https://github.com/WatashiwaSid/jenkins-cicd/blob/6c39dd6833bf08543fa2afca12e3f20f40b2c150/uploads/petclinic.png)


