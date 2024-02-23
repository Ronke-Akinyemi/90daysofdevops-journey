---
title: "Jenkins Freestyle  Project-1"
datePublished: Fri Feb 23 2024 19:03:55 GMT+0000 (Coordinated Universal Time)
cuid: clsz0tbc0000009jvgy6b2sia
slug: jenkins-freestyle-project-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708713367691/9ae13276-176b-41bf-9202-709f17c7f58b.png
tags: docker, aws, jenkins, 90daysofdevops

---

### Project Description

The project aims to automate the building, testing, and deployment process of a web application using Jenkins and GitHub. The Jenkins pipeline will be triggered automatically by GitHub webhook integration when changes are made to the code repository. The pipeline will include stages such as building, testing, and deploying the application, with notifications and alerts for failed builds or deployments.

### Sign in to your AWS account and create a new instance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708520806308/ee90f689-c2da-4915-b875-7acdb8f278ca.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708520841632/c0d24aec-c349-4565-bde7-842ea987a5ea.png align="left")

* Utilize the User Data field to install Docker and Jenkins during instance initialization.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708520898271/9f8f73a5-5d24-4ef1-bf25-981fb4195ecc.png align="left")

### Launch the Instance:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708682256105/7f9b6cbf-6bdc-4dba-89b3-81fc22b01408.png align="center")

* Connect to the instance to check if docker and Jenkins are running.
    

```basic
systemctl status docker
systemctl statud jenkins
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708682763243/6c078573-a649-4d59-86be-f561d8d9dc4e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708682816166/623e970b-8785-4d88-9861-69ffe2736276.png align="center")

* Open port 8080, the default port for running Jenkins, on the server and port 8000 to access the webpage.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708683503621/73652e33-9a16-4788-99b2-daaf274bb5ae.png align="center")

* Navigate to the URL http://&lt;public url&gt;:8080
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708683644369/610b1fcc-60f7-49bb-8ed6-7ed72956dc01.png align="center")

* To retrieve the "Administrator password," run the following command:
    

```basic
 sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708683955517/d8948c1b-7dc6-4ace-b338-ba6aad3f4f2b.png align="center")

* Copy that and paste it in the "Administration password" space and click on continue.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708684132968/ef9fe61e-e0be-4f4f-b81d-d5441ab9ef43.png align="center")

* Then click on "Install suggested plugins" to install all the suggested plugins.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708684232162/31a0744b-7335-457f-9cc3-c068d781a370.png align="center")

* Create First Admin User: Set up the initial admin user by providing all required input. Save and continue.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708684570031/c73ecad3-d2b0-4d7c-9530-b0a01fa4a58e.png align="center")

### Now, Jenkins is ready

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708684682097/e22c6d90-c81d-4366-98a6-2b4e2c7f4788.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708685698766/553a61b5-a884-4588-8208-068c67a5aa90.png align="center")

* Now, create a Jenkins Pipeline: Click on “New Item” to create a new job. Enter an item name and click on "Freestyle project".
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708684871192/62b23503-b2dd-4004-9489-11c11849a850.png align="center")

* Provide a description, then click on "GitHub project" and go to GitHub to copy the repository url.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708686343576/20c4936c-9e83-4c27-80fe-aa46bcd1a6cb.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708686586921/91d6137b-d0b6-48ac-9032-7b1f6fc2cba5.png align="center")

### You need to install necessary Jenkins plugins for integration with GitHub

* Click on "Manage Jenkins" in the left sidebar, then select "Manage Plugins" from the dropdown menu.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708687237098/81eb175b-76ad-40c5-82d4-69c636335fd2.png align="center")

* Go to the "Available" tab. In the search box, type in "GitHub Integration Plugin"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708687342314/51d4db13-1720-4dbe-9167-c3fc4d781e5c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708687575904/556d63de-3dfe-4b4f-ada2-74c441b8984b.png align="center")

* Navigate to GitHub and select Webhook. Enter the payload URL. Select the content type as application/json and click on "Add webhook".
    

```basic
http://<publicIP>:8080/github-webhook/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708687908033/0f2335f2-1111-4ee4-bf79-1eed77a9a2e9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708690943183/7e162e51-72ff-41d7-ad18-4684de7719b9.png align="center")

### Generate SSH Key:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708691362932/fda24121-ac59-45a4-a689-f602b47aceea.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708691477474/af6bec70-7d14-4bc0-ac93-e5fd1e38e1b4.png align="center")

* After generating the SSH key pair , add the public key to your GitHub account settings. Provide the public key of the server you want to connect to and click on "Add SSH key".
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708692164190/8a182ef9-fccc-4758-845b-7feb10a012ed.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708692399605/e2e99128-942f-4ae4-bcd2-bb52c001cf20.png align="center")

###   
Generate a personal access token in GitHub to establish the connection between GitHub and Jenkins.

* To generate a personal access token on GitHub, follow these steps: click your profile icon, then navigate through "Settings" &gt; "Developer settings" &gt; "Personal access tokens", and finally click on the "Generate new token" button to start creating a new token.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708693061583/1756f08a-11ed-4d96-b89d-0171b3853e91.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708693281088/edecc6db-a655-4bc9-b843-04db03d22bcf.png align="center")

* After generating the token, make sure to copy it to a secure place.
    
* In Jenkins, navigate to the setting up global credential.
    
* Select the type "Secret text" and paste the token you copied earlier.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708693578507/a7e324e8-bc7d-4964-bc9c-4404c13081af.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708693766240/db2673dd-3d0c-4d81-992b-90418707cf0e.png align="center")

* In the "Build Triggers" section, select "GitHub hook trigger for GITScm polling" because a webhook has already been set up, enabling Jenkins to trigger builds in response to webhook notifications from GitHub.
    
* Then, in the build steps, select the "Execute shell" option and add the following to build and run the docker container.
    

```basic
docker build . -t django-notes-app
docker run -d -p 8000:8000 django-notes-app
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708694666226/06be089f-83b4-466e-b4cd-423d2f17b19c.png align="center")

* Now, Click on Build Now and check the console output.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708709718022/b0e90a50-ca32-48b7-be4b-60e46689e296.png align="center")

* To ensure that the previous container is stopped before building and running a new one, let's update the Jenkins job configuration with the following steps:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708710624852/ce1659a3-14d5-4708-aa22-92453fbb03ae.png align="center")

* Modify the code of your web application and push the updates to your GitHub repository.
    
* The Jenkins pipeline will be triggered automatically by GitHub webhook integration when changes are made to the code repository.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708709787583/09acd9bb-24f2-4110-be54-f30e32e9fad5.png align="center")

* Navigate to the URL &lt;public\_IP:8000&gt; and check for the web-application.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708710001004/51ca9865-b763-40e1-9d4e-91f49bc2bafc.png align="center")

Thank you for reading.