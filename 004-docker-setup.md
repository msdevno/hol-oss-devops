# 4. Setting up Docker in Linux

## 4.1 Overview
In this lab we will configure a Docker machine to use it in our HOL-DEVOPS project.

### 4.1.1 Requerimients
You must to have the Azure account mentioned in Lab 01.

## 4.2 Setting up the Linux Machine in Azure

1. Browse to Azure Portal. For this lab we will use an Ubuntu template.

2. Create a new Linux Machine and specify all the details
![](./images/4.2.i001.png)

3. Select the machine size
![](./images/4.2.i002.png)

3. Specify all the settings 
![](./images/4.2.i003.png)

4. Validate the configuration selected
![](./images/4.2.i004.png)

6. Deploy your machine by clicking on "OK"
![](./images/4.2.i005.PNG)

## 4.2 Setting up Docker

1. Once your machine is deployed; Connect to the machine, for this Lab we will use Putty as is showing below
![](./images/4.2.i006.PNG)

2. User and Password are the same that you defined in the step 2 of this Lab
![](./images/4.2.i008.PNG)

3. Create a CA private "$ openssl genrsa -aes256 -out ca-key.pem 4096"
![](./images/4.2.i009a.PNG)
![](./images/4.2.i009b.PNG)

4. Create public keys "openssl req -new -x509 -days 365 -key ca-key.pem -sha256 -out ca.pem" **Do no forget specify your FQDN** 
![](./images/4.2.i009c.PNG)

5. Create a server key "$ openssl genrsa -out server-key.pem 4096" 
![](./images/4.2.i009d.PNG)

6. Create a CSR "openssl req -subj "/CN=$HOST" -sha256 -new -key server-key.pem -out server.csr" **Do no forget specify your HOST** 
![](./images/4.2.i009e.PNG)

7. Allow connections using IPs "$ echo subjectAltName = IP:10.10.10.20,IP:127.0.0.1 > extfile.cnf" **Make sure to use your own IPs**
![](./images/4.2.i009f.PNG)

8. Sign the public key "openssl x509 -req -days 365 -sha256 -in server.csr -CA ca.pem -CAkey ca-key.pem \ -CAcreateserial -out server-cert.pem -extfile extfile.cnf"
![](./images/4.2.i009g.PNG)

9. Create a client key "openssl genrsa -out key.pem 4096"
![](./images/4.2.i009h.PNG)

10. Create a CSR "openssl req -subj '/CN=client' -new -key key.pem -out client.csr"
![](./images/4.2.i009i.PNG)

11. Create an extensions config file "$ echo extendedKeyUsage = clientAuth > extfile.cnf"
![](./images/4.2.i009j.PNG)

12. Sign the public key "$ openssl x509 -req -days 365 -sha256 -in client.csr -CA ca.pem -CAkey ca-key.pem \ -CAcreateserial -out cert.pem -extfile extfile.cnf
![](./images/4.2.i009k.PNG)

13. Create Docker Certificates. Use base64 or another encoding tool to create base64-encoded topics

     ***~/.docker$ base64 ca.pem > ca64.pem***

     ***~/.docker$ base64 server-cert.pem > server-cert64.pem***

     ***~/.docker$ base64 server-key.pem > server-key64.pem***

13. At the end you should have all those keys listed below. **Store your keys, we will use it in step 17 in to this Lab**
![](./images/4.2.i009m.PNG)

14. Browse to Azure portal and open the Docker machine created in step 4.2 in this Lab.

15. Go to Extensions -> Add -> Select Docker extension
![](./images/4.2.i011.PNG)

16. Clicking on "Create" 
![](./images/4.2.i012.PNG)

17. Provide the key's location and click on "OK". **Check step 13 in this Lab**
![](./images/4.2.i013.PNG)

18. When the Docker extension deploy finish you will see the new Extension as is showing below
![](./images/4.2.i014.PNG)

## 4.3 Setting up Docker communication endpoint

1. Browse to Azure portal and open the Docker machine created in step 4.2 in this Lab.
2. Go to Network interfaces -> Network security group -> Inbound security rules -> Add
Fill all the fields
![](./images/4.2.i015.PNG)

3. When the rule has been deployed you will see it as is showing below
![](./images/4.2.i016.PNG)

4. Verify the Docker environment variables

   **export DOCKER_HOST=tcp://yourhost:2376**

   **export DOCKER_TLS_VERIFY=1**

   **export DOCKER_CERT_PATH=/yourpath/.docker/**

5. Verifying the connection
![](./images/4.2.i018.PNG)

