---
title: "Docker Cheatsheet"
datePublished: Fri Nov 03 2023 13:39:01 GMT+0000 (Coordinated Universal Time)
cuid: cloinw3fg000508k0cqsq4rzq
slug: docker-cheatsheet
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699017254475/9655102d-e1bd-4aff-8811-2d6851e40fba.png
tags: docker, devops, 90daysofdevops, trainwithshubham, dockercheatsheet

---

### **Docker Container Commands:**

1. **Create a Container**:
    
    docker create \[OPTIONS\] IMAGE \[COMMAND\] \[ARG...\]
    
2. **Start a Container**:
    
    docker start \[OPTIONS\] CONTAINER
    
3. **Stop a Container**:
    
    docker stop \[OPTIONS\] CONTAINER
    
4. **Remove a Container**:
    
    docker rm \[OPTIONS\] CONTAINER
    
5. **List Running Containers**:
    
    docker ps
    
6. **List All Containers(both stopped and running)**
    
    docker ps -a
    
7. **Inspect a Container**:
    
    docker inspect CONTAINER\_ID
    
8. **List the port mappings for a container**
    
    docker port CONTAINER\_ID
    
9. **To view resource usage statistics for one or more container**
    
    docker stats CONTAINER\_ID
    
10. **To display the running processes inside a specified container**
    
    docker top CONTAINER\_ID
    
11. **Execute a Command in a Running Container**:
    
    docker exec \[OPTIONS\] CONTAINER COMMAND \[ARG...\]
    
12. **To remove all stopped containers**
    
    docker container prune
    

### **Docker Image Commands:**

1. **List Local Images**:
    
    docker images
    
2. **Pull an Image from Docker Hub**:
    
    docker pull IMAGE\_NAME
    
3. **Remove an Image**:
    
    docker rmi IMAGE\_NAME
    
4. **Build an Image from Dockerfile**:
    
    docker build \[OPTIONS\] PATH\_TO\_DOCKERFILE
    
5. **Save one or more Docker images to a tar archive file.**
    
    docker save \[OPTIONS\] IMAGE \[IMAGE...\]
    
6. **Load Docker images from an archive file**
    
    docker load \[OPTIONS\]
    
7. **Log in to Docker Hub**:
    
    docker login
    
8. **Push an Image to Docker Hub**:
    
    docker push IMAGE\_NAME
    
9. **To remove unused or dangling images**
    
    docker image prune
    

### **Docker Volume Commands:**

1. **List Volumes**:
    
    docker volume ls
    
2. **Create a Volume**:
    
    docker volume create VOLUME\_NAME
    
3. **Remove a Volume**:
    
    docker volume rm VOLUME\_NAME
    

### **Docker Network Commands:**

1. **List Networks**:
    
    docker network ls
    
2. **Create a Network**:
    
    docker network create NETWORK\_NAME
    
3. **Remove a Network**:
    
    docker network rm NETWORK\_NAME
    

### **Docker Compose Commands:**

1. **Start Containers Defined in a Compose file**:
    
    docker-compose up \[OPTIONS\]
    
2. **Stop Containers Defined in a Compose file**:
    
    docker-compose down \[OPTIONS\]
    
3. **View Compose logs**:
    
    docker-compose logs \[SERVICE\]
    
4. **List Containers:**
    
    docker-compose ps
