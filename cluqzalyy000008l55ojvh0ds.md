---
title: "Project-4"
datePublished: Mon Apr 08 2024 13:18:38 GMT+0000 (Coordinated Universal Time)
cuid: cluqzalyy000008l55ojvh0ds
slug: project-4
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1712579694127/d300bdae-ad77-4b35-9509-565d8ffb82af.png
tags: docker, aws, devops

---

# Project Description

The project aims to deploy a web application using Docker Swarm, a container orchestration tool that allows for easy management and scaling of containerized applications. The project aims to demonstrate the benefits of Docker Swarm for deploying and managing containerized applications in production environments.

## **Setting Up the Environment on AWS EC2**

To deploy a web application using Docker Swarm on AWS EC2, you'll prepare your environment by setting up three instances with Docker pre-installed. You can use the EC2 User Data to execute scripts upon instance launch for streamlining Docker installation.

```bash
#!/bin/bash

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

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712570368521/5d8485b3-baff-42cb-a68e-89b02b94289f.png align="center")

* Ensure that inbound rules for all the three instances allowed Custom TCP traffic on `ports 2377` and `8001` from anywhere (IPv4) within the AWS console.
    
* This ensures communication between your manager nodes and worker nodes in the cluster and grants external access to your applications as necessary.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712572103404/c9e95054-ba5c-4eac-8374-e97fb8a98bf4.png align="center")

### **Initialize Swarm Mode on Manager Node**

* SSH into the EC2 instances assigned as the manager node i.e "Swarm-manager"
    
* Run the following command to initialize Swarm mode:
    

```basic
docker swarm init
```

* The `docker swarm init` command is used to initialize a Docker Swarm on a node, effectively turning it into a Swarm manager.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712574317896/1e2b5ab4-a19d-4569-bdb4-e2d3e00d02cd.png align="center")

* After running `docker swarm init`, Docker generates a join token, which you can use to add worker nodes to the Swarm.
    
* Copy and run the copied token on the remaining servers to add worker nodes to the Swarm.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712575782428/ae184149-da82-4a95-abd5-d974c08cd39f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712575866604/e419eea3-e83d-41b7-8348-95fcaf03dd7f.png align="center")

* To check all the connected nodes on the manager node in a Docker Swarm cluster, you can use the following command:
    

```basic
docker node ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712576235398/b8169e4e-0983-463e-a2a5-4be0068a5bcb.png align="center")

### **Creating a Docker Swarm Service on the Manager Node**

* To create a service on the manager node, run the following command:
    

```basic
docker service create --name django-app-service --replicas 3 --publish 8001:8001 trainwithshubham/react-django-app:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712577016328/e1c2065a-b200-483b-932d-92304625e8b5.png align="center")

* Now, to list the services running within the Docker Swarm cluster, run the following command:
    

```basic
docker service ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712577348914/56bd58b5-495e-4d9a-820f-19eda0617688.png align="center")

* The `docker ps` command is used to list all currently running containers.
    

```basic
Docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712577551136/6f34a8ad-667c-4830-ac06-c57a946414db.png align="center")

* To verify that your service is running across all nodes in your Docker Swarm cluster, you can access the application by using the IP address of any node in the cluster, followed by the specified port number, here, 8001. `<Public IPv4 address:8001>`
    
* **Swarm-manager**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712582065181/415b57b7-08bd-4d91-a787-1f835bf33a0c.png align="center")

* **Swarm-worker1**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712578556854/73eddfd7-51b2-4f92-8057-4be3412a201c.png align="center")

* **Swarm-worker2**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712578587014/6a9af0df-27c9-4749-a194-bed829a4df9e.png align="center")

### **Removing Nodes**

* You can remove a node from the environment if needed by using the command `docker swarm leave` on the respective worker node.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712579254060/0e876911-aada-4014-80cd-5413be299e6c.png align="center")

* To verify if a node has been successfully removed from the Docker Swarm cluster, you can check the list of nodes using:
    

```basic
docker node ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712579377697/34d6c65b-32ee-4d43-a833-1b18b7e040dd.png align="center")

Thank you for reading