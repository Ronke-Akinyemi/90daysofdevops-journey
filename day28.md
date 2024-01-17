---
title: "Day 28 Task: Jenkins Agents"
datePublished: Wed Nov 15 2023 20:16:04 GMT+0000 (Coordinated Universal Time)
cuid: clp07cx8t000209jq5lnzfbcw
slug: day-28-task-jenkins-agents
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700079072423/3dc3dc3a-b92e-426e-bc08-e053cda34047.png
tags: aws, devops, jenkins, 90daysofdevops, trainwithshubham

---

# Jenkins Master (Server)

Jenkins’s server or master node holds all key configurations. The Jenkins master server is like a control server that orchestrates all the workflow defined in the pipelines. For example, scheduling a job, monitoring the jobs, etc.

# Jenkins Agent

An agent is typically a machine or container that connects to a Jenkins master and this agent executes all the steps mentioned in a Job. When you create a Jenkins job, you have to assign an agent to it. Every agent has a label as a unique identifier.

When you trigger a Jenkins job from the master, the actual execution happens on the agent node that is configured in the job.

A single, monolithic Jenkins installation can work great for a small team with a relatively small number of projects. As your needs grow, however, it often becomes necessary to scale up. Jenkins provides a way to do this called “master to agent connection.” Instead of serving the Jenkins UI and running build jobs all on a single system, you can provide Jenkins with agents to handle the execution of jobs while the master serves the Jenkins UI and acts as a control node.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700071228557/74497167-78dd-49e2-8d36-07f59ca97750.png align="center")

## Pre-requisites

Let’s say we’re starting with a fresh Ubuntu 22.04 Linux installation. To get an agent working make sure you install Java ( same version as Jenkins master server ) and Docker on it.

`Note:- While creating an agent, be sure to separate rights, permissions, and ownership for Jenkins users.`

# Task-01

* Create an agent by setting up a node on Jenkins
    
* Create a new AWS EC2 Instance and connect it to the master(Where Jenkins is installed)
    
* The connection of the master and agent requires SSH and the public-private key pair exchange.
    
* Verify its status under the "Nodes" section.
    

### Steps:

1. **Create an EC2 Instance:**
    
    * Log in to your AWS Management Console.
        
    * Navigate to the EC2 Dashboard.
        
    * Launch a new EC2 instance. Choose an Amazon Machine Image (AMI), and instance type, and configure other details. In this case, we're using Ubuntu AMI
        
    * In the "Configure Security Group" step, ensure that port 22 (SSH) is open.
        
    * Launch the instance and select an existing or create a new key pair.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700073967302/df0099d2-2b5d-4809-8022-f37b97a5d546.png align="center")
    
2. **Connect to the EC2 Instance:** Use the private key associated with your key pair to connect to the EC2 instance via SSH.
    
    Example:
    
    ```bash
    ssh -i /path/to/private-key.pem ubuntu@your-ec2-instance-public-ip
    ```
    
3. #### Install Java and Jenkins on the Jenkins Master EC2 Instance:
    

```bash
 sudo apt update
 sudo apt install openjdk-11-jre
 #Install Jenkins
 curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
 echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
   https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
   /etc/apt/sources.list.d/jenkins.list > /dev/null
 sudo apt-get update
 sudo apt-get install jenkins
 #Start jenkins
 sudo systemctl enable jenkins
 sudo systemctl start jenkins
 sudo systemctl status jenkins
```

1. Install Java and Docker on the Jenkins Agent EC2 instance:
    

```bash
##Java

$ sudo apt update
$ sudo apt install openjdk-11-jre
$ java -version

##Docker

$ sudo apt-get update
$ sudo apt-get install docker.io
```

1. Verify the services are running on the two instances
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700074533017/8c6525f3-d402-4761-9f76-142872e40334.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700074552838/031625b1-b047-440d-ab00-764f6474cb03.png align="center")

1. #### Set up SSH Key Pair Exchange: Generate SSH key pair on your Jenkins Master EC2 Instance:
    

```bash
ssh-keygen
cd .ssh
ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700075225964/4e97b760-2a84-455e-89be-67fa313bb254.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700075623598/039f37bb-87aa-4521-9bd1-15f1f64c50c3.png align="center")

1. Copy the public key(id\_rsa.pub) from the master to the Agent EC2 instance
    
2. In the Agent Instance:
    

```bash
cd .ssh
vim authorized_keys
```

1. Edit authorized keys and paste the public key from the master instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700076132285/106f2408-1aca-4bd9-b979-7e4da7e48c3d.png align="center")

1. #### Set up a new node:
    

* Go to your Jenkins master web interface.
    
* Navigate to "Manage Jenkins" -&gt; "Manage Nodes and Clouds."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700076349862/f4639d0f-1a90-4316-8063-3bae74cf21d1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700076420219/12229cff-6b12-4c7b-8177-52589430cef0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700076512032/33d1b2c9-c956-41bd-a465-e47d05427e4b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700076719440/d7e6e964-cc8c-4b57-9adf-c7a613b48288.png align="center")

1. In the "Launch method" select launch agent via SSH and in the "Host" section, input the public IP of the Agent instance
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700077450151/5103fc1d-3434-44ce-9d5f-0dedf2434541.png align="center")

1. "Add Credential" is where you will add your credentials if you don't have them saved already.Select "**SSH username with private key**". Fill all required details, and in the private key area add **Private key from the master instance (id\_rsa).**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700076736157/b51aa48f-8c43-464d-8842-04dc9acebe46.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700076750893/d3be05df-8f3d-4cda-9fde-323830506549.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700076829515/6a0ee615-2e14-4ead-948f-955161da03d5.png align="center")

1. Enter "Save"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700077843126/973535e1-f42d-42f9-b352-0ed7ab70a09d.png align="center")

# Task 2

* Run your previous Jobs (which you built on Day 26, and Day 27) on the new agent
    
* Use labels for the agent, your master server should trigger builds for the agent server.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700078099325/af9e69c2-21e0-4bf8-bb92-1b6a83313c1d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700078255937/0cf7fb05-03a7-46a5-96e5-b84e61647f1a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700078392773/ef3fae0d-ba61-446f-9ab6-a82b0843caa2.png align="center")
