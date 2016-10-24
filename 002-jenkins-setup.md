# 2. Setting up Jenkins Job

## 2.1 Overview
In this lab, we will use Jenkins to create a build using maven to use it in our HOL-OSS-DEVOPS project.

### 2.1.1 Objectives
This lab aims to get you familiar with Jenkins on Azure and OpenShift Clouds.

### 2.1.2 Requerimients
You must have the Azure account or an OpenShift account mentioned in Lab 01.

## 2.2 Setting up the Jenkins Machine
### 2.2.1 Using Azure

1. Browse to Azure Portal
You can use all the Jenkins templates showed below; for this lab we will use Jenkis template published by Docker.
![](./images/2.2.i001.png)

2. Create a Jenkins Machine
![](./images/2.2.i002.png)

3. Fill all the requerimients
![](./images/2.2.i003.png)

4. Select the machine size
![](./images/2.2.i004.png) 

![](./images/2.2.i005.png)

5. Validate the configuration selected
![](./images/2.2.i006.png)

6. Deploy the machine
![](./images/2.2.i008.png)

7. Login in your Jenkins server with the defult credentials.

When you login for the first time to jenkins it will ask for unlock
![](./images/2.2.i009.png)

To unlock Jenkins you should connect directly to the vm and look in the "initialAdminPassword" file. We will use Putty to look in this file as is showing below.
![](./images/2.2.i010.png)
![](./images/2.2.i011.png)
![](./images/2.2.i012.png)
![](./images/2.2.i013.png)
![](./images/2.2.i014.png)

Once that we find the file. Please notice the path.
![](./images/2.2.i015.png)

Now we can fill the Administratior password and continue to the next step.
![](./images/2.2.i016.png)

8. Create a new Jenkins user 
![](./images/2.2.i019.png)
![](./images/2.2.i020.png)

9. Customize Jenkins selecting "Install suggested plugins"
![](./images/2.2.i017.png)
![](./images/2.2.i018.png)

10. Install maven plugins
![](./images/2.2.i022.png)
![](./images/2.2.i023.png)


11. Create a new Item and select an FreeStyle Project
![](./images/2.2.i024.png)
![](./images/2.2.i025.png)

12. Fill all the form and save it
![](./images/2.2.i026.png)
![](./images/2.2.i027.png)
![](./images/2.2.i028.png)
![](./images/2.2.i029.png)
![](./images/2.2.i030.png)
![](./images/2.2.i031.png)

13. Maven Configuration

Go to the main page and select Manage Jenkins as is showing below.

![](./images/2.2.i031.png)

Select Global Tool Configuration and create a Maven installation.

![](./images/2.2.i032.png)

![](./images/2.2.i033.png)

![](./images/2.2.i034.png)

After the maven installation you should configure the Maven Option Variables.
Go to Configure System and Select Maven Project Configuration.

![](./images/2.2.i035.png)

![](./images/2.2.i036.png)

