---
title: "Getting Started with AWS Basics"
datePublished: Thu Nov 30 2023 22:00:13 GMT+0000 (Coordinated Universal Time)
cuid: clplqon3v000008l8cq9l9okq
slug: getting-started-with-aws-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701381339558/e90b237c-4c9c-4f9f-aa34-c986f19ca8f1.png
tags: aws, learning-journey, devops-articles

---

## AWS:

Amazon Web Services is one of the most popular Cloud Providers that has a free tier for students and Cloud enthusiasts for their Hands-on while learning (Create your free account today to explore more on it).

Read from [here](https://aws.amazon.com/what-is-aws/)

## IAM:

AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. With IAM, you can centrally manage permissions that control which AWS resources users can access. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.

Read from [here](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)

### Task1:

Create an IAM user with the username of your wish and grant EC2 Access. Launch your Linux instance through the IAM user that you created now and install Jenkins and docker on your machine via single Shell Script.

* Sign in to the AWS Management Console.
    
* Navigate to IAM (Identity and Access Management).
    
* In the IAM dashboard, click "Users" and "Add user."
    
* Enter a username of your choice, and click "Next."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701377355098/09edc946-bfe7-40ae-925c-5ed05c3dfaee.png align="center")

* Attach the "AmazonEC2FullAccess" policy to the user and click "Next."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701377417233/e94fd312-7871-48f5-95d2-8fa0eecd3f3b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701377517764/371843b1-4477-44a0-a69a-b3e7f3963f66.png align="center")

* Review the settings and click "Create user."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701377355098/09edc946-bfe7-40ae-925c-5ed05c3dfaee.png align="center")

* Note down the **username** and the **password** as they will be used to authenticate the IAM user.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701377842520/0d87b984-0ad8-4cf2-a4c2-28a07f696014.png align="center")

* Sign in to the AWS account using the IAM user you just created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701378110361/2feb1fc2-a8a8-44f9-a492-67861e957b54.png align="center")

* Reset the password
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701378237706/1244d5f7-29bf-4441-9093-98da095b44e8.png align="center")

* **Launch EC2 Instance with IAM User**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701378293921/6612bf0e-7c38-497b-beff-9a862706896f.png align="center")

* Connect to the instance you just created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701378622672/a3ced0a3-cdc8-4077-bac3-e941692241b0.png align="center")

**SSH into the EC2 Instance:**

* Wait for the instance to be in the "**running**" state.
    
* SSH into the instance using the public IP and your private key:
    
    ```plaintext
    ssh -i "YourKeyPair.pem" ubuntu@your-instance-ip
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701379032032/85e08485-80eb-4d74-8ead-df80c92f2218.png align="center")

* Install Jenkins and Docker on your machine via a single Shell Script.
    

```plaintext
#!/bin/bash

# Update package list
sudo apt update

# Install OpenJDK 11
sudo apt install -y openjdk-11-jre

# Install Jenkins
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo gpg --dearmor -o /usr/share/keyrings/jenkins-keyring.gpg
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.gpg] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install -y jenkins

# Start Jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins

# Install Docker
sudo snap install docker
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701379311844/2263a3f0-7eec-4b6a-bfe8-4a018f1d32e5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701379454003/7fd65ef7-2f4c-4029-a8e3-a1c87418d3df.png align="center")

### Task2:

In this task, you need to prepare a DevOps team of avengers. Create 3 IAM users of Avengers and assign them to DevOps groups with the IAM policy.

Sign in to the AWS Management Console. Navigate to IAM. In the IAM dashboard, click "Users" and "Add user." Create 3 IAM users of Avengers and assign them to DevOps groups with the IAM policy.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701380302203/9a8ccf4f-3bd5-4a95-ae4e-06b06a0e2543.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701380540375/179ca225-2679-43b4-a4b9-4322ece1776a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701380561567/4806f471-8404-44b5-826e-39d9a3ad4286.png align="center")