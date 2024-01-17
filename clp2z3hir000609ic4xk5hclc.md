---
title: "Kubernetes"
datePublished: Fri Nov 17 2023 18:48:06 GMT+0000 (Coordinated Universal Time)
cuid: clp2z3hir000609ic4xk5hclc
slug: kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700245827402/fd4e7b8f-7542-4896-a4f3-b181d48cd677.png
tags: kubernetes, devops, 90daysofdevops, trainwithshubham

---

**Kubernetes Overview**

With the widespread adoption of [containers](https://cloud.google.com/containers) among organizations, Kubernetes, the container-centric management software, has become a standard for deploying and operating containerized applications and is one of the most important parts of DevOps.

Originally developed at Google and released as open-source in 2014. Kubernetes builds on 15 years of running Google's containerized workloads and the valuable contributions from the open-source community. Inspired by Google’s internal cluster management system, [Borg](https://research.google/pubs/pub43438/).

## Tasks

1. What is Kubernetes? Write in your own words and why do we call it k8s?
    
2. What are the benefits of using k8s?
    
3. Explain the architecture of Kubernetes
    
4. What is a Control Plane?
    
5. Write the difference between kubectl and kubelets.
    
6. Explain the role of the API server.
    

# Kubernetes

**Kubernetes (K8s)** is an open-source container orchestrating tool designed to automate, deploy, scale, and operate containerized applications.

"K8s," is a shorthand notation derived from the word "Kubernetes." The number 8 represents the eight letters between "K" and "s" in the word. This abbreviation is commonly used in the tech community as a convenient way to refer to Kubernetes, especially in commands, filenames, and other contexts where brevity is important.

# Benefits of using k8s

1. **Scalability:** Kubernetes makes it effortless to scale applications up or down seamlessly based on demand. It automatically adds or removes containers as needed, ensuring your applications can handle fluctuating workloads without performance bottlenecks.
    
2. **Portability:** Containers encapsulate an application and its dependencies, making it easy to move and run the application consistently across different environments, from development to production.
    
3. **Resource Efficiency:** Kubernetes optimizes the utilization of hardware resources by efficiently scheduling containers on the available nodes, ensuring that resources are used effectively.
    
4. **High Availability:** Kubernetes supports multi-node clusters and automatically handles the distribution of application instances across these nodes. This enhances the availability of applications by reducing the impact of node failures.
    
5. **Self-healing:** If a container or node fails, Kubernetes can automatically detect the failure and reschedule containers on healthy nodes, maintaining the desired state of the application.
    
6. **Access to Cloud-Native Management Tools:** Kubernetes integrates with various cloud-native management tools, providing features like auto-scaling, load balancing, and service discovery. This integration enhances the overall management and optimization of your applications.
    
7. **Rolling Updates and Rollbacks:** Kubernetes supports rolling updates, allowing for the seamless deployment of new versions of applications without downtime. If an issue arises, rollbacks can be performed quickly.
    
8. **Easy Deployment and Updates:** Kubernetes simplifies application deployment and updates using declarative manifests. These manifests describe the desired state of the application, and Kubernetes handles the actual deployment process, ensuring consistent and reliable updates.
    
9. **Open-Source and Free:** Kubernetes is an open-source project, providing free access to its robust features and extensive community support. This open-source nature fosters collaboration, innovation, and various tools and integrations.
    
10. **Container Orchestration:** Kubernetes automates the deployment, scaling, and management of containerized applications, simplifying the process of running applications in containers.
    
11. **Large and Active Community:** Kubernetes has a vibrant and active community that contributes to its development, provides documentation, and offers support to users. This active community ensures that Kubernetes remains a relevant and evolving platform.
    

# Architecture of Kubernetes

1. **Master Node:** The master node is responsible for coordinating and overseeing the entire cluster. It manages the scheduling of applications, monitors their health, and ensures that the desired state of the cluster matches the actual state. The master node acts as the control plane for the Kubernetes cluster, and it typically consists of several components, each serving a specific purpose:
    
    * **API Server:** The API server is the critical component for all administrative tasks and communication within the cluster. It exposes the Kubernetes API, which allows users and other components to interact with the cluster. All the communication between the components of the master node and the worker nodes happens through the API server.
        
    * **etcd:** etcd is a distributed key-value store that is used as the backing store for all cluster data. This includes the configuration details of the cluster, the state of each node, and information about pods, services, and other objects. 
        
    * **Controller Manager:** Controllers are responsible for tasks such as node auto-scaling, handling replication controllers, and ensuring that the desired state of the system is maintained.
        
    * **Scheduler:** The Scheduler is responsible for placing containers onto available nodes in the cluster.
        
2. **Node (Worker Node):**
    
    * **Kubelet:** The primary agent that runs on each node and is responsible for ensuring that the containers are running in a Pod.
        
    * **Kube-proxy:** Maintains network rules on nodes, enabling communication between Pods and external traffic. It also performs simple load balancing for services.
        
    * **Container Runtime:** The software responsible for running containers, such as Docker.
        
3. **Pod:** The smallest deployable unit in Kubernetes. A Pod represents a single instance of a running process in a cluster and may contain one or more containers that share the same network namespace.
    
4. **Controller:** The controller helps manage and regulate the state of the cluster. They manage the lifecycle of Pods and other objects, ensuring that the current state matches the desired state.
    
5. **Service:** A Service defines a set of Pods and a policy to access them. It provides a stable endpoint (IP address and port) to access the deployed application.
    
6. **Volume:** A Volume in Kubernetes represents a directory that is accessible to all containers in a Pod. It can be used to share data between containers and persists beyond the lifecycle of a Pod.
    
7. **Namespace:** A way to divide cluster resources between multiple users, teams, or projects. It provides scope for Pods, Services, and other resources, helping in organizing and isolating workloads.
    
8. **ConfigMap and Secret:** ConfigMaps allow you to decouple configuration artifacts from image content, while Secrets are used for managing sensitive information such as passwords or API keys.
    

# Control Panel

The control plane in Kubernetes refers to the set of components that manage the overall state of the cluster, making decisions about what and where to run applications. It is responsible for regulating and orchestrating various tasks to ensure that the cluster's desired state matches the actual state. The control plane components run on the master node(s) in a Kubernetes cluster.

# Differences between kubectl and kubelets

| **Feature** | **kubectl** | **kubelet** |
| --- | --- | --- |
| **Purpose** | CLI tool for managing and interacting with the Kubernetes cluster. | Node agent responsible for managing containers on a node. |
| **User Role** | Used by administrators and developers. | Runs on each node and is primarily used by the node itself. |
| **Functionality** | Manages Kubernetes resources, deploys applications, and performs cluster operations. | Ensures containers are running on the node according to instructions from the master. |
| **Component Type** | Standalone CLI tool installed on user machines. | System component running on each node in the cluster. |
| **Communication** | Communicates with the Kubernetes API server over the network. | Communicate with the API server to report node status and receive container deployment instructions. |
| **Abstraction Level** | Provides a high-level abstraction for managing the cluster. | Works at the node level, managing containers and reporting node status. |

# Roles of the API server

1. **Validation and Configuration:** The API server validates and configures user-submitted requests, ensuring that the desired state of the cluster is accurately represented and adheres to defined policies.
    
2. **Resource Management:** The API server is responsible for creating, updating, and deleting Kubernetes resources, such as pods, deployments, services, and namespaces. It maintains a consistent view of the cluster's state and ensures that resource requests are fulfilled according to defined rules.
    
3. **Authentication and Authorization:** The API server implements authentication and authorization mechanisms to control access to the cluster and its resources. It verifies user identities and enforces access control policies, ensuring that only authorized users can perform actions on the cluster.
    
4. **Event Handling:** The API server records events that occur within the cluster, providing valuable insights into its operation and potential issues. These events can be used for monitoring, troubleshooting, and auditing purposes.
    
5. **Communication with Components:** The API server serves as the central communication point for the control plane, interacting with other Kubernetes components, such as the scheduler, controller manager, and kubelet, to coordinate the management of workloads and cluster resources.