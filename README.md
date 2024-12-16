# How to set up Jenkins on an Ubuntu EC2 instance

## Description
This guide walks you through the process of setting up Jenkins on an Ubuntu EC2 instance, including the installation of Java, Maven, and Jenkins itself. By following these steps, you'll be able to set up a Jenkins server that can automate builds and deployments for your projects. This setup is ideal for continuous integration (CI) and continuous delivery (CD) pipelines.

## 1. Create EC2 Ubuntu - Jenkins VM

## 2. Connect to Jenkins VM via SSH
OPEN Git Bash
- ssh -i "keypair" ubuntu@publicdns

## 3. Update the Server
- sudo apt update

## 4. Install Java on the Server
- sudo apt-get install default-jdk -y
- java -version

## 5. Install Maven
- sudo apt install maven -y
- mvn --version

## 6. Install Jenkins

### 6.1 Add Jenkins GPG Key and Repository
- Next, add the Jenkins GPG key with the following command:
  - sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
- Then, add the Jenkins repository because it is not added by default in the Ubuntu 24.04 sources list:
  - echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
- Once the key and the repo are added, update the system again:
  - sudo apt update -y

### 6.2 Install Jenkins on Ubuntu 24.04
- Now, install Jenkins:
  - sudo apt install jenkins -y
- Start Jenkins:
  - sudo systemctl start jenkins
- Enable Jenkins to start on boot:
  - sudo systemctl enable jenkins
- Check the Jenkins status:
  - sudo systemctl status jenkins  # "Ctrl + Z" to exit the status screen

## 7. Access Jenkins Web Interface
- Go to your server's public DNS:
  - http://PublicDNS:8080
- Make sure port 8080 is open in the Security Group (SG) settings.
- Retrieve the Jenkins initial admin password by running:
  - sudo cat /var/lib/jenkins/secrets/initialAdminPassword
- Follow the on-screen instructions to install the suggested plugins.

## 8. Exit the Server
Once Jenkins is set up, type `exit` to exit the EC2 server:
- exit
