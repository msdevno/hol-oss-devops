# hol-oss-devops
This set of hands on labs is created to give you an introduction to open source DevOps using Visual Studio Team Services and the open source cloud services in Azure. We appreciate your feedback and support in continuing to develop this content.

This lab showcases the following technologies: Microsoft Azure, Visual Studio Team Services, Java, Maven, Jenkins, Linux, Docker, TomCat. 


### **Suggested timeline for Open Source DevOps Hands On Lab (HOL)**

| Time (min) | Activity |
| ---        | ---      |
| 30         | Introduction to open source DevOps |
| 30         | Lab1 - [Before you begin this lab](./001-lab-setup.md) |
| 60         | Lab2 - [Creating and configuring a Jenkins server in Azure](./002-jenkins-setup.md) |
| 30         | Lab3 - [Setting up an automated build in Visual Studio Team Services](./003-vsts-build.md) |
| 30         | Lab4 - [Configuring Docker](./004-docker-setup.md) |
| 30         | Lab5 - [Release management in Visual Studio Team Services](./005-vsts-release.md) |

### **Detailed contents of the HOL**

 - [Introduction to open source DevOps](./000-oss-devops-introduction.md)
    
1. [Before you begin this lab](./001-lab-setup.md)  

2. [Creating and configuring a Jenkins server in Azure](./002-jenkins-setup.md)  
    * Overview
        * Objectives
        * Requirements
    * Creating a VM in Azure running Jenkins
    * Unlock Jenkins
    * Configuring a Maven build in Jenkins
        * Install maven plugins
        * Maven Configuration
        * Create a Maven build

3. [Setting up an automated build in Visual Studio Team Services](./003-vsts-build.md)  
    * Overview
        * Objectives
        * Requirements
    * Setting up VSTS
        * Creating a VSTS project
        * Connecting VSTS to GitHub
        * Connecting VSTS to Jenkins
    * Sample Java application on GitHub
        * Fork GitHub repository
    * Building the application using VSTS
        * Creating a build definition
        * Queue your first build

4. [Configuring Docker](./004-docker-setup.md)
    * Overview
        * Objectives
        * Requirements

5. [Release management in Visual Studio Team Services](./005-vsts-release.md)
    * Overview
        * Objectives
        * Requirements
    * Installing the VSTS Docker extension
    * Connecting VSTS to Docker Hub and a Docker Host
    * Creating a Release Definition in VSTS
    * Configure release tasks
    * Create your first release
