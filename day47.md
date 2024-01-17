---
title: "AWS Elastic Beanstalk"
datePublished: Wed Dec 13 2023 16:57:54 GMT+0000 (Coordinated Universal Time)
cuid: clq40lxan000208i0cojgc91k
slug: aws-elastic-beanstalk
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702408843382/f6e1c62f-80f7-457d-8432-fc856287aa08.png
tags: docker, aws, devops, elastic-beanstalk, 90daysofdevops

---

## What is AWS Elastic Beanstalk?

AWS Elastic Beanstalk is a Platform as a Service (PaaS) solution provided by Amazon Web Services (AWS) that simplifies the deployment and management of web applications. It supports multiple programming languages and runtime environments such as Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker. AWS Elastic Beanstalk allows developers to focus on their applications while AWS handles the underlying infrastructure and operational tasks.

## Components of AWS Elastic Beanstalk

* Application Version: Represents a specific iteration or release of an application's codebase.
    
* Environment Tier: Defines the infrastructure resources allocated for an environment (e.g., web server environment, worker environment).
    
* Environment: Represents a collection of AWS resources running an application version.
    
* Configuration Template: Defines the settings for an environment, including instance types, scaling options, and more.
    

### Advantages of AWS Elastic Beanstalk

* Highly scalable
    
* Fast and simple to begin
    
* Quick deployment
    
* Supports multi-tenant architecture
    
* Simplifies operations
    
* Cost efficient
    

## Elastic Beanstalk Environment

1. **Web Server Environment:** Web server environments are suitable for hosting web applications that handle incoming HTTP requests.
    
    * **Components:**
        
        * **Auto Scaling Group:** Web server environments typically include an Auto Scaling group of EC2 instances. This allows the environment to automatically scale the number of instances based on demand.
            
        * **Elastic Load Balancer (ELB):** An ELB is used to distribute incoming traffic among the instances in the Auto Scaling group. This enhances the availability and fault tolerance of the application.
            
        * **Web Server:** The web server environment is configured to handle incoming HTTP requests and respond to client requests.
            
2. **Worker Environment:** The Worker environments are suitable for applications that perform background processing or handle tasks independently of incoming HTTP requests.
    
    * **Components:**
        
        * **Auto Scaling Group:** Similar to web server environments, worker environments include an Auto Scaling group of EC2 instances. However, these instances are configured to perform background processing tasks.
            
        * **Message Queue (Optional):** Worker environments often use message queues, such as Amazon SQS, to distribute tasks among worker instances. This allows for asynchronous and distributed processing.
            
        * **Worker Process:** Worker environments are configured to run background processes or tasks independently of the web server. They are not directly involved in handling HTTP requests.
            

Choosing between a **web server environment** and a **worker environment** depends on your application's nature and the workload it needs to handle.

In some cases, applications may use a combination of web server and worker environments to handle different aspects of their functionality.

## Deploying the 2048 game using Docker and the AWS Elastic Beanstalk.

The Github Repo for the **2048 Game** project to be deployed, can be found [here](https://github.com/jabir000/2048?source=post_page-----3a79d6738916--------------------------------).

### **Containerization of the 2048 Web Application using Docker.**

Create an EC2 Instance on AWS and connect to it using SSH

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702480859565/0ea7b5c6-7610-4891-9876-f5b043274bab.png align="center")

Then, install Docker and Docker runtime on the EC2 instance.

Use the below command to check the status of the docker after installation.

```bash
sudo systemctl status docker
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702481043669/3fd0c729-03f5-4cce-9226-f2eeb865f880.png align="center")

Create a folder named "2048", and it is in this folder you will create your Dockerfile.

```bash
mkdir 2048
cd 2048
vim Dockerfile
```

Use the Vim editor to create and write in your "Dockerfile". Save and exit the editor.

```bash
FROM ubuntu:22.04
RUN apt-get update
RUN apt-get install -y nginx zip curl
RUN echo "daemon off;">>/etc/nginx/nginx.conf
RUN curl -o /var/www/html/master.zip -L https://codeload.github.com/jabir000/2048/zip/master
RUN cd /var/www/html/ && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip
EXPOSE 80
CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf"]
```

**Build the Image:** Run the following command to build the Docker image

```bash
docker build -t "your_docker_image" .
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702481725494/38f5abda-0a62-4a25-8a6f-f6e4895f149b.png align="center")

**Use the below command to verify the Image:**

```bash
sudo docker images
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702481840053/20117e38-4fe9-4aef-8064-c66487300d85.png align="center")

**Run a Container from the Image using the below command:**

```bash
sudo docker run -d -p 80:80 "your_image_id" 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702481992919/4e19847d-f1ff-47d0-b02a-3dca1c309dde.png align="center")

**Use the below command to verify the Container:**

```bash
sudo  docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702482073393/a7901d26-8afa-4f16-b7f8-2741010780a9.png align="center")

**You can then access your game by pasting the public IP address of your EC2 instance in your browser.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702482223426/d095ac76-c811-4e16-81ea-6dd793f694c6.png align="center")

The 2048 game was successfully deployed using Docker.

### **Deploying the 2048 game using AWS Elastic Beanstalk**

1. Open the AWS Management Console and go to the Elastic Beanstalk service.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702482687563/42e2f582-3111-4ef8-9207-7012e9a11d83.png align="center")

1. Click on "Create Application"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702482748783/3c4f41f5-2444-4047-832b-c8edf6c1a300.png align="center")

1. Configure environment: Choose "web server environment" under the Environment tier. Provide a name for your application and provide the Environment description.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702482788093/6eb242cd-9340-4375-86b5-896596fdda6c.png align="center")

Choose "Managed platform" as the Platform type. Choose "Docker" as the platform.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702483153434/053c4e48-cb11-49d5-8b5a-70e4b7e25ce2.png align="center")

**Under the Application code, choose "Upload your code"**

* Upload the ZIP archive containing your application code. Provide a version label and upload the Dockerfile you created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702483279199/89693b2e-3190-4098-b876-11fa3236ec0d.png align="center")

For the Configuration presets, choose "Single instance (free tier eligible)"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702483506458/9526c47a-c8c4-4284-8ef6-a906db0ca095.png align="center")

Configure service access: Select the “use an existing service role”, then go on to create an EC2 Instance profile in the IAM console with the required permissions for AWS Elastic Beanstalk as listed below.

a. **AWSElasticBeanstalkWebTier**

b. **AWSElasticBeanstalkWorkerTier**

c. **AWSElasticBeanstalkMulticontainerDocker**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702483845356/2463622c-8cd1-452c-9109-603d69b07948.png align="center")

Do not use the default VPC, create your custom VPC with the necessary inbound rules on the security group allowing HTTP/HTTPS traffic.

Choose the custom VPC you created and a Public subnet for the instance settings.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702483941426/23ee2616-527c-4366-ad88-8798d15f64a7.png align="center")

Then skip to Review: Review your configuration and Click on "Submit"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702484541202/a1a04536-fbfd-42ea-a361-b134ed1482ba.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702484560992/7be2db5e-aa1d-4060-8bee-be6f8e08874a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702484664774/e40cd457-75dc-482f-97a5-3d14064ee4a2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702484690212/2fc6aa00-c6bb-47bc-869b-fd0a18abd716.png align="center")

**Wait for Deployment:** Elastic Beanstalk will automatically handle the deployment. Monitor the progress in the AWS Management Console.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702484886537/3698ec30-8918-471b-b775-d5cc97ae7225.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702484976104/eb31a4b1-358c-4fa8-a7a6-ec7b536616d6.png align="center")

Access the Deployed Application: Once the deployment is complete, access the game application through the provided domain.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702485335095/9b01416d-5ad3-40a2-afb8-49ec770390a3.png align="center")

Thank you.
