---
title: "AWS EC2 Automation"
datePublished: Tue Dec 05 2023 20:24:18 GMT+0000 (Coordinated Universal Time)
cuid: clpssgj98000308jv3w522zfd
slug: aws-ec2-automation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701807742507/7fa9a310-fb06-4f4d-a0bc-6418681fe1fb.png
tags: aws, devops, 90daysofdevops

---

## Automation in EC2:

Amazon EC2 or Amazon Elastic Compute Cloud can give you secure, reliable, high-performance, and cost-effective computing infrastructure to meet demanding business needs.

Also, if you know a few things, you can automate many things.

## Launch template in AWS EC2:

* You can make a launch template with the configuration information you need to start an instance. You can save launch parameters in launch templates so you don't have to type them in every time you start a new instance.
    
* For example, a launch template can have the AMI ID, instance type, and network settings that you usually use to launch instances.
    
* You can tell the Amazon EC2 console to use a certain launch template when you start an instance.
    

## Instance Types:

Amazon EC2 has a large number of instance types that are optimised for different uses. The different combinations of CPU, memory, storage and networking capacity in instance types give you the freedom to choose the right mix of resources for your apps. Each instance type comes with one or more instance sizes, so you can adjust your resources to meet the needs of the workload you want to run.

## AMI:

An Amazon Machine Image (AMI) is an image that AWS supports and keeps up to date. It contains the information needed to start an instance. When you launch an instance, you must choose an AMI. When you need multiple instances with the same configuration, you can launch them from a single AMI.

### Task1:

* Create a launch template with Amazon Linux 2 AMI and t2.micro instance type with Jenkins and Docker setup (You can use the Day 39 User data script for installing the required tools.
    
* Create 3 Instances using Launch Template.
    

* **Create a launch template:**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701801358183/0dc9127e-1f0c-4873-81e6-2e4653fe227d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701801899454/8ee9786c-6df4-45b0-8cbb-3c39d3f4ed65.png align="center")

* **Provide the AMI as Amazon Linux 2:**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701803119165/a85d9de7-a0eb-4c3a-ab46-24a5267356eb.png align="center")

* **Select Instance Type: t2.micro**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701803278301/e231ceb0-50ff-41c4-aabd-56b5a4910b59.png align="center")

* **Select an existing security group or create one:**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701803385612/954e8512-442f-48b1-962e-ca744e9a2060.png align="center")

* Write a User Data script for Jenkins and Docker setup.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701803499820/784e88f2-7f32-47f5-bc46-7603ce542bd3.png align="center")

* **Click the launch template and use the launched template to launch instances:**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701803649284/5661a3a1-93f9-4e91-aef9-002df6d16369.png align="center")

* **Specify the number of instances you want to launch: Here I'm launching 3 instances:**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701803804330/97a2b32f-c67f-4dc2-a32f-387e90012fd7.png align="center")

* **Click on Instances and you will see the launched instances:**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701804137509/3615e8a1-cc34-405a-bce5-9b839af74941.png align="center")

* ### **You can go one step ahead and create an** **auto-scaling group**.
    

### **Auto-Scaling Group:**

An Auto Scaling Group (ASG) is a service offered by Amazon Web Services (AWS) that enables you to scale your Amazon EC2 (Elastic Compute Cloud) instances automatically based on defined conditions. The primary purpose of an Auto Scaling Group is to ensure that you have a specified number of instances running to handle the load for your application.

* **Go to the Auto Scaling Section to create an Auto Scaling Group using the launch template that was just created:**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701804919199/d59c408e-2388-46f7-b4a1-443f086401ca.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701804945903/9541cd52-8b61-42b2-8e94-16d9d30347c4.png align="center")

* **Select availability zones and subnets:**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701805105011/b4c879ac-4fad-476b-ac10-dc57b7d017ca.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701805376480/2f199921-76a7-4348-ba05-f8b08a6fa24c.png align="center")

* **Configure the desired capacity and scaling policies:**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701805514666/bcd8b535-9882-4f83-93a5-8ce529b0b422.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701805543753/22b519d4-81e6-423e-9bf4-bc887e45a6e5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701805646970/95c65995-7eba-4be9-9d5c-ade72af00bf8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701805666975/33f017d3-5a1c-473b-8b21-80d4dfadbc0a.png align="center")

* **Review and click "Create auto-scaling group"**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701805684759/4813df8d-a672-42f1-97b0-322784cff9db.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701805768720/4cb0e299-7a40-4788-b204-9bce567a65e9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701805797965/16ae153e-67e4-4e86-9940-b9ade60bd4c8.png align="center")

* **Then, click on "Instances"**
    

Here, there are 5 Instances, 3 were created from the first task and the remaining 2 were created by the auto-scaling group because in the **desired capacity** I specified 2.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701805851761/42122c5e-9008-4a99-a168-c1e43827c128.png align="center")

...
