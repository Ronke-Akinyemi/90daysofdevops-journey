---
title: "Docker for DevOps Engineer"
datePublished: Thu Nov 02 2023 20:49:54 GMT+0000 (Coordinated Universal Time)
cuid: clohnucp0000108l4b3y23o9j
slug: docker-for-devops-engineer
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698958038813/d0fec6ff-cf74-48b8-a228-37705a7eb66e.png
tags: docker, devops, docker-compose, trainwithshubham

---

## **Docker Volume**

In Docker, a volume is a managed data storage area that exists independently of a container's life cycle. It allows for persistent data storage, detached from a specific container, and can be shared among multiple containers. Volumes are managed by Docker and can be easily backed up, moved, and restored. They are designed to facilitate data sharing and persistence across containers within the Docker environment. Volumes do not expand the size of containers that use them. Instead, they act as separate storage entities outside the container's main structure. This means that even if a container is removed or replaced, the data within the volume remains intact and unaffected.

Using the `-v` flag in Docker commands is concise but combines all options into a single field, making it less explicit. On the other hand, the `--mount` flag provides a more explicit and verbose approach by separating the options. The key distinction lies in how the syntax is structured. Here's a comparison illustrating the syntax for each flag:

**\-v Syntax:**

```bash
docker run -v /host/path:/container/path -v /data:/data:ro -v /more/data
```

**\--mount Syntax:**

```bash
docker run --mount type=bind,source=/host/path,target=/container/path --mount type=bind,source=/data,target=/data,readonly --mount type=volume,source=/more/data
```

The `--mount` flag separates the options explicitly, making it clearer and more organized, while the `-v` syntax combines them into a single field, sacrificing some readability for brevity.

**There are different types of volumes in Docker**

1. **Named Volume:** These are named entities managed by Docker. They are more convenient and easier to manage as Docker takes care of the location and lifecycle.
    
    ```bash
    docker volume create my_volume
    docker run -v my_volume:/path/in/container my image
    ```
    
2. **Anonymous Volumes:** These are created when a container needs a private volume that doesn't need to be shared or managed outside that container.
    
    ```bash
    docker run -v /path/in/container my_image
    ```
    
3. **Bind Mounts:** These allow you to specify a directory on the host machine that will be mounted into the container.
    
    ```bash
    docker run -v /host/path:/container/path my_image
    ```
    

### Common Docker Volume Commands

* **Create a volume**
    
    `docker volume create my_volume`
    
* **List volumes**
    
    `docker volume ls`
    
* **Inspect a volume**
    
    `docker volume inspect my_volume`
    
* **Remove a volume**
    
    `docker volume rm my_volume`
    

### **Docker Network**

In Docker, a network is a virtual communication bridge that allows containers to interact with each other and with other resources. It provides a means for containers to communicate within the Docker environment. Docker supports different types of networks, such as bridge, host, overlay, and macvlan, each serving specific connectivity purposes. Networks enable containers to share data and communicate in isolated environments, offering flexibility in managing how containers interact and exchange information.

### Common Docker Network Commands

* **Create a Network**
    
    `docker network create <network_name>`
    
* **List Networks**
    
    `docker network ls`
    
* **Inspect a Network**
    
    `docker network inspect <network_name>`
    
* **Connect a Container to a network**
    
    `docker network connect <network_name> <container_name>`
    
* **Disconnect a Container from a network**
    
    `docker network disconnect <network_name> <container_name>`
    
* **Remove a Network**
    
    `docker network rm <network_name>`
    

**Task 1**

Create a multi-container docker-compose file which will bring *UP* and bring *DOWN* containers in a single shot ( Example - Create application and database container )

```bash
version : "3.3"
services:
  web:
    image: varsha0108/local_django:latest
    deploy:
        replicas: 2
    ports:
      - "8001-8005:8001"
    volumes:
      - my_django_volume:/app
  db:
    image: mysql
    ports:
      - "3306:3306"
    environment:
      - "MYSQL_ROOT_PASSWORD=test@123"
volumes:
  my_django_volume:
    external: true
```

The configuration implies that the `web` service container requires the `my_django_volume` volume to persist data within the `/app` directory. This volume is assumed to exist beforehand or be created externally. If the `my_django_volume` volume does not exist, you can create it using the following command.

```bash
docker volume create my_django_volume
```

1. Use the `docker-compose up` command with the `-d` flag to start a multi-container application in detached mode.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698952340185/e38e7c72-caaa-400e-b670-6ae256c09d16.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698952363687/47420309-bbec-4d18-9b2c-324c8931e731.png align="center")

1. Use the `docker-compose scale` command to increase or decrease the number of replicas for a specific service. You can also add [`replicas`](https://stackoverflow.com/questions/63408708/how-to-scale-from-within-docker-compose-file) in the deployment file for *auto-scaling*.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698954338742/7b13fd44-f3cf-47b1-9d94-72d97694cc42.png align="center")

1. Use the `docker-compose ps` command to view the status of all containers, and `docker-compose logs` to view the logs of a specific service.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698955018548/632450da-dc3a-47bd-9970-99e991ac2ac4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698954504262/bc4a6d64-65c7-43f4-ab63-369294a66b56.png align="center")

1. Use the docker volume ls command to list all volumes and the docker volume rm command to remove the volume when you're done.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698954563768/4d999429-87a4-46db-9d32-e1d5e375311f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698954426938/fc211a5e-dde7-4d11-9a28-408c5e08993e.png align="center")

**Task 2**

Learn how to use Docker Volumes and Named Volumes to share files and directories between multiple containers.

* **Create a new volume -** `docker volume create ubuntu_volume`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698955476384/c7c89fbf-1b63-4f4c-bbbe-28b927b207af.png align="center")

Create two or more containers that read and write data to the same volume using the `docker run --mount` command.

`docker run -d --name nginx_container_1 -v ubuntu_volume:/app nginx:latest docker run -d --name nginx_container_2 -v ubuntu_volume:/app nginx:latest`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698955998703/3c5a006a-3228-43dc-ae41-96020a84bad7.png align="center")

Verify that the data is the same in all containers by using the `docker exec` command to run commands inside each container.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698956561269/a60ddb24-c0b3-4953-91e8-e3f72eb48e29.png align="center")

Use the docker `volume ls` command to list all volumes and the docker `volume rm` command to remove the volume when you're done.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698956760114/54157354-24cd-4d85-89f5-752164df3f38.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698956781651/357d695f-7455-4541-94d0-85976c8f7221.png align="center")

Further insights on Docker volumes can be found on SpaceLift's blog. Explore more on this topic [here](https://spacelift.io/blog/docker-volumes).

Thank you!