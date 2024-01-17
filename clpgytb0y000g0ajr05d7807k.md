---
title: "Mastering ConfigMaps and Secrets in Kubernetes"
datePublished: Mon Nov 27 2023 13:48:57 GMT+0000 (Coordinated Universal Time)
cuid: clpgytb0y000g0ajr05d7807k
slug: mastering-configmaps-and-secrets-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701092478475/670c16bc-68ba-44ac-8d8a-4aa882c5f041.png
tags: kubernetes, devops, devops-articles, trainwithshubham, devopscommunity

---

## What are ConfigMaps and Secrets in Kubernetes?

In Kubernetes, ConfigMaps and Secrets help separate configuration settings and sensitive information from your application code. This separation makes it simpler to handle and update configurations without having to modify the actual application.

### **ConfigMaps**

ConfigMaps are used to store non-sensitive data like environment variables. ConFigMaps are used to store configuration data in key-value pairs that can be consumed by containerized applications running in a Kubernetes cluster. ConfigMaps can store plain text, key-value pairs, or entire configuration files as data. ConfigMaps are often used to store environment variables, configuration files, or any configuration-related data that applications need during runtime. You can mount ConfigMaps as volumes in your containers, inject them as environment variables, or use them in other ways depending on your application's needs.

### **Secrets**

Secrets are similar to ConfigMaps but are specifically designed for sensitive information, such as passwords, API keys, or other confidential data. Secrets can store sensitive data in various formats, including plain text, base64-encoded, or even as files. Secrets keep confidential information secure and separate from the application code and configuration.

## Task 1:

* **Create a ConfigMap for your Deployment**
    
* **Create a ConfigMap for your Deployment using a file or the command line**
    

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: todo-app-config
data:
  name: django-todo-app
  application: todo-app
  protocol: TCP
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701083576235/beccda55-c1b4-4545-abfe-583a9dacca90.png align="center")

* **Apply the changes using the below command:**
    

```plaintext
kubectl apply -f configMap.yml
```

* **Update the deployment.yml file to include the ConfigMap**
    

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: config-todo-app
  namespace: my-todo-app  
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
        image: trainwithshubham/django-todo:latest
        ports:
        - containerPort: 8000
        env:
        - name: TODO_APP
          valueFrom:
            configMapKeyRef:
              name: todo-app-config
              key: application
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701084316939/0d7d6775-86b7-4cab-8971-971047e1698b.png align="center")

* **Apply the updated deployment using the command:**
    

```plaintext
kubectl apply -f deployment.yml -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701084879850/b7c6dd4c-07f7-4c6a-9502-2311a1dfa683.png align="center")

* **Verify that the ConfigMap has been created by checking the status of the ConfigMaps in your Namespace.**
    

Check the status of the deployment and ConfigMap by running the following command:

```plaintext
kubectl get configmaps -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701085282572/42d29275-ca06-4f7d-a346-036fb585b085.png align="center")

Use the **describe** command to get a detailed view of the ConfigMap

```plaintext
kubectl describe configmap <configmap-name> -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701085398251/532fcdd8-7c03-48b1-980c-b7467549649d.png align="center")

**To display the pods:**

```plaintext
kubectl get pod -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701085980693/9dd97836-4d97-4d82-8392-651765b5b7da.png align="center")

**Navigate inside one of the Pods and check the environment variable and the application for detailed status.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701086206506/c4d004a6-dc8e-4b6e-9079-f732d9e30ef4.png align="center")

## Task 2:

* **Create a Secret for your Deployment**
    
* **Create a Secret for your Deployment using a file or the command line**
    

```yaml
apiVersion: v1
  kind: Secret
  metadata:
    name: todo-app-secret
    namespace: my-todo-app
  type: Opaque
  data:
    username: <base64-encoded-username>
    password: <base64-encoded-password>
```

You can create your **username** and **password** if you don't have them already

Open a terminal and run the following commands to generate base64-encoded values:

```plaintext
echo -n "your_username" | base64
echo -n "your_password" | base64
```

Replace "your\_username" and "your\_password" with the desired values. The output of each command is the base64-encoded representation.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701087458756/0b05cd42-c65b-4b85-b4b8-86b701858c46.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701087700036/4aee1037-7ee1-4485-99c2-f3ddf6fa66bf.png align="center")

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: todo-app-secret
  namespace: my-todo-app
type: Opaque
data:
  username: cm9ua2U=  # base64-encoded "ronke"
  password: cGFzc3dvcmQ=  # base64-encoded "password"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701087848524/865679aa-f772-4bfa-a911-108778e4b6a8.png align="center")

* **Apply the changes using the below command:**
    

```plaintext
kubectl apply -f secret.yaml -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701088278204/5968e55d-c39a-4ca5-b415-88223c99d748.png align="center")

* **Update the** `deployment.yml` **file to include the Secret**
    

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: config-todo-app
  namespace: my-todo-app
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
        image: trainwithshubham/django-todo:latest
        ports:
        - containerPort: 8000
        env:
        - name: env_secret
          valueFrom:
            secretKeyRef:
              name: todo-app-secret
              key: password
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701088603614/9456d179-91fc-45c5-ba3e-ffa6535c2600.png align="center")

* **Apply the updated** `deployment.yml` **by running the below command:**
    

```plaintext
kubectl apply -f deployment.yml -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701089292749/daf66cae-ddad-4bd9-9a17-1a837beef181.png align="center")

* **Verify that the Secret has been created by checking the status of the Secrets in your Namespace.**
    

```plaintext
kubectl get secret -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701089707063/30ecbdf9-6ea7-4fec-9b29-555ebeeab3c4.png align="center")

The describe command is used to get a detailed view of a Secret:

```plaintext
kubectl describe secret <secret-name> -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701089963425/c2f85f2c-c5cb-48a9-a83a-75d7297fb8b6.png align="center")

**To display the pods:**

```plaintext
kubectl get pod -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701090511425/55e69b15-a596-40f5-a4cc-d0cff71a9623.png align="center")

**Navigate inside one of the Pods and check the environment variable**

```plaintext
kubectl exec -it <pod-name> -n <namespace-name> -- sh
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701090657739/7649e686-af78-4bb4-a299-25cd49b570ea.png align="center")

Thank you!