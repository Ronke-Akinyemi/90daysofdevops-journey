---
title: "Important Docker Interview Questions and Answers"
datePublished: Sat Nov 04 2023 17:49:39 GMT+0000 (Coordinated Universal Time)
cuid: clokca8zi000109kz4qjcftv4
slug: important-docker-interview-questions-and-answers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699119991186/97ebabd2-e14f-43eb-86af-66aa565c1766.png
tags: docker, devops, learning-journey, 90daysofdevops, trainwithshubham

---

1. ### **What is the Difference between an Image, Container and Engine?**
    
    **Image**: An image is a static, immutable file that serves as a template for creating containers. It comprises the application code, runtime, libraries, dependencies, and configurations needed to execute a specific application.
    
    **Container:** A container is a runtime instance created from an image. It encapsulates an application and its dependencies, ensuring consistency and reliability across different computing environments.
    
    **Engine:** The engine is the underlying software that enables the creation, running, and management of containers. The engine is responsible for building, running, and distributing containers. It interfaces with the underlying operating system's kernel, handling tasks such as creating and managing containers, networking, and storage.
    
2. ### **What is the Difference between the Docker command COPY vs ADD?**
    
    **COPY:** is a straightforward command specifically meant for copying files and directories from the host into the container during the build process. It has a simple syntax: `COPY <src> <dest>`.
    
    It is a recommended approach for most use cases, as it explicitly copies files and directories from the source to the destination within the container. COPY doesn't have additional features beyond copying local files and directories.
    
    ```dockerfile
    # Using COPY to copy a single file into the container
    COPY index.html /app/index.html
    
    # Using COPY to copy an entire directory into the container
    COPY ./src/ /app/src/
    ```
    
    In the above examples, the `COPY` command is used to copy a file named `index.html` from the host context into the `/app` directory in the container. It also copies the entire `src` directory from the host context into the `/app/src` directory in the container.
    
    **ADD:** has extended functionalities compared to COPY. In addition to copying files, it can also handle automatic extraction of compressed files (e.g., tar, gzip) and can fetch files from URLs.
    
    ```dockerfile
    # Using ADD to copy and automatically extract a compressed file into the container
    ADD app.tar.gz /app/
    
    # Using ADD to fetch a file from a URL and add it to the container
    ADD http://example.com/file.txt /app/file.txt
    ```
    
    In the above examples, the `ADD` command copies and extracts the contents of the `app.tar.gz` file from the host context into the `/app` directory in the container. Additionally, it fetches the `file.txt` from the specified URL and adds it to the `/app` directory in the container.
    
3. ### **What is the Difference between the Docker command CMD vs RUN?**
    
    `RUN` is used for executing commands during the Docker image build process. The instructions specified with `RUN` are executed at image build time. Each `RUN` command creates a new layer in the image.
    
    ```dockerfile
    RUN apt-get update && apt-get install -y package_name
    ```
    
    `CMD` is used to specify the default command to be executed when a container is started from the image.
    
    The CMD instruction in a Dockerfile provides the default command or executable that will run when a container starts from the built image. It is often used to define the primary process within the container.
    
    `RUN` commands are part of the image creation process, while the `CMD` command defines what will run when the container starts.
    
    ```dockerfile
    CMD ["python", "app.py"]
    ```
    
4. ### **How will you reduce the size of the Docker image?**
    
    **Use Smaller Base Images:** Begin with minimal base images like Alpine Linux to reduce the initial image size.
    
    **Use Multi-Stage Builds:** Employ multi-stage builds to separate the built environment from the runtime environment, copying only necessary essential files into the final image."
    
    **Optimize Dockerfile Instructions:** Combine commands to reduce the number of layers, use specific version tags, and minimize unnecessary components.
    
    **Use .dockerignore:** a .dockerignore file helps specify files and directories that should not be included in the image. This reduces the context size sent to the Docker daemon during image build.
    
    **Compress Files:** For files that must be included in the image, compress or minimize them. Use tools like gzip or other file compression techniques to reduce their size.
    
    **Optimize Caching:**
    
    Utilize Docker layer caching effectively by ordering commands in the Dockerfile. Place commands that change frequently earlier in the Dockerfile to take advantage of caching.
    
    **Cleanup Commands:**
    
    Remove temporary files, caches, and any unnecessary remnants after installation or setup steps. 
    
5. ### **Why and when to use Docker?**
    
    Docker ensures consistency by encapsulating applications and their dependencies into containers. This means that the environment in which the application runs is consistent across different stages of the development and deployment lifecycle. Docker containers are highly portable. Once an application is containerized, it can run on any system that supports Docker, irrespective of the underlying infrastructure. Docker simplifies the process of scaling applications. Docker scalability feature allows applications to handle varying workloads efficiently.
    
    Docker is well-suited for microservices architectures, enabling the deployment of independent services in separate containers. This modular approach enhances scalability, flexibility, and easier maintenance.
    
    Docker is used when you need to develop and deploy applications in the cloud**;** Docker containers are portable and easily deployed to any cloud platform. Docker is a good choice for running microservices-based applications because it is lightweight and efficient. Docker is a good choice for running web applications because it is scalable and easy to deploy. Docker is a good choice for running batch processing jobs because it efficiently distributes the workload across multiple containers.
    
6. ### **Explain the Docker components and how they interact with each other**
    
    **Docker Daemon (dockerd):** The Docker daemon serves as the fundamental background service responsible for overseeing and managing Docker containers. It listens for Docker API requests and communicates with the container runtime (e.g., containerd, runc) to create, run, and manage containers.
    
    **Docker Client:** The Docker client (Docker) is the primary interface through which users interact with Docker. It sends commands to the Docker daemon to build, run, and manage containers.
    
    **Docker Registries:** The Docker Registry is a storage location designed for storing and sharing Docker images. It can be public (like Docker Hub) or private within an organization to manage and distribute their own Docker images.
    
7. ### **Explain the terminology: Docker Compose and Docker File.**
    
    **Docker Compose:** allows docker to set up multi-container environments. One can easily use a single command to build images and run all the containers.
    
    **There is a three-step process to work with Docker Compose**
    
    1\. Define the application environment with Dockerfile for all services.  
    2\. Create a docker-compose.yml file defining all services under the application.  
    3\. Run `docker-compose up` to run all services under applications.
    
    The docker-compose commands provide several subcommands to manage Docker containers with docker-compose. Docker-compose comes by default with docker installation.
    
    **DockerFile:** A dockerfile is like a set of instructions for making a container. It tells the docker what base to use, what commands to run, and what files to include.
    
8. ### **Docker vs Hypervisor?**
    
    **Docker** and **Hypervisor** are different technologies that can virtualize computing resources. However, they have different strengths and weaknesses and are best suited for different use cases.
    
    **Docker** uses containers to isolate applications from each other and the underlying operating system. Containers are lightweight and portable and can be started up and stopped very quickly. Docker is often used for developing and deploying microservices-based applications.
    
    **Hypervisors** create virtual machines (VMs) that can run multiple operating systems on a single physical server. VMs are more heavyweight than containers, but they offer greater isolation and flexibility. Hypervisors are often used for running enterprise applications and for consolidating workloads.
    
9. ### **What are the advantages and disadvantages of using docker?**
    
    ### **Advantages**
    
    **Portability:**  Portability is a crucial strength of Docker, as it allows containers to be highly mobile and capable of running on any system that supports the Docker platform. Portability enables consistent deployment across different environments, from development to production.
    
    **Efficiency:** Containers are lightweight and share the host system's kernel, making them more resource-efficient than traditional virtual machines.
    
    **Consistency:** Docker enables developers to package applications and their dependencies together. This consistency ensures that the application runs the same way across different environments.
    
    **Scalability:** Docker allows easy scaling of applications. With orchestration tools like Kubernetes, Docker Swarm, or Docker Compose, managing and scaling containers becomes simpler.
    
    ### **Disadvantages of Docker:**
    
    **Complex Networking:** Docker networking can be complex when dealing with multiple containers and inter-container communication. It might require specific knowledge and planning to set up the desired network configurations.
    
    **Security Concerns:** While Docker containers provide isolation, misconfigurations or vulnerabilities within containers or in the Docker environment can pose security risks. Proper security measures must be taken to mitigate these risks.
    
    **Performance Overhead:** In specific scenarios, running multiple containers on a single host might incur some performance overhead due to shared resources.
    
    **Persistence and State Management:** Containers are temporary, so managing persistent data might require additional configuration and understanding of volume management in Docker.
    
    **The overhead of Microservices:** For small applications, using Docker might introduce overhead due to the added complexity of containerization.
    
10. ### **What is a Docker namespace?**
    
    A Docker namespace is a Linux kernel feature that isolates processes from each other and the underlying operating system. This isolation is achieved by creating separate namespaces for different aspects of a process, such as its process ID (PID), network interface, filesystem mounts, and inter-process communication (IPC) resources.
    
11. ### **What is a Docker registry?**
    
    A Docker registry is a central repository for storing, managing, and distributing Docker container images. It is a storage location for these images, enabling users to share and access them easily. The most commonly used Docker registry is Docker Hub, a public registry provided by Docker that allows developers to share and collaborate on container images.
    
12. ### What is an entry point?
    
    An entry point in Docker is a command executed when a Docker container is started. It is defined in the Dockerfile using the ENTRYPOINT instruction. The entry point command can be anything, such as a shell script, a binary executable, or a Python script.
    
13. ### **How to implement CI/CD in docker?**
    
    Here are the key steps to set up CI/CD with Docker:
    
    **Version Control System (VCS):** Ensure your project code is stored in a version control system such as Git. This enables versioning and collaboration among developers.
    
    **Dockerize Your Application:** Create a Dockerfile to containerize your application. Define the necessary dependencies, configurations, and commands to build your application into a Docker image.
    
    **CI Server Integration:** Integrate your VCS with a Continuous Integration server (e.g., Jenkins, GitLab CI/CD, Travis CI) to automate the build process. Configure the CI server to pull code from the repository, build the Docker image, and run tests within a Docker container.
    
    **Automate Testing:** Implement automated tests within the CI pipeline. These tests can include unit tests, integration tests, or any other relevant tests for your application.
    
    **Artifact Repository:** Store the built Docker images in a Docker registry (e.g., Docker Hub, AWS ECR, or a private registry). This registry will store the images and make them accessible for deployment.
    
    **Continuous Deployment:** Automate the deployment process by using a Continuous Deployment tool or scripts. Define deployment stages (e.g., staging, production) and configure the CI/CD pipeline to push the built Docker images to the appropriate environment.
    
    **Orchestration with Docker Compose or Orchestration Tools:** Use Docker Compose or container orchestration tools like Kubernetes, Docker Swarm, or Amazon ECS to manage and orchestrate multiple containers as part of your application. These tools allow for scaling, load balancing, and managing containerized applications in a production environment.
    
    **Monitoring and Logging:** Implement monitoring and logging solutions to track the performance and behaviour of your Dockerized applications in different environments. Tools like Prometheus, ELK Stack (Elasticsearch, Logstash, Kibana), or cloud-native monitoring services can be used for this purpose.
    
14. ### **Will data on the container be lost when the docker container exits?**
    
    Yes, by default, data on the container will be lost when the Docker container exits. This is because Docker containers are ephemeral, meaning that they are intended to be created, used, and then destroyed. When a container exits, all of its data is deleted unless you have taken steps to persist it.
    
    **There are two main ways to persist data in Docker containers:**
    
    * **Docker volumes:** Docker volumes are directories or files that exist outside of the container filesystem. When you mount a volume inside a container, any data written to that volume will persist even after the container is stopped or deleted.
        
    * **Bind mounts:** Bind mounts allow you to mount a directory or file from the host machine inside the container. This allows you to share data between the container and the host, and any data written to the mounted directory or file will also persist even after the container is stopped or deleted.
        
    
15. ### **What is a Docker swarm?**
    
    Docker Swarm is Docker's native clustering and orchestration tool used to manage a group of Docker hosts as a single virtual system. It allows you to deploy and manage a cluster of Docker nodes, treating them as a single entity. This enables you to scale applications across multiple Docker hosts, load balance across the cluster, and manage failover and high availability.
    
16. ### **What are the docker commands for the following:**
    
    View running containers
    
    ```plaintext
    docker ps
    ```
    
    Command to run the container under a specific name 
    
    ```plaintext
    docker run --name container_name image_name
    ```
    
    Command to export a docker image
    
    ```plaintext
    docker save -o file_name.tar image_name
    ```
    
    Command to import an already existing docker image - 
    
    ```plaintext
    docker load -i file_name.tar
    ```
    
    Commands to delete a container
    
    ```plaintext
    docker rm container_name
    ```
    
    Command to remove all stopped containers, unused networks, build caches, and dangling images
    
    ```plaintext
    docker system prune -a
    ```
    
    Thanks for reading!