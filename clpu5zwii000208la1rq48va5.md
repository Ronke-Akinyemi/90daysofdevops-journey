---
title: "Setting up an Application Load Balancer with AWS EC2"
datePublished: Wed Dec 06 2023 19:31:02 GMT+0000 (Coordinated Universal Time)
cuid: clpu5zwii000208la1rq48va5
slug: setting-up-an-application-load-balancer-with-aws-ec2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701889629185/3b475907-32af-4e5a-8589-7100765c8abe.png
tags: aws, devops-journey, trainwithshubham

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701809630282/cbd32d91-b31f-4360-879e-1347478f703b.png align="center")

## What is Load Balancing?

Load balancing is the distribution of workloads across multiple servers to ensure consistent and optimal resource utilization. It is an essential aspect of any large-scale and scalable computing system, as it helps you to improve the reliability and performance of your applications.

## Elastic Load Balancing:

**Elastic Load Balancing (ELB)** is a service provided by Amazon Web Services (AWS) that automatically distributes incoming traffic across multiple EC2 instances. Elastic Load Balancer provides three types of load balancers:

1. **Application Load Balancer (ALB):** An Application Load Balancer operates at layer 7 of the Open Systems Interconnection (OSI) model. The ALB is designed for applications that primarily use HTTP/HTTPS protocols. It supports advanced features like HTTP/2, request routing based on URLs, methods, headers, and SSL/TLS termination.
    
2. **Network Load Balancer (NLB):** Network Load Balancer operates at layer 4 of the Open Systems Interconnection (OSI) model. The NLB is optimized for TCP and UDP protocols and is well-suited for microservices, containerized applications, and high-performance applications that require low-latency traffic delivery. It supports IP address-based routing, port-based routing, and connection tracking.
    
3. **Classic Load Balancer (CLB):** The Classic Load Balancer is a simpler and less feature-rich type of load balancer. The CLB operates at layer 4 of the Open Systems Interconnection (OSI) model. It is primarily used for legacy applications that are incompatible with the more modern ELB types.
    

### Task 1: Launch 2 EC2 instances with an Ubuntu AMI and use User Data to install the Apache Web Server.

* Modify the index.html file to include your name so that when your Apache server is hosted, it will display your name also do it for 2nd instance which includes " TrainWithShubham Community is Super Awesome :) ".
    
* Copy the public IP address of your EC2 instances.
    
* Open a web browser and paste the public IP address into the address bar.
    
* You should see a webpage displaying information about your PHP installation.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701879578461/013eb22c-c719-4498-ac56-c9ea6a51c43d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701880264586/d55f3c6b-8e11-428c-b20b-19d1128cf5f6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701880168616/b2a1bd05-71d4-4581-ba75-b189ff7f769d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701880421305/58a2d5dd-c4f9-4ba0-aea2-cb74ae5a45f0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701880672122/f8d8cebc-49dd-4da8-afb1-7533ad34e499.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701880696776/362b579e-60b5-4d1f-ba20-d76bccf484f6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701880988100/2d222354-2808-4764-bc7a-a166d52addc0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701879957979/21fbcbd1-2ab9-4a35-adb5-889ed22642a8.png align="center")

### Task 2: Create an Application Load Balancer (ALB) in EC2 using the AWS Management Console.

* Add EC2 instances which you launch in task-1 to the ALB as target groups.
    
* Verify that the ALB is working properly by checking the health status of the target instances and testing the load-balancing capabilities.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701881533068/040cb3a3-4040-4d75-8b8c-3e2a46a9262b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701881893238/30ec69ab-6f60-4bda-af03-dd7746fb161a.png align="center")

* Create a new security group or choose an existing one.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701882405310/0f0c9f63-7783-447f-a84f-80c77ef51939.png align="center")

**Configure Routing:** Create a new target group or choose an existing one.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701882178588/18dd6961-bfcc-435c-9a46-a5e9372057a9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701882592906/84f1ed47-7c2c-40ff-9c5d-05c607dbcbf2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701883011531/1d5d9f89-5fb9-4fca-90dd-d661f50228e5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701883142256/581e8425-4797-44d5-894b-020857dfc867.png align="center")

* **Register Targets:**
    
    * Add the EC2 instances you launched in Task 1 to the ALB as target group.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701883268930/410dc0f1-95c0-436c-9ccc-d8c251a4ccb6.png align="center")

* **Review and Create:** Review your settings and click "Create target group."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701883369961/475b3b4a-d4d9-4da7-ac0b-386af25a64e6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701883479024/2394968c-18bc-4807-a304-f2e9d204e096.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701887044517/a72e29f7-fea2-4489-a978-86dbabf8dd22.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701887250559/aaee5a5c-853d-4316-9b61-a3bb46873272.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701887385702/d7438a8e-4aa1-4fd1-8eb2-f913a6a389c1.png align="center")

**Verify Target Health:**

* Go to the "**Target Groups**" section in the EC2 dashboard. Click on the target group associated with your ALB.
    
* Verify that the status of your EC2 instances is "healthy."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701888093122/2e9881c2-4c47-463a-9ddf-77bbc8616207.png align="center")

* **Test Load Balancing:** Copy the DNS name of your ALB (can be found in the "Description" tab). Open a web browser and paste the DNS name in the address bar.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701888249740/b64e60ab-4b3b-41eb-aace-2a94f0a00b48.png align="center")

* Refresh the page, and you should see the different responses from your two instances, indicating that the ALB is distributing traffic.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701888426912/8a780eb3-4c83-461b-9b21-048140d601b9.png align="center")