---
title: "Launching your Kubernetes Cluster with Deployment"
datePublished: Mon Nov 20 2023 19:44:12 GMT+0000 (Coordinated Universal Time)
cuid: clp7bf6yr000309jqfoed561e
slug: launching-your-kubernetes-cluster-with-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700509278415/23afa7df-3199-4467-a252-f1ff8a4deced.png
tags: kubernetes, devops, 90daysofdevops, trainwithshubham

---

## What is Deployment in Kubernetes?

Deployment is a resource object that manages creating and updating Pods, the basic deployment units in Kubernetes. Deployments provide a declarative way to describe how you want your application to run on a Kubernetes cluster. Deployment means that you don't have to manually manage your Pods' creation, scaling, or updating. Instead, you define the desired state of your application in a Deployment, and the Kubernetes controller will ensure that the actual state of your application matches the desired state.

### Some of the benefits of using Deployments in Kubernetes

* **Declarative updates:** Deployments provide a declarative way to update your application. You don't have to write complex scripts to update your application. Instead, you define the desired state of your application in a Deployment, and the Kubernetes controller will take care of the rest.
    
* **Self-healing:** Deployments are self-healing. If a Pod crash or is terminated, the Deployment controller will automatically create a new Pod to replace it.
    
* **Scaling applications:** Deployments can be used to scale applications up or down. This can be done in response to changes in traffic or load.
    
* **Rolling Updates and Rollbacks:** Deployments can be used to update existing applications that are running on a Kubernetes cluster. Kubernetes will gradually replace instances of the old version with the new one. If you encounter any problems with the latest version, you can effortlessly roll back to a prior version.
    

### Task: **Create one Deployment file to deploy a sample todo-app on K8s using the "Auto-healing" and "Auto-Scaling" feature**

* add a deployment.yml file
    

```plaintext
apiVersion: apps/v1
kind: Deployment
metadata:
  name: todo-app
  labels:
    app: todo
spec:
  replicas: 2
  selector:
    matchLabels:
      app: todo
  template:
    metadata:
      labels:
        app: todo
    spec:
      containers:
      - name: todo
        image: rishikeshops/todo-app
        ports:
        - containerPort: 3000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700506153707/21f4aa29-dc51-4016-8ea1-85b4cbe9b7da.png align="center")

Apply the deployment to your minikube cluster by running this command

```plaintext
kubectl apply -f deployment.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700506444026/65e06874-2f72-431e-ae8a-17ab2e59bc00.png align="center")

To get the status of the deployment

```plaintext
kubectl get deployments
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700506858277/f751e942-b10d-4abb-b482-6e9193e5da45.png align="center")

To list the Pods created by the deployment

```plaintext
kubectl get pods
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700507181816/ceee018d-4690-4475-a4aa-515ff64a2fe4.png align="center")

To see the self-healing feature of Deployment, let's delete a pod out of the two created pods.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700508591595/77b12f06-c23b-4e13-a81f-534448748444.png align="center")

We can see that a new pod was created.

That's it for the Day-32 task. Thank you.
