---
title: "Your CI/CD pipeline on AWS-Part 2"
datePublished: Tue Dec 19 2023 21:55:07 GMT+0000 (Coordinated Universal Time)
cuid: clqcvv9jc000308l73otucu9h
slug: your-cicd-pipeline-on-aws-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703022605802/f3c378ba-baab-43ab-81fd-4db1c00f31c2.png
tags: aws, devops

---

## What is CodeBuild?

AWS CodeBuild is a fully managed build service in the cloud. CodeBuild compiles your source code, runs unit tests, and produces artifacts that are ready to deploy. CodeBuild eliminates the need to provision, manage, and scale your build servers.

# Task-01 :

* **Read about the Buildspec file for Codebuild.**
    

The `buildspec.yaml` file in AWS CodeBuild is used to define the build process for your project. It specifies the various phases of the build, including commands to install dependencies, build artifacts, and perform other tasks. The `buildspec.yaml` file is written in YAML format.

* **Create a simple index.html file in the CodeCommit Repository**
    
* **You have to build the index.html using nginx server**
    

Go to the AWS Management Console, open the CodeCommit console

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703017384618/6b42ec70-b7d0-4621-9a73-da131a5ecc49.png align="center")

Click "Create Repository" to create a new repository

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703017432211/8d8e554d-2d20-4d66-9267-d768e1815e26.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703017460407/2e6d814c-ef18-4126-b6c1-d050c89a9dc6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703017501791/3619d356-87fb-4886-a6f5-c0dce23ae8ce.png align="center")

**You need to set up GitCredentials in your AWS IAM.**

Go to the IAM console and select an IAM user with programmatic access.

In the "**Security credentials**" tab, scroll down to the HTTPS Git credentials for AWS CodeCommit. Then, click "**Generate credentials**" to get a username and password, then note them down.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703017657707/25606664-53f9-45a5-8b54-d4212eda920f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703017737460/90e31396-d0e4-459d-9d09-f724eb635bcf.png align="center")

**Use those credentials in your local and then clone the repository from CodeCommit.**

Go to the CodeCommit console and select your repository. Click on "Clone URL" to get the repository URL.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703017893064/fe5f2d4c-defc-49cb-80c8-ae8966b698c3.png align="center")

Then, in the terminal, run:

```bash
git clone <repository-url>
```

You will be prompted for your git credentials i.e. your username and password.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703017996150/1e028118-5180-4c45-8c94-4fbc93979e07.png align="center")

**Create a simple index.html file in the CodeCommit Repository**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703018185006/f3dbf88f-2b20-4f8a-89d1-29ea9132f259.png align="center")

With `git add` and `git commit` command, save the file and commit the changes made to the repository

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703018503081/e44333f2-8fb7-4084-a2a7-6674d6042257.png align="center")

Then push them to the `origin master` branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703018728577/44e87eb6-f883-4802-b5f1-b84340ea1cb5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703018860259/7f1a4173-dfed-4c8d-8591-503990639cd1.png align="center")

# Task-02 :

* Add `buildspec.yaml` file to the CodeCommit Repository and complete the build process.
    

Create a Buildspec file

```bash
version: 0.2

phases:
  install:
    commands:
      - echo Installing NGINX
      - sudo apt-get update
      - sudo apt-get install nginx -y
  build:
    commands:
      - echo build started on 'date'
      - cp index.html /var/www/html
  post_build:
    commands:
      - echo configuring NGINX
artifacts:
  files:
    - /var/www/html/index.html
```

With `git add` and `git commit` command, save the file and commit the changes made to the repository. Then push the changes to the repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703019166616/a48ba8b4-2cae-451d-af5c-b6f0bc9808a9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703019289959/472094b4-a502-4359-aad0-18c6ace7a638.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703019351732/cdcc8b01-b937-4f06-bab2-fbf419fcd164.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703019406217/da59d79d-fe4c-4eb5-89cb-e3e88a761577.png align="center")

**Create a CodeBuild Project:** Go to the AWS CodeBuild service, navigate to the "Codebuild" section and create a new build project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703019642973/f7977066-a3df-4a45-9d1d-b8a44dfd7db4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703019556967/20c4ca75-4f5c-40a8-9390-7e697cb7c6c5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703019787736/21ec5f66-99c6-422a-95dd-caca6db359a8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703019858175/0c3d98a8-5ea4-41a5-901e-5be9528ce090.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703019924825/09ff6aa9-76ff-4f79-971e-5f47dc3b6b01.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703020090542/9e9594d6-c6c9-4897-9430-77a512207833.png align="center")

Then, click on "Start build"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703020272488/fd460ad1-acee-4281-8b4b-71b8fec43bd9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703020344283/2210fc97-1957-415a-8520-8d39fda5cbed.png align="center")

Now, to include artifacts and store them in an S3 bucket as part of a CodeBuild project.

Create an S3 bucket.

Click on your project and in the "Edit" dropdown, choose "Artifacts"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703020578914/5bf97789-bbb1-4cf2-927c-5e42de7f08c0.png align="center")

Under Artifacts 1 - Primary, choose "Amazon S3" as the type and provide your bucket name. Click on "Update artifacts"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703020691133/77797d43-7d69-4ef5-87f3-78f2929afdcc.png align="center")

After updating the artifacts, start a new build

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703020917756/0e6c7cdb-54ff-42d6-8a92-17c123707381.png align="center")

In buildspec.yml file, the path of the file, which is /var/www/html/index.yml, is specified. You can verify if the S3 bucket has the folder and the index.html file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703021301025/a9407e86-35ff-4ebf-862e-7c0a2551fa07.png align="center")

Click on the "index.html" to see the properties of the file. Then click on "Open"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703021464062/7b1f526b-276a-4537-b805-823429be63b6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703021779836/77afe45d-b5e5-438c-ae98-9d8b00ab2eb2.png align="center")

Thank you