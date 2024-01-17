---
title: "AWS and IAM Basics"
datePublished: Fri Dec 01 2023 19:37:43 GMT+0000 (Coordinated Universal Time)
cuid: clpn118jn000409jy6hw30ul8
slug: aws-and-iam-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701458508847/347d4945-6673-47c1-8c6f-32335f4c09a1.png
tags: aws, iam, devops-journey, 90daysofdevops, trainwithshubham

---

## AWS:

Amazon Web Services is one of the most popular Cloud Providers that has a free tier for students and Cloud enthusiasts for their Hands-on learning. Read from [here](https://aws.amazon.com/what-is-aws/).

## User Data in AWS:

* When you launch an instance in Amazon EC2, you have the option of passing user data to the instance that can be used to perform common automated configuration tasks and even run scripts after the instance starts. You can pass two types of user data to Amazon EC2: shell scripts and cloud-init directives.
    
* You can also pass this data into the launch instance wizard as plain text, as a file (this is useful for launching instances using the command line tools), or as base64-encoded text (for API calls).
    
* This will save time and manual effort every time you launch an instance and want to install any application on it like Apache, docker, Jenkins etc. Get to know IAM more deeply. [Click here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html)
    

### Task1:

* Launch EC2 instance with already installed Jenkins on it. Once the server shows up in the console, hit the IP address in the browser and your Jenkins page should be visible.
    
* Take a screenshot of the Userdata and Jenkins page, this will verify the task completion.
    

Log in to the AWS Management Console using your AWS account credentials. Go to the EC2 dashboard. Click on "Launch Instance" to create a new EC2 instance. Select an AMI that includes the operating system and other configurations you prefer.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701452488497/b47e2d8e-a274-43b8-b4e1-a1518f767481.png align="center")

When launching the instance, scroll down to the "Advanced Details" section, and you'll find a field for entering User data.

```plaintext
#!/bin/bash
sudo apt update
sudo apt install -y openjdk-11-jre
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo gpg --dearmor -o /usr/share/keyrings/jenkins-keyring.gpg
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.gpg] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install -y jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

You can then launch the EC2 Instance with User Data

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701452863674/08676f0b-87ef-4c6f-a604-d8f6cb8c22b7.png align="center")

Configure Security Group: Go to the Security Group and click on edit "inbound rules" to allow incoming traffic on port 8080

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701453603418/315c722d-bc05-4456-ac14-828c406b8861.png align="center")

Copy the public IP from the Instance details section

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701453808320/939b8956-2bc7-4c3d-8c61-5b9cca07c95b.png align="center")

You can access Jenkins by navigating to your public IP:8080 in a web browser.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701454036597/e9546249-e698-4b0b-88c8-2921c1c3b0c5.png align="center")

### Task2:

* Read more on IAM Roles and explain the IAM Users, Groups and Roles in your terms.
    
* Create three Roles named: DevOps-User, Test-User and Admin.
    

**IAM Users:**

IAM, or Identity and Access Management, secures access to your AWS services and resources. IAM users are entities within your AWS account that represent the people, applications, or services that interact with AWS resources. Each IAM user has its own set of security credentials (username and password or access key) and permissions. IAM users can be created, modified, and deleted as needed.

**IAM Groups:**

IAM groups are collections of IAM users. Instead of attaching policies directly to individual users, one can create groups, assign policies to the groups, and then add users to the groups.

**IAM Roles:**

IAM Roles in AWS allow entities to get credentials for a short duration. Unlike IAM users, intended for individual human users, IAM roles are typically used for applications or services needing AWS resources without long-term credentials.

Go to the IAM dashboard, click on Roles on the left side and then click the "Create role" button.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701458195080/7360456f-a8ce-4f9d-9ffb-802510179232.png align="center")

Choose the trusted entity type (e.g., AWS service and then EC2)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701458301427/a8b7c6ff-42af-47f9-880f-46b6b92621bc.png align="center")

Select the permissions policies for the role

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701458339743/325d8a59-b409-46bc-9e86-2b66ddf70d93.png align="center")

Review the role details and give it a name, such as DevOps-User. Click "Create role."

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701458414405/68421dc7-6f82-490e-9da4-1cd94b254f8d.png align="center")

Follow the same steps as above but this time name the role as `Test-User` and the last role as `Admin`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701458680175/804e5d11-b118-4bf2-ae9c-e8b6e452a21b.png align="center")
