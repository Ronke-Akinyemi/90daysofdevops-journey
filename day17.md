---
title: "Day 17 Task: Docker Project for DevOps Engineer"
datePublished: Tue Oct 31 2023 15:14:03 GMT+0000 (Coordinated Universal Time)
cuid: cloegyqn000000al5013kf085
slug: day-17-task-docker-project-for-devops-engineer
tags: docker, devops-journey, 90daysofdevops, trainwithshubham

---

### Docker

Docker is a tool that makes it easy to run applications in containers. Containers are like small packages that hold everything an application needs to run. To create these containers, developers use something called a Dockerfile.

### Dockerfile

A dockerfile is like a set of instructions for making a container. It tells the docker what base to use, what commands to run, and what files to include.

**Task:**

* Create a Dockerfile for a simple web application (e.g. a Node.js or Python app)
    
* Build the image using the Dockerfile and run the container
    
* Verify that the application is working as expected by accessing it in a web browser
    
* Push the image to a public or private repository (e.g. Docker Hub )
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698759186633/2396e57f-f669-4216-9d69-5b20d7f2ceb3.png align="center")

* `FROM`: Specifies the base image. Here, it's using the official Python image.
    
* `WORKDIR`: Sets the working directory inside the container to `/app`.
    
* `COPY`: Copies all files from the current directory to the container's `/app` directory.
    
* `RUN`: Installs Python dependencies from the `--no-cache-dir Flask`
    
* `EXPOSE`: Exposes port 5000.
    
* `ENV`: Sets an environment variable. (Optional)
    
* `CMD`: Defines the command to start the application. In this case, it runs `--host`
    

**Build the docker image:**

Open a terminal, navigate to your project directory and run the following command to build your Docker image:

`docker build -t my-python-app .`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698763393873/ee3298c8-84e6-489c-8f94-5e791ebfabf3.png align="center")

**Run the Docker container:**

After the image is built, run the container using:

`docker run -p 8080:5000 my-python-app`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698763813725/bc3134db-b227-4238-8e47-d33c21cdd6a4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698763451721/477d5e20-4c71-4020-b188-24d51109b09d.png align="center")

**Access the Application:**

Open a web browser and navigate to [`http://localhost:8080`](http://localhost:8080/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698765007405/461f4424-e036-4bc9-bf72-c795b62c60e8.png align="center")

**Pushing the Docker Image to DockerHub:**

* **Log in to Docker Hub**
    
* **Tag your local image with your Docker Hub repository name:**
    
* **Push the image to Docker Hub**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698764118010/fa6d9d13-78fe-4bc0-a1d1-c3c394ac0e44.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698763900228/d2321d7c-04ad-475f-97b8-dc223fbde1e5.png align="center")
