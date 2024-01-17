---
title: "Working with Services in Kubernetes"
datePublished: Wed Nov 22 2023 22:46:04 GMT+0000 (Coordinated Universal Time)
cuid: clpacsrxk00040ala530idosm
slug: working-with-services-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700692973518/94e01ddf-bec2-4262-955c-6894cf2c1848.png
tags: kubernetes, devops-articles, devops-journey, 90daysofdevops, trainwithshubham

---

## What are Services in K8s?

In Kubernetes, Services are objects that provide stable network identities to Pods and abstract away the details of Pod IP addresses. Services allow Pods to receive traffic from other Pods, Services, and external clients.

### The commonly used Service types are:

### **ClusterIP:**

* This is the default service type.
    
* Exposes the Service on an internal IP within the cluster.
    
* The Service is only reachable from within the cluster.
    

**NodePort:**

* Exposes the Service on each Node's IP at a static port.
    
* A Service of the type NodePort is automatically created, which forwards to the selected pods.
    

**LoadBalancer:**

* Exposes the Service externally using a cloud provider's load balancer.
    
* The external load balancer will route traffic to the NodePorts.
    

**ExternalName:**

* Maps the Service to the contents of the externalName field (e.g., a DNS name).
    
* Allows Service resources to refer to external services by name.
    

## Task-1

* Create a Service for your todo-app Deployment from Day-32
    
* Create a Service definition for your todo-app Deployment in a YAML file.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700687489518/f9c52e9d-1ae2-4cd3-b4d5-ac75ce1b912d.png align="center")

To break down the YAML manifest:

```plaintext
apiVersion: v1
kind: Service
metadata:
  name: todo-service
  namespace: my-todo-app
```

* **apiVersion:** specifies the API version that the object uses
    
* **kind:** defines the type of Kubernetes resource. Here, it is a Service
    

```plaintext
spec:
  type: NodePort
  selector:
    app: todo
```

* **spec**: describes the desired state of the service
    
* **type:** specifies the type of Service. In this case, it is a NodePort service.
    
* **NodePort:** makes the service accessible on a static port on each node in the cluster. This allows external traffic to reach the service.
    
* **selector:** specifies a set of labels used t identify the pods that this service will forward traffic to. Here, it selects pods with the label **app:todo**
    

```plaintext
ports:
    - protocol: TCP
      port: 8000
      targetPort: 8000
      nodePort: 30100
```

* **ports:** specifies the ports that the service will use
    
* **protocol:** specifies the protocol to use, here it is **TCP**
    
* **port:** specifies the port to which the service will be exposed internally in the cluster
    
* **targetPort:** specifies the port to which traffic will be forwarded to the pods matching the selector
    
* **nodePort:** specifies the port on each node where the service will be accessible externally, here, it is set to **30100.**
    

Apply the Service definition to your k8s(minikube) cluster using the below command:

```plaintext
kubectl apply -f service.yml -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700688608206/f3118f26-cff3-4254-be69-20caf4f8d70e.png align="center")

To list Services in a Kubernetes cluster, use the `kubectl get svc` command. The **\-n** flag is used to specify the namespace where the Service is located.

```plaintext
kubectl get svc -n my-todo-app
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700688899013/58df153f-a7df-446d-94b1-9b62827f3ada.png align="center")

The `minikube service` command is the main command to interact with services in a minikube cluster. It is used to expose Kubernetes services outside of the cluster.

```plaintext
minikube service todo-service -n=my-todo-app --url
```

**todo-service:** is the name of the service you want to expose

**n-my-todo-app:** specifies the namespace in which the service is located, and

**\--url:** is used to print the URL(s) of the exposed service(s)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700689448684/0ce483ba-3b83-462a-9653-b7ac2d3306bc.png align="center")

When you run this command, Minikube will open the specified (todo-service) in your default browser, and the **\--url** option will print the URL that you can use to access the service.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700689724325/9304662e-367e-4a57-9fc2-02fa8f02c67a.png align="center")

## Task-2:

* Create a LoadBalancer Service for accessing the todo-app from outside the cluster
    
* Create a LoadBalancer Service definition for your todo-app Deployment in a YAML file.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700689820638/13ec5be4-9009-48b0-8e5f-8e3ec5ee71bb.png align="center")

Task-2 Service type: ClusterIP

* Apply the ClusterIP Service definition to your k8s(minikube) cluster using the below command.
    

```plaintext
kubectl apply -f service.yml -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700690039577/6875f62a-5f43-472d-8913-71640edff237.png align="center")

* Get the ClusterIP Service IP address:
    

```plaintext
kubectl get services -n <namespace>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700690141876/a96e87f4-9489-4aa0-8e70-ece94b5376c0.png align="center")

* Identify all the pods in the same namespace:
    

```plaintext
kubectl get pods -n <namespace>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700690239026/aa9bb50a-4571-4b51-8434-1ce779b01703.png align="center")

* Verify that the ClusterIP Service is working by accessing the todo-app from another Pod in the cluster in your Namespace.
    

**Exec** into the pod: i.e go inside the container

```plaintext
kubectl exec -it <pod-name> -n <namespace> -- sh
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700690583083/5d90b29a-9509-4b93-84d7-ffaf8f78ecd4.png align="center")

## Task-3:

* Create a LoadBalancer Service for accessing the todo-app from outside the cluster
    
* Create a LoadBalancer Service definition for your todo-app Deployment in a YAML file.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700690739505/516b6394-9641-4b82-8beb-1c9c6e5c8860.png align="center")

Task-3 Service type: LoadBalancer

* Apply the LoadBalancer Service definition to your K8s (minikube) cluster
    

```plaintext
kubectl apply -f service.yml -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700691213074/522309a2-a7a3-4e3d-9782-37551ec675e7.png align="center")

* Get the load balancer service:
    

```plaintext
kubectl get services -n <namespace>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700691397916/92ec3223-5edd-4f78-b78f-60d22ac36834.png align="center")

Get the LoadBalancer URL:

```plaintext
 minikube service list
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700692025222/5da2003b-3c29-4651-8f2c-e51afb253a08.png align="center")

* Verify that the LoadBalancer Service is working by accessing the todo-app from outside the cluster in your Namespace.
    

This command `minikube service todo-service -n my-todo-app` will open the Service in your web browser

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700692053521/a3ec0bd4-6569-4771-9c93-29dc8a094f33.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700692706240/38033602-1b4a-40f4-b312-bfcd34ae303f.png align="center")

Thank you!
