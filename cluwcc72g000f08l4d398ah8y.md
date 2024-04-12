---
title: "Automated Deployment of Portfolio App on AWS S3 using GitHub Actions"
datePublished: Fri Apr 12 2024 07:22:38 GMT+0000 (Coordinated Universal Time)
cuid: cluwcc72g000f08l4d398ah8y
slug: automated-deployment-of-portfolio-app-on-aws-s3-using-github-actions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1712905914272/0d33258b-8be9-4307-a17e-94135c6954c8.png
tags: aws, github, cloud-computing, devops, s3

---

# Project Description

This project involves automating the deployment of a Portfolio App on AWS S3 using GitHub Actions, which entails setting up a CI/CD pipeline that automatically builds and deploys your website every time you push new changes to your GitHub repository. This workflow enables efficient, consistent deployments and ensures that your portfolio is always up-to-date with the latest changes.

### **Step 1: Get a Portfolio application from GitHub**

Clone the [GitHub](https://github.com/Ronke-Akinyemi/tws-portfolio) repository to your local development environment or directly to your AWS server. In either case, we will configure AWS S3 and set up the GitHub Actions Workflow.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712843077810/e34f87c7-d6ae-4f05-a4f9-2e23fd268cb7.png align="center")

### **Step 2: Build the GitHub Actions Workflow**

"Navigate to the code repository on GitHub, then click on "Actions" followed by "New workflow" and select "Set up a workflow yourself". Create a main.yml workflow File.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712843606628/b0b4f7f0-fa34-4511-ace9-e7684ee5190f.png align="center")

```bash
name: Portfolio Deployment

on:
  push:
    branches:
    - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v1

    - name: Configure AWS Credentials
      uses: aws-actions/configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: us-east-1

    - name: Deploy static site to S3 bucket
      run: aws s3 sync . s3://90daysofdevops-day86 --delete
```

### **Step 3: Setup GitHub Secrets for AWS CLI**

Go to your GitHub repository, click on "Settings" &gt; "Secrets" &gt; "Actions", and add new secrets. E.g AWS\_S3\_BUCKET, AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712899260579/1410bf19-0c00-4cca-b58d-c53edec0e1d3.png align="center")

### **Step 4: Setup AWS S3 with Public Access and Static Website Hosting**

### **Create an S3 Bucket**

* Log in to the AWS Management Console and navigate to the S3 service.
    
* Click on “Create bucket”. Provide a unique bucket name.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712900113764/2b6bbdff-5413-4ee0-a872-075e022ff6b2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712900398737/e8692689-84dc-44a1-bc10-9f49b415d228.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712900431157/d1aa01dc-1642-47f9-ad8e-baf7a5bf8a52.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712900454032/6ec5f3cc-2b0c-4870-9494-9de9cc866891.png align="center")

Navigate to bucket properties and edit "Static website hosting".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712902349485/352e4b8a-d237-4911-8ce9-98633ea344fb.png align="center")

### **Set Bucket Permissions**

* In order to make the content publicly accessible, you need to modify the policy. Navigate to the Permission tab of your bucket, go to "Bucket policy" and click on "Edit"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712902870059/1957fb0e-6a5f-40e9-8ead-ea689238b821.png align="center")

### **Step 5: Update the Index.html File and Run the Workflow**

Make a new change in your app index.html file to trigger the GitHub Action workflow. Commit, add, and push the changes to your GitHub repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712904321845/8250e414-ed49-4de6-ae23-ede94968d525.png align="center")

### **Step 6: Execute the GitHub Actions Workflow**

Once the index.html file has been updated, the GitHub Actions workflow will automatically execute and deploy it to the AWS S3 bucket, rendering it publicly accessible.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712904299450/f297135a-99c7-4d41-922b-d3cbfdf5e5af.png align="center")

### **Step 7: Verify the Deployment**

Access the deployed application by navigating to the S3 bucket's Permissions &gt; Static website hosting, copy the URL, and open it in your browser.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712904720999/41103afb-89f0-49f0-9b64-5640bfceebbd.png align="center")

To see CI/CD at work, just make changes in your GitHub repository's main branch. The CI/CD pipeline will kick in automatically, updating your application with the new changes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712905128582/37036b37-dfd5-4ff5-882e-afd91bbb4471.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712905233369/1443cc72-9988-475c-ba80-87c27718ac28.png align="center")

You can also verify how the GitHub Actions workflow has transferred your portfolio app files into the S3 bucket as specified in the YAML file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712905760273/3af42dd8-bd50-430d-b8c9-8ff82cb2f184.png align="center")

Thank you for reading.