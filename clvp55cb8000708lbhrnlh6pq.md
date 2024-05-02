---
title: "Mounting AWS S3 Bucket on Amazon EC2 Linux Using S3FS"
datePublished: Thu May 02 2024 11:06:40 GMT+0000 (Coordinated Universal Time)
cuid: clvp55cb8000708lbhrnlh6pq
slug: mounting-aws-s3-bucket-on-amazon-ec2-linux-using-s3fs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1714647238013/54e5dc2a-f597-468a-a452-137a3984d60a.png
tags: ec2, aws, devops, s3

---

# Project Description

This hands-on project involves mounting an AWS S3 bucket onto an Amazon EC2 Linux instance using S3FS. This project provides a practical introduction to Amazon Web Services (AWS), specifically Amazon S3 (Simple Storage Service) and Amazon EC2 (Elastic Compute Cloud), as well as S3FS, a FUSE-based file system.

### **Step 1: Create a New IAM User**

First, log in to the AWS Management Console and navigate to the IAM service. Then, under "Users," click "Add user" and enter a username.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714640546579/27c311fe-b7ec-428e-a202-a5883fad8a98.png align="center")

### **Step 2: Attach Policies to the User**

During user creation, select "Attach Policies directly" and click on "Create Policy." Create a new policy with the settings mentioned below, focusing on S3-related actions:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714642369482/19ca61a3-f0f7-4672-91e1-462db4446e33.png align="center")

* **For Service, choose** S3
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714642563974/ce2456ee-bd0b-4b0b-9c56-981d8462be64.png align="center")

* **Under Actions Allowed :** Choose "ListAllMyBuckets", "ListBucket", "ListBucketVersions", "GetObject", "GetObjectVersion", "PutObject"
    
* **Under Resources:** Choose Specific. Then tick "Any" on Bucket and Object
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714641948884/9d3d14bb-73b7-4bae-9073-47459973ca18.png align="center")

### **Step 3: Review and Create**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714643362595/1865ec4a-a822-4c4a-82af-1e747d5f4e56.png align="center")

After creating the policy, give it a suitable name and proceed to create the IAM user, attaching the newly created policy to the user.

### **Step 4: Get Access Keys**

Once the user is created, go to "Security Credentials," and under "Access Keys," click on "Create Keys." Choose "Command Line Interface (CLI)" and get the Access Key and Secret Key.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714643900121/a842923d-3191-403a-916b-d95c50171eb5.png align="center")

### **Step 5: Launch an EC2 Instance**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714644088733/1bfa423e-8bb2-4581-a3e4-1446e803e580.png align="center")

### **Step 6: Install AWS CLI On the Instance**

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714644353565/cde574b4-7ecd-4f87-a886-becfc7768da2.png align="center")

### **Step 7: Install S3FS On the EC2 Instance**

```bash
sudo apt install s3fs -y
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714644698997/41c7e24b-96dd-4d60-a1f4-eaccefae750c.png align="center")

### **Step 8: Create a Folder and Add Files**

Create a folder named "bucket" at a location `/home/ubuntu` on the EC2 instance. Add 2–3 files to this folder.

```bash
mkdir bucket
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714644862982/84bdb4b0-ec64-4c8e-9eb3-cd326df0de2a.png align="center")

```bash
touch test1.txt test2.txt test3.txt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714644987420/7a65931b-993d-42f9-b354-dd4c1bbe203a.png align="center")

### **Step 9: Create S3 Bucket**

Go to the S3 dashboard and click on "Create bucket". Enter a name for your bucket.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714645336394/e4a28bff-5280-47a9-a97d-750c27302d8a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714645410159/bc6011ee-5ac4-4ed9-921a-da6a18984c58.png align="center")

### **Step 10: Configure AWS CLI**

On the EC2 instance, configure the AWS CLI by running the command `aws configure` and providing the Access Key and Secret Key obtained earlier.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714645693256/0fab1957-6c2a-4f7d-ba6c-5ef01d61f390.png align="center")

### **Step 11: Sync Files to S3 Bucket**

Run the below command to sync the files from the given location on the EC2 instance to the S3 bucket.

```bash
aws s3 sync /home/ubuntu/bucket s3://devopschallenge-day89-s3-bucket
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714646032850/f3e63a1c-53e7-4a7b-980d-75bf62378d7f.png align="center")

### **Step 12: Verify the Sync**

Go to your S3 bucker to confirm that all the files from the EC2 instance are successfully uploaded to the S3 bucket.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714646380706/d43277d8-812a-4e2c-9cb4-70cf6188626a.png align="center")

Thank you for reading.