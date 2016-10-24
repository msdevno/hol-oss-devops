# 5. Release management in Visual Studio Team Services
## 5.1. Overview
In this lab, we will configure release management for our sample application. We will create a Docker Registry service endpoint that enables us to pull a TomCat image from Docker Hub and run it to create a container. We will retrieve the artifact created by our automated build in Lab 3, and using the VSTS build agent created in Lab 4, we will run a docker command to deploy the artifact to the TomCat container running on a Linux machine in Azure.

### 5.1.2 Requirements
You must have completed all previous labs.

## 5.2. Connecting VSTS to Docker Hub and a Docker Host

1. Register for a Docker ID by creating an account on Docker Hub as explained [in the Docker documentation](https://docs.docker.com/docker-hub/accounts/).

2. Navigate to "Services" under "Settings"
![](./images/5.2.i001.PNG)

3. Create a new Docker Registry connection by clicking on "+ New Service Endpoint" and selecting "Docker Registry"
![](./images/5.2.i002.PNG)

4. Specify the following information for your connection and click OK:   

    **Connection name**: Docker Hub  
    **Docker registry**: https://index.docker.io/v1/  
    **Docker ID**: The Docker ID you created in step 1  
    **Password**: Your Docker Hub Password  
    **Email**: Optional

    ![](./images/5.2.i003.PNG)

5. You should now see the service endpoint you just created in the overview:
![](./images/5.2.i004.PNG) 

6. Create a new Docker Host connection by clicking on "+ New Service Endpoint" and selecting "Docker Host"
![](./images/5.2.i005.PNG) 

5. Specify the following information for your connection and click OK:   

    **Connection Name**: Docker Host  
    **Server URL**: Specify the server URL of the Docker Machine you created in LABX
    **CA Certificate**: Paste in the CA certificate you saved to disk in LABX
    **Certificate**: Paste in the certificate you saved to disk in LABX
    **Key**: Paste in the key you saved to disk in LABX

    ![](./images/5.2.i006.PNG) 

6. You should now see the service endpoint you just created in the overview:
![](./images/5.2.i007.PNG)  

## 5.3 Creating a Release Definition in VSTS

We will now create a new *Release Definition* that contains all the steps to be executed when we deploy a release. We will enable [*Continous Deployment*](https://en.wikipedia.org/wiki/Continuous_delivery) so that a new release is created every time a build is successful.

1. Go to "Releases" under "Build & Release"
![](./images/5.3.i001.PNG)

2. Create a new release definition by clicking "+ New definition"

3. This time we will not base our release definition on a template, therefore you select "Empty" and click "Next"
![](./images/5.3.i002.PNG)

4. Select "Build" as the artifact source and fill out the fields as specified below and click "Create":  
    
    **Source (Build definition):** Point to the build we created in Lab 03  
    **Continous deployment:** Check  
    **Queue:** Select the queue containing the VSTS agent we installed in Lab 04.

    ![](./images/5.3.i003.PNG) 

5. You should now see a default release definition that is empty. 
![](./images/5.3.i004.PNG)

6. Give your release definition a new name:
![](./images/5.3.i005.PNG)

7. Rename "Environment 1" to "Staging":
![](./images/5.3.i006.PNG)

7. Save your release definition and click "OK".
![](./images/5.3.i007.PNG)

## 5.4 Installing the VSTS Docker extension

1. Browse to the [Docker Integration](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker) extension on the Visual Studio marketplace.
![](./images/5.4.i001.PNG)

2. Install the extension by clicking "Install" and selecting the account you want to install the extension for. 

## 5.5 Configure release steps

We will now configure the release tasks for the Staging environment of our release definition.

1. Go to "Releases" under "Build & Release" and select the release definition you created earlier. 

2. Click "+ Add task"
![](./images/5.5.i001.PNG)

3. Select "All" in the menu to show all the tasks that are available. Find the task called "Docker" and click "Add" twice to add two Docker tasks. 
![](./images/5.5.i002.PNG)

4. When you close the pop-up, your release definition should look like this: 
![](./images/5.5.i003.PNG) 

5. Select the first "Docker" task and edit it to match the following fields:

    **Docker Registry Connection:** Select your Docker Registry endpoint  
    **Action:** Run an image  
    **Image Name:** tomcat:8.0  
    **Container Name:** ossdevops-v$(Release.ReleaseId)-staging  
    **Ports:** 8888:8080  
    **Run in Background:** Checked  
    
    **Advanced options**  
    **Docker Host Connection:** Select your Docker Host endpoint   
    **Working Directory**: $(System.DefaultWorkingDirectory)  
    ![](./images/5.5.i004.PNG)  

    Note that we name our container using a variable: $(Release.ReleaseId). This is a built-in variable that will insert the ID of the release into the name of the container being created in this task.

6. Select the second "Docker" task and edit it to match the following fields:

    **Docker Registry Connection:** Select your Docker Registry endpoint  
    **Action:** Run a Docker command  
    **Command:**   
    
    ```
    cp $(System.DefaultWorkingDirectory)/ArtifactSource/drop/sample-app/target/OSSDevOpsHOL.war ossdevops-v$(Release.ReleaseId)-test:/usr/local/tomcat/webapps/OSSDevOpsHOL.war
    ```  
    
    **Advanced options**  
    **Docker Host Connection:** Select your Docker Host endpoint   
    **Working Directory**: $(System.DefaultWorkingDirectory)  
    ![](./images/5.5.i005.PNG)  

    The command above copies the .war file contained in our artifact to the newly created container running on our Docker Host.

7. If you haven't done so already, save your release definition.

8. In the command in step 6, you can see that the path contains "ArtifactSource". This refers to the source of our artifact, which default is the name of our build. As we want our source to be called "ArtifactSource", we need to specify this. Go to the "Artifacts" tab of your release definition: 
    ![](./images/5.5.i006.PNG)  

9. As you can see there, the "Source alias" is currently "Queue Jenkins Job & Publish", which is a painful name to include in a path. Click the three dots next to the alias and select Edit:
    ![](./images/5.5.i007.PNG)  

10. Rename the value of "Source Alias" to "ArtifactSource" so that it matches we value we specified in our path in step 6. Click "Save".
    ![](./images/5.5.i008.PNG)  

11. Go to the "Trigger" tab of your release definition and update the "Set trigger on artifact source" to point to the artifact source called "ArtifactSource".
    ![](./images/5.5.i009.PNG)

12. Save your release definition again.

## 5.6 Create your first release

1. Create a new release by clicking "+ Release" and selecting "Create Release".
    ![](./images/5.6.i001.PNG) 

2. Select your last successful build and click "Create": 
    ![](./images/5.6.i002.PNG) 

3. A new release has now been created and you can click the link to navigate to the release: 
    ![](./images/5.6.i003.PNG)

4. Click on the "Logs" tab of the release to see the details of your deployment and verify that the release was successful.
    ![](./images/5.6.i004.PNG)