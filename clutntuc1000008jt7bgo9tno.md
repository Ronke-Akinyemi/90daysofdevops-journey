---
title: "Deploying a Node.js App on AWS ECS Fargate and AWS ECR"
datePublished: Wed Apr 10 2024 10:20:58 GMT+0000 (Coordinated Universal Time)
cuid: clutntuc1000008jt7bgo9tno
slug: deploying-a-nodejs-app-on-aws-ecs-fargate-and-aws-ecr
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1712744219020/27187436-bec7-4e74-965c-d6aed24e46c4.png
tags: aws, cloud-computing, devops

---

# Project Description

The project involves deploying a Node JS app on AWS ECS Fargate and AWS ECR. The project aims to demonstrate the process of deploying a Node.js application using AWS ECS Fargate and AWS ECR, showcasing a serverless infrastructure approach. This involves creating a Docker container for the Node.js app, storing the container image in AWS ECR (Elastic Container Registry), and running the containerized application on AWS ECS (Elastic Container Service) with Fargate, which allows for running containers without having to manage servers or clusters.

### **Step 1: Launch an EC2 Instance**

1. Create a new EC2 instance with user data that includes commands to install AWS CLI and Docker.
    

```bash
#!/bin/bash
echo "AWS CLI Installation"
echo "------------------------------------------------------------------"
sudo apt install -y unzip
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
echo "Docker installation"
echo "------------------------------------------------------------------"
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ubuntu
sudo reboot
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712657820433/b8843f89-f5cb-4ea8-8777-f0c333edd72c.png align="center")

### **Step 2: Clone the GitHub Repository**

Clone the GitHub repository containing your Node.js application to your AWS EC2 instance where you will configure AWS ECR.

```bash
git clone https://github.com/Ronke-Akinyemi/node-todo-cicd.git
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712658305760/a026bae9-1e7f-4762-990a-d66c57bcc00c.png align="center")

### **Step 3: Configure AWS ECR**

To create an ECR Repository, open the AWS Management Console and navigate to Amazon ECR. Click "Create repository". Name your repository and configure settings as needed. Then click "create creation".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712662452894/4b8e7168-8871-4496-abb7-0fc4a10b7e96.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712662485007/b9be4bfa-c965-44eb-a453-6d7bfa0062b6.png align="center")

### **Step 4: Create an IAM role and attach the required policies**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712742520725/5753ad1d-0197-4a31-9be2-41b39b41ea1f.png align="center")

### **Step 5: Configure AWS CLI**

Install AWS CLI on the instance. After installation, run the `aws configure` command to set up your credentials.

```bash
aws configure
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712663843961/c2242c5e-2bc2-4ae7-9b98-900e98273349.png align="center")

### **Step 6: Push the Image to ECR**

Navigate to the ECR repository created earlier and select "View push commands".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712664362810/a265624b-6d41-4d3b-849d-3d07efa82a4c.png align="center")

To push an image to the `ronke/node-todo-app` ECR repository, follow these steps:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712736586238/622f73ae-57e0-4dd1-9c39-793b9a721c59.png align="center")

1. Retrieve an authentication token and authenticate your Docker client to your registry. Use the AWS CLI:
    

```bash
aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/e2b3s2m7
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712664788396/e2875ba4-9d27-4b1d-b3d4-1e97a4de8eb3.png align="center")

2. Build your Docker image using the following command.
    

```bash
docker build -t ronke/node-todo-app .
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712665307023/2e933305-2bf3-40e1-8633-78cba5bbdeb4.png align="center")

3. After the build completes, tag your image so you can push the image to this repository:
    

```bash
docker tag ronke/node-todo-app:latest public.ecr.aws/e2b3s2m7/ronke/node-todo-app:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712665466699/5964519f-3a6d-44dc-a6f3-bf1dd53d9c41.png align="center")

4. Run the following command to push this image to your newly created AWS repository:
    

```bash
docker push public.ecr.aws/e2b3s2m7/ronke/node-todo-app:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712665595062/b64843f8-4462-44fd-bc7f-3286f1c78e0d.png align="center")

### **Step 7: Configure AWS ECS**

From the AWS Management Console, navigate to the Elastic Container Service (ECS). Click on the "Create repository". Provide a name for your repository and any additional configuration. Then click on the "Create repository" to create the repository. Select AWS Fargate as the launch type.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712738333940/8f5aeb62-37d8-454d-8721-4e9a4cb2f6df.png align="center")

### **Step 8: Create Task Definition**

Define task definitions by specifying your container images, CPU, memory, and the container ports for the application to run on.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712739026213/cfb4a8ae-fe3f-42e0-8d56-58bd473c7868.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712739076502/7b2d21b2-6cc9-4243-9bc0-4f7739908c64.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712739169861/57ffba1f-e11c-45cd-bcb3-9f4e79991f8d.png align="center")

### **Step 9: Review and Create**

Review the task definition configuration to ensure everything is set up correctly and then click on the "Create" button to create the task definition. Once the task definition is created, it can be used to run tasks within your ECS cluster.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712739731817/8b1064d7-c2ed-4ef3-889a-25db885f4835.png align="center")

### **Step 10: Deploy Task:**

Click on "Deploy", and then click on "Run task" to deploy your application as ECS task.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712740312079/90336805-a124-40c5-be6f-d6f9abe66a7f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712740339653/46e861a4-ffab-4487-9c13-ea749d0e595b.png align="center")

### **Step 11: Verify the task is running**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712740450920/fc91687c-9431-49d1-beb3-f886b49ca56c.png align="center")

### **Step 12: Open the Port in the Security Group**

Ensure port 8000 is open in the Security Group used in your task.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712741587804/4b0e5f63-c00f-4eaa-a33d-67a2462a4d51.png align="center")

### **Step 13: Navigate to the created task public IP address**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712741837642/51029190-e43b-4761-8d67-e2d944c926fd.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712741320168/e723fc81-112e-42fd-8877-612c68fde0b5.png align="center")

Thank you for reading.