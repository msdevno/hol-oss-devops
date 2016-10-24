# 4. Setting up Docker in Linux

## 4.1 Overview
In this lab we will configure a Docker machine to use it in our HOL-DEVOPS project.

### 4.1.1 Requerimients
You must to have the Azure account mentioned in Lab 01.

## 4.2 Setting up the Linux Machine in Azure

1. Browse to Azure Portal

2. Create a new Linux Machine and fill all the requeriments
![](./images/4.2.i001.PNG)

3. Select the machine size
![](./images/4.2.i002.png)

3. Fill all the settings
![](./images/4.2.i003.png)

4. Validate the configuration selected
![](./images/4.2.i004.png)

6. Deploy the machine
![](./images/4.2.i005.png)

## 4.2 Setting up Docker

1. Connect to the machine using Putty
![](./images/4.2.i006.png)

![](./images/4.2.i007.png)

![](./images/4.2.i008.png)

2. Create the ssh keys
![](./images/4.2.i009a.png)
![](./images/4.2.i009b.png)
![](./images/4.2.i009c.png)
![](./images/4.2.i009d.png)
![](./images/4.2.i009e.png)

Make sure to use your own IPs
![](./images/4.2.i009f.png)
![](./images/4.2.i009g.png)
![](./images/4.2.i009h.png)
![](./images/4.2.i009i.png)
![](./images/4.2.i009j.png)
![](./images/4.2.i009k.png)
![](./images/4.2.i009k.png)
![](./images/4.2.i009l.png)
![](./images/4.2.i009m.png)

3. Browse to Azure portal and open the Docker machine created in step 4.2 in this Lab.

4. Go to Extensions -> Add -> Select Docker extension
![](./images/4.2.i011.png)

5. Select create 
![](./images/4.2.i012.png)

6. Load all the keys and select OK
![](./images/4.2.i013.png)

7. When the deployment of the Docker extension finish you will see the new Extension as is showing below
![](./images/4.2.i014.png)

## 4.3 Setting up Docker communication endpoint

1. Browse to Azure portal and open the Docker machine created in step 4.2 in this Lab.
2. Go to Network interfaces -> Network security group -> Inbound security rules -> Add
Fill all the fields

![](./images/4.2.i015.png)

3. When the rule has been deployed you will see it as is showing below
![](./images/4.2.i016.png)

