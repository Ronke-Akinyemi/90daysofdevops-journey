---
title: "Working with Namespaces and Services in Kubernetes"
datePublished: Tue Nov 21 2023 19:36:28 GMT+0000 (Coordinated Universal Time)
cuid: clp8ql3sk00060al80nyk4m7t
slug: working-with-namespaces-and-services-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700595221402/4c9151d8-873b-4964-a05d-220fc00c26d6.png
tags: kubernetes, devops, devops-articles, devops-journey

---

### What are Namespaces and Services in Kubernetes?

* In Kubernetes, Namespaces are used to create isolated environments for resources. Each Namespace is like a separate cluster within the same physical cluster.
    
* Services are used to expose your Pods and Deployments to the network.
    

## Task 1:Create a Namespace for your Deployment

* Use the below command to create a Namespace
    
    `kubectl create namespace <namespace-name>`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700588718590/f550c928-f198-4f3b-b2b4-03ed3f03582d.png align="center")

* Update the deployment.yml file to include the Namespace
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700589862935/3a7de796-323b-4803-991e-367e97a30783.png align="center")

* Apply the updated deployment using the command:
    
    `kubectl apply -f deployment.yml -n <namespace-name>`
    

Here's a breakdown of the command:

* **kubectl apply**: This is the primary command for applying or updating Kubernetes resources.
    
* **\-f** deployment.yml: This flag specifies the path to the YAML or JSON file containing the configuration for the Kubernetes resource you want to create or update. In this case, it's a file named deployment.yml.
    
* **\-n** &lt;namespace-name&gt;: This flag specifies the namespace in which the resources should be created or updated. 
    

Putting it all together, the command

 **kubectl apply -f deployment.yml -n &lt;namespace-name&gt;**

 is saying: "Apply the configuration specified in the deployment.yml file to the Kubernetes cluster, and do it in the namespace named &lt;namespace-name&gt;."

This command is commonly used when you want to deploy or update resources within a specific namespace in a Kubernetes cluster. It ensures that the resources are created or updated in the specified namespace rather than the default namespace.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700588851488/c476f4c2-6f6b-4b30-9fe0-9123ade3dcb5.png align="center")

* Verify that the Namespace has been created by checking the status of the Namespaces in your cluster.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700588934426/9290d975-9560-4561-8f17-15e6df26e6b1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700588961210/3b348e61-4a9a-42f8-88d6-5722e70e50aa.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700590673477/f027355d-e238-47d5-83ce-c440d6a3c4b7.png align="center")

### Task 2:Read about Services, Load Balancing, and Networking in Kubernetes

**Services**

A Kubernetes Service is an abstraction that outlines a collection of Pods and establishes a policy for interacting with them. It provides a consistent endpoint, comprising an IP address and port, facilitating communication with a cluster of replicated Pods.

**Load Balancing**

Load balancing guarantees the equal distribution of traffic among numerous Pods, enhancing application availability and reliability.

**Networking**

Networking enables seamless communication between containers, pods, and services within the cluster. It encompasses various components and mechanisms facilitating efficient data exchange and traffic management.

Thanks for reading!
