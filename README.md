# How to set up Jenkins on an Ubuntu EC2 instance

## Description
This guide walks you through the process of setting up Jenkins on an Ubuntu EC2 instance, including the installation of Java, Maven, and Jenkins itself. By following these steps, you'll be able to set up a Jenkins server that can automate builds and deployments for your projects. This setup is ideal for continuous integration (CI) and continuous delivery (CD) pipelines.

## Why do we need these tools?

1. **Java**: Jenkins is a Java-based application. Therefore, it needs Java to run. We need to install Java before we install Jenkins.
2. **Maven**: Maven is a build automation tool commonly used with Java projects. It helps manage project dependencies, build, and deploy applications. Jenkins integrates well with Maven to automate building Java projects.
3. **Jenkins**: Jenkins is the core tool that will allow us to automate various tasks in the software development lifecycle, such as building, testing, and deploying code.

Now let's walk through the setup process step by step.

## 1. Create EC2 Ubuntu - Jenkins VM
- First, you will need an EC2 instance running Ubuntu. If you don’t have one, you can create a new EC2 instance on AWS using the Ubuntu image.

## 2. Connect to Jenkins VM via SSH
Once your EC2 instance is set up, you need to connect to it via SSH (Secure Shell). SSH allows you to securely access your server from a local machine.

**OPEN Git Bash or terminal:**
- Use the following command to connect to your EC2 instance: ssh -i "keypair" ubuntu@publicdns

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

### 6.2 Install Jenkins on Ubuntu 
- Now, install Jenkins:
  - sudo apt install jenkins -y
- Start Jenkins:
  - sudo systemctl start jenkins
- Enable Jenkins to start on boot:
  - sudo systemctl enable jenkins
- Check the Jenkins status:
  - sudo systemctl status jenkins  | "Ctrl + Z" to exit the status screen

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
