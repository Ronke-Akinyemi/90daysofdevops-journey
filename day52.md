---
title: "Your CI/CD pipeline on AWS - Part 3"
datePublished: Thu Dec 21 2023 09:00:51 GMT+0000 (Coordinated Universal Time)
cuid: clqez39en000e08jwdoq91y6o
slug: your-cicd-pipeline-on-aws-part-3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703148658758/10752a0a-d0d8-485c-a235-2c6429c79220.png
tags: aws, codedeploy, 90daysofdevops

---

## What is CodeDeploy?

AWS CodeDeploy is a deployment service that automates application deployments to Amazon EC2 instances, on-premises instances, serverless Lambda functions, or Amazon ECS services.

CodeDeploy can deploy application content that runs on a server and is stored in Amazon S3 buckets, GitHub repositories, or Bitbucket repositories. CodeDeploy can also deploy a serverless Lambda function. You do not need to make changes to your existing code before you can use CodeDeploy.

# Task-01 :

* Read about Appspec.yaml file for CodeDeploy.
    
* Deploy the index.html file on the EC2 machine using nginx
    
* you have to set up a CodeDeploy agent in order to deploy code on EC2.
    

An AppSpec file, often named **appspec.yaml**, is a YAML-formatted or JSON-formatted file that provides instructions to CodeDeploy on how to deploy an application revision. It's a crucial component of the deployment process, ensuring that your application's files, scripts, and other resources are copied to the correct locations and that any necessary actions are taken during the deployment lifecycle.

Example of an AppSpec file:

```bash
version: 0.0
os: linux
files:
  - source: /
    destination: /var/www/html/
hooks:
  BeforeInstall:
    - location: install_dependencies.sh
      timeout: 300
      runas: root
  AfterInstall:
    - location: change_permissions.sh
      timeout: 300
      runas: root
  ApplicationStart:
    - location: start_server.sh
      timeout: 300
      runas: root
  ApplicationStop:
    - location: stop_server.sh
      timeout: 300
      runas: root
```

* Deploy the index.html file on the EC2 machine using nginx
    

[Day 50](https://hashnode.com/post/clqb7yjcx000508lba74u1mr6) and [Day 51](https://hashnode.com/post/clqcvv9jc000308l73otucu9h) are all about CodeCommit and CodeBuild respectively.

When you use **CodeDeploy**, the first step you need to take is to create an **Application.**

In the AWS Management Console, go to CodeDeploy, then go to Applications and click on "Create application".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703134784671/b27ced73-1291-48f3-9e87-b5147897ab71.png align="center")

When you create an application, you will need to select which platform to deploy your code to.

Provide a name for your application and for the Compute platform, choose **EC2/On-premises,** then click on "Create application"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703134857670/2315949f-ffdd-473f-aaeb-625ff63ffc35.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703137033426/88cb4f9f-9456-4bae-8958-7477a5324f1a.png align="center")

Before we continue, we need to give access to deployment to access the AWS resource so we need to create an IAM role.

Go to the IAM service and create a role named "**code-deploy-service-role**" with the below permissions.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703137689775/f80a9e35-83a7-4388-8eae-31d7921de957.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703138573974/ffa9e68d-76b4-4195-9d17-c61ac66e4144.png align="center")

You will need to create an EC2 instance on which you want to deploy the **index.html** file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703137848624/a3ce9d28-a3fc-42d7-b482-8a30b948a967.png align="center")

Create a "deployment group". On EC2, a deployment group is just a group of servers you choose to deploy your code to. You can do this by adding individual EC2 instances through their AWS tag or tag groups.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703138109619/2f190a1b-1f33-4c72-85b3-87b414f51d4f.png align="center")

Provide a name for the "Deployment group name" option, and then for "Service role", provide the service role ARN from the role you created in the above step.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703138817570/04c3bdf3-1429-48d1-b5f0-3caf1f38f63d.png align="center")

For "Deployment type", choose "In-place", and in the "Environmental configuration", select "Amazon EC2 instances".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703139025431/b0cfaaff-59c8-4f07-9bac-121eaf618014.png align="center")

Now, click on "Create deployment group"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703139472066/10101cf6-58e6-41d8-bc1b-57e2febe94f2.png align="center")

A Deployment group is created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703139640651/2cdc94df-2a71-4a22-a82f-204388419aa1.png align="center")

* ### You have to set up a CodeDeploy agent in order to deploy code on EC2
    

The AWS CodeDeploy agent is a software package that runs on the target instances and enables CodeDeploy to deploy applications to those instances.

If you do not have the agent installed on your instance, your deployment will not work. The agent can be installed either with the AWS CLI or AWS System Manager.

The CodeDeploy agent can be installed on an Ubuntu server from [here](https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-ubuntu.html?source=post_page-----28e2b6b44c8b--------------------------------)

```bash
sudo apt update
sudo apt install ruby-full
sudo apt install wget
cd /home/ubuntu
wget https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703140984645/045fd69e-fb5d-472b-85d0-bc762e9ebb62.png align="center")

### **Add appspec.yaml file to CodeCommit Repository and complete the deployment process.**

Create an appspec.yaml file that will instruct CodeDeploy on how to deploy your code and the dependencies file for installing and starting nginx on the server.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703142099945/f9331fbe-a80c-458d-a6d0-f0e84ab747d6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703142124044/6a3449f5-28d8-414d-ad71-b0aa296ac96c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703142299632/0d87be2e-52c8-4fdc-9a13-7c43f2cc05e1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703142320788/cca990f5-b255-4051-b23e-4b942192b7cc.png align="center")

Push all the files to code commit using ‘git add’ and ‘git commit’ commands.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703143023780/12e5121d-ccea-4cd2-84e2-56bc39e8d67a.png align="center")

Then push to the repository with the "git push" command

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703143204911/7ee70cbc-a184-46f6-abca-f121621d6afb.png align="center")

Make some changes to the **buildspec.yml** file so that CodeBuild will build the appspec.yml file and transfer the artifact to the S3 bucket.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703143920919/7145cf6d-b36f-4a52-9c5d-ad312439f296.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703143806888/cddcba04-d3bf-48f0-a706-707d59501c92.png align="center")

All the files are present in the CodeCommit Repository

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703143553956/fddf06d6-2008-4ece-9722-340180f7a5d4.png align="center")

In Build Projects, go to "Edit" and choose "Artifacts"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703144429837/02bbf006-5ec1-46f3-8896-303262e8602a.png align="center")

In Artifacts, select "artifact type" as Amazon S3 and choose bucket name and for "Artifact packaging" choose Zip and then click on "Update artifacts".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703144488739/b270f726-e3ea-4582-a34b-36311efe0982.png align="center")

After updating artifacts, click on "Start build"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703144886893/f6aca535-8339-4bb0-99da-49bb848ecb37.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703144954018/d8329ed6-71e4-40ba-b65a-97f372190f91.png align="center")

After the build is successful, navigate to the S3 bucket and copy the S3 URL of your zip file. This will pull the code during CodeDeploy.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703145219307/4651fad6-1946-465d-8f4a-916943165ab4.png align="center")

Then create Deployment

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703145488132/fbc24a88-d672-459e-829a-83b873db9a1f.png align="center")

Deployment is created, but the event is in the pending state

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703145840988/7e928273-85d8-4200-913c-23cf00267a40.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703145870319/da484224-15e8-48aa-8e50-18afda134ef2.png align="center")

You need to create a role that will give access to the EC2 with all the necessary permissions.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703146310314/fcd459f6-bdb1-4a02-a8a7-67769b58bd27.png align="center")

Then, attach the created role to the EC2 instance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703146683176/3e567948-cfc8-43ed-9812-dd4a375cb031.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703146808762/28eeea6e-cc09-4652-bbfa-80e74b0dca22.png align="center")

After updating the IAM role, restart the CodeDeploy-agent in the EC2 instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703146947925/275ad0e6-ca39-4c9b-aff9-317c942e4f04.png align="center")

Deployment is now successful.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703147354534/f1a57c25-050d-4fe9-b0e5-1df5c37a5aa3.png align="center")

You can now go to the public instance ip to view the webpage

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703149174240/0b66458e-c703-4eb7-b635-a2bde55e89dd.png align="center")

Thank you!
