---
title: "Managing Persistent Volumes in Your Deployment"
datePublished: Tue Nov 28 2023 14:39:05 GMT+0000 (Coordinated Universal Time)
cuid: clpig1mhx000008l570gc04ix
slug: managing-persistent-volumes-in-your-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701180755703/ed5b4688-b2d5-4126-bf10-fe6b2eaf0cab.png
tags: kubernetes, devops, devops-journey, kubernetes-persistent-volumes

---

## What are Persistent Volumes in k8s?

In Kubernetes, a Persistent Volume (PV) is a piece of storage in the cluster that has been provisioned by an administrator. A Persistent Volume Claim (PVC) is a request for storage by a user. The PVC references the PV, and the PV is bound to a specific node. Read official documentation of [Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/).

### Task 1:

Add a Persistent Volume to your Deployment todo app.

* **Create a Persistent Volume using a file on your node.**
    

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-todo-app
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  hostPath:
    path: "/tmp/data"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701176103210/e7ca9f60-91e1-4aab-abc1-4c6a904b2c03.png align="center")

* **Apply the updates using the below command:**
    

```plaintext
kubectl apply -f pv.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701176476014/130c0aab-7bac-46f6-a884-1ac28681e2d5.png align="center")

* **Create a Persistent Volume Claim that references the Persistent Volume.**
    

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-todo-app
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701176697119/f24842cd-1ec5-407d-bfe2-35944d41e3db.png align="center")

* **Apply the updates using the below command:**
    

```plaintext
kubectl apply -f pvc.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701177974831/f7ba5a67-c920-4c75-ab92-4a51e4f74042.png align="center")

* **Update your deployment.yml file to include the Persistent Volume Claim. After Applying pv.yml, and pvc.yml your deployment file looks like this:**
    

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: todo-app-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: todo-app
  template:
    metadata:
      labels:
        app: todo-app
    spec:
      containers:
        - name: todo-app
          image: trainwithshubham/django-todo:latest
          ports:
            - containerPort: 8000
          volumeMounts:
            - name: todo-app-data
              mountPath: /app
      volumes:
        - name: todo-app-data
          persistentVolumeClaim:
            claimName: pvc-todo-app
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701178088032/6d8941b9-b4f8-492b-8d3e-704199a5627d.png align="center")

* **Apply the updated deployment using the command:**
    

```plaintext
kubectl apply -f deployment.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701177720210/d20761b3-954d-453a-94f6-5422fd7948f0.png align="center")

* **Verify that the Persistent Volume has been added to your Deployment by checking the status of the Pods and Persistent Volumes in your cluster. Use this commands** `kubectl get pods` **,** `kubectl get pv`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701178479104/922f401a-532a-40e2-b0a7-f1430bb4addf.png align="center")

### Task 2:

Accessing data in the Persistent Volume.

* **Connect to a Pod in your Deployment using the command:**
    

```plaintext
kubectl exec -it <pod_name> -- sh
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701179051439/e1f5f02b-8157-45bf-8146-c0230c94c023.png align="center")

* **Verify that you can access the data stored in the Persistent Volume from within the Pod.**
    

Now, let's confirm our ability to access stored data. We'll initiate the auto-scaling feature of the Kubernetes deployment by deleting the existing pod. Afterward, we'll connect to the newly created pod and verify whether the file we previously created in the initial pod is still present.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701179975904/5dfd26ac-3cb5-44c6-b67c-7733f883b4e3.png align="center")

Thank you!