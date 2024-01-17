---
title: "Day 18 of #90DaysOfDevops"
datePublished: Wed Nov 01 2023 14:33:46 GMT+0000 (Coordinated Universal Time)
cuid: clofuysk2000309juepsdgg3t
slug: day-18-of-90daysofdevops
tags: docker, devops, trainwithshubham

---

# Docker compose

Docker Compose allows docker to set up multi-container environments. One can easily use a single command to build images and run all the containers.

**There is a three-step process to work with Docker Compose**

1\. Define the application environment with Dockerfile for all services.  
2\. Create a docker-compose.yml file defining all services under the application.  
3\. Run `docker-compose up` to run all services under applications.

The docker-compose commands provide several subcommands to manage Docker containers with docker-compose. Docker-compose comes by default with docker installation.

## Docker-compose commands

**build -** This is used to build images for services for which the build is defined.

**up -** This will create docker containers with available services in docker-compose `.yml` file in the current directory.

**down -** This will stop and delete all containers, network and associated images for the services defined in a configuration file.

**ps -** This will list all containers created for the services defined in a configuration file with their status, port bindings and command.

**exec -** This is used to execute a command to the running container.

**start -** This is used to start stopped containers of the services defined in the configuration file.

**stop -**This will stop running containers for the services defined in the configuration file.

**restart -** This is used to restart containers of the services defined in a configuration file.

**pause -** This is used to pause running containers for the services defined in a configuration file.

**unpause -** This is used to start paused containers for the services defined in a configuration file.

**rm -** This is used to remove stopped containers for the services in a configuration file.

## YAML

### What is YAML?

YAML, a human-readable data serialization language, is an acronym for "YAML Ain't Markup Language," known for its simplicity and readability. Its widespread use in handling configuration files and data exchange is due to its capacity to create easily interpretable formats for both humans and machines. This versatility makes YAML a popular choice for applications requiring seamless data serialization. YAML files use a .yml or .yaml extension,and follow specific syntax rules.

It uses indentation to represent data structures, making it relatively human-readable, similar to how Python uses indentation for defining scope. YAML is often used in scenarios such as configuration files for software, specifying data formats, and exchanging information between systems. The structure of YAML is based on key-value pairs and nested structures.

### **Task 1**

Learn how to use the docker-compose.yml file, to set up the environment, configure the services and links between different containers, and also to use environment variables in the docker-compose.yml file.

### Sample of a docker-compose.yaml file

```bash
version : "3.3"
service
  web:
    image: nginx:latest
    ports:
    - "80:80"
  
  db:
    image: mysql
    ports:
    - "3306:3306"
    environment:
    - "MYSQL_ROOT_PASSWORD=test@123":s
```

**Run Docker-compose:** open a terminal and navigate to the directory where your 'docker-compose.yml' file is located and run:

`docker-compose up` will start the services defined in the composed file and if the images('nginx:latest' and 'mysql') are not available on your machine, Docker will pull them from DockerHub.

The 'web' will be accessible at 'http://localhost:80', and the 'db' service will be accessible at 'localhost:3306'.

**To stop and remove the services**

`docker-compose down` will stop and remove the containers, networks, and volumes created by 'docker-compose up'.

### Task 2

* Pull a pre-existing Docker image from a public repository (e.g. Docker Hub) and run it on your local machine. Run the container as a non-root user (Hint- Use `usermod` command to give user permission to docker). Make sure you reboot instance after giving permission to user.
    
* Inspect the container's running processes and exposed ports using the docker inspect command.
    
* Use the docker logs command to view the container's log output.
    
* Use the docker stop and docker start commands to stop and start the container.
    
* Use the docker rm command to remove the container when you're done.
    

**Pull the docker image from the public repository ('nginx')**

`docker pull nginx`

**Run the containner as a non-root user**

`docker run -d -p 9090:80 --name new_nginx --user $(id -u):$(id -g) nginx`

* `docker run`: This is the command to start a new container.
    
* `-d`: It runs the container in detached mode, meaning it runs in the background.
    
* `-p 9090:80`: This maps port 9090 on the host machine to port 80 in the container.
    
* `--name new_nginx`: This sets the name of the container as "new\_nginx".
    
* `--user $(id -u):$(id -g)`: This will run the container as a non-root user by setting the user ID and group ID to the current host user's ID.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698832165248/f6143f3d-3daa-448f-b504-a49ce9955c52.png align="center")

**Inspect running processes and exposed ports:** `docker inspect new_nginx`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698834318418/cafa8981-4d71-4694-91d6-0c2c342468d7.png align="center")

**View container's log output:** `docker logs new_nginx`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698846966206/c8df12bf-82c6-4efd-bad1-f3e19a7fe524.png align="center")

**Stop the container:** `docker stop new_nginx`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698847044407/14cba35f-b66d-4ba2-827c-d92fe8dcb0c8.png align="center")

**Start the container:** `docker start new_nginx`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698847081222/d695a5d0-2f8c-43e4-b3df-2c830a3dcaf8.png align="center")

**Remove the container:** `docker rm new_nginx`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698847350113/93910522-5cea-458b-bff0-51d5cb67bdb9.png align="center")