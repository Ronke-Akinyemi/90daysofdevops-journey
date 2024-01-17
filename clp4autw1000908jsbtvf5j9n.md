---
title: "Launching your First Kubernetes Cluster with Nginx running"
datePublished: Sat Nov 18 2023 17:05:03 GMT+0000 (Coordinated Universal Time)
cuid: clp4autw1000908jsbtvf5j9n
slug: launching-your-first-kubernetes-cluster-with-nginx-running
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700325131629/0d14ffeb-a526-4796-93dd-065cbfeff2d2.png
tags: kubernetes, devops, 90daysofdevops, trainwithshubham

---

### **What is minikube?**

Minikube is a tool which quickly sets up a local Kubernetes cluster on macOS, Linux, and Windows. It can deploy as a VM, a container, or on bare metal.

Minikube is a pared-down version of Kubernetes that gives you all the benefits of Kubernetes with a lot less effort. This makes it an interesting option for users who are new to containers, and also for projects in the world of edge computing and the Internet of Things.

### **Features of minikube**

* Minikube supports the latest Kubernetes release (+6 previous minor versions)
    
* Cross-platform (Linux, macOS, Windows)
    
* Deploy as a VM, a container, or on bare-metal
    
* Multiple container runtimes (CRI-O, containerd, docker)
    
* Direct API endpoint for blazing-fast image load and build
    
* Advanced features such as LoadBalancer, filesystem mounts, FeatureGates, and network policy
    
* Add-ons for easily installed Kubernetes applications
    
* Supports common CI environments
    

### Understanding the concept of Pod

Pods are the smallest deployable units of computing that you can create and manage in Kubernetes. A Pod is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers. A Pod's contents are always co-located and co-scheduled, and run in a shared context. A Pod models an application-specific "logical host": it contains one or more application containers which are relatively tightly coupled.

## **Task-01: Install Minikube on your local**

For installation, you can visit [here](https://minikube.sigs.k8s.io/docs/start/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700323067566/a40140f8-6e2b-4225-a410-ebf96f533661.png align="center")

After the installation is complete, go to your terminal and run `minikube version`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700323107461/fa91b809-cbb5-4a49-bb42-e4c1f024f529.png align="center")

## **Task-02:** Create your first pod on Kubernetes through minikube

Open your terminal and launch your Minikube cluster with this command : `minikube start`

The `minikube start` command will start a local Kubernetes cluster using Minikube

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700323471387/1b351317-1e90-4744-9703-0e0db691ff95.png align="center")

To verify that your Minikube cluster is running : `kubectl cluster-info`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700323804687/250c8c7d-74aa-4f53-9772-9b0f1cff39d4.png align="center")

Let's create a YAML file which will be used to create our pod

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700323987208/0b80ce87-0433-46c5-8dd3-98a0daa8aefc.png align="center")

To create a pod using this YAML file - `kubectl apply -f <yaml_filename>`

This command creates a pod named “nginx” and uses the official Nginx Docker image.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700324163088/15c14d7b-939a-49a9-99e0-f403e68def10.png align="center")

Verify that the Nginx pod is running by running the following commands:

`kubectl get pods`

`kubectl describe pod nginx`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700324490942/f13f20be-eb08-4e7c-844a-e7f634d66c75.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700324525833/0fa09f80-4211-490d-8a71-c7d7baf4b178.png align="center")