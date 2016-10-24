# 3. Setting up an automated build in Visual Studio Team Services
## 3.1. Overview
In this lab, we will retrieve our sample Java application from GitHub and trigger a Jenkins build from Visual Studio Team Services (VSTS). Jenkins will build our application using Maven and package it, before VSTS retrieves the package and stores it as an artifact.

### 3.1.1 Objectives
This lab aims to get you familiar with how Visual Studio Team Services can retrieve code from a GitHub repository and you can integrate with Jenkins to build and package an application. 

### 3.1.2 Requirements
You must have completed Lab 01 and Lab 02.

## 3.2. Building an application using VSTS
In this session, we will create a GitHub service endpoint that enables us to retrieve the code in a GitHub repository. We will also create a Jenkins service endpoint to enable a connection to Jenkins. Our intention is for Jenkins to build and package the application, VSTS simply queues the Jenkins build and retrieves the package when Jenkins is finished packaging it.

### 3.2.1 Creating a VSTS project

    

