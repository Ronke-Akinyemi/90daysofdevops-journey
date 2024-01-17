---
title: "Your CI/CD pipeline on AWS - Part 4"
datePublished: Thu Dec 21 2023 16:02:50 GMT+0000 (Coordinated Universal Time)
cuid: clqfe5xhg000008l6etio419w
slug: your-cicd-pipeline-on-aws-part-4
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703174434289/73909426-36e4-4153-996e-4db417f7391c.png
tags: aws, codepipeline, 90daysofdevops

---

## What is CodePipeline ?

CodePipeline builds, tests, and deploys your code every time there is a code change, based on the release process models you define. Think of it as a CI/CD Pipeline service.

# Task-01 :

* **Create a Deployment group of Ec2 Instance.**
    

We already created an application and deployment group in the previous day, [Day 52](https://hashnode.com/post/clqez39en000e08jwdoq91y6o).

* **Create a CodePipeline that gets the code from CodeCommit, Builds the code using CodeBuild and deploys it to a Deployment Group.**
    

1. Access the AWS Management Console and navigate to the CodePipeline service.
    
    Click on "Create pipeline"
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703170778062/97f07b7d-1065-4b72-95d2-bf09f6f1d914.png align="center")
    
2. Choose a pipeline name and for Pipeline type, choose v2. Then for Service role, New service role.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703171070124/dfb857b3-897b-446c-9ee3-9b8e7ef2eed2.png align="center")
    
3. Add variables
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703171162760/7be32a3a-7501-491a-af9b-f9efd905541b.png align="center")
    
4. For source provider, choose AWS CodeCommit. Configure the CodeCommit repository and branch.For Change detection options, choose AWS CodePipeline
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703171347713/06eaadac-4854-4d2d-9846-d31419b69cb2.png align="center")
    
5. Add a build stage. Select AWS CodeBuild as the build provider and put your project name.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703171480249/fd9766fa-d7ee-4c3a-8382-a401c6d59491.png align="center")
    
6. Add a deploy stage: Select AWS CodeDeploy as the build provider and put your Application name.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703171526694/2f811459-acfd-4ebc-88af-5ef19c18a10d.png align="center")
    
7. Review all the details you provided and click on "Create pipeline"
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703171657928/6fe2c9ce-9982-45d6-ac37-b743f48c4ee5.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703171683715/b7ece29f-dd96-4914-a56f-e6fc4e1cba9e.png align="center")
    
8. Pipeline Execution: The pipeline will source for the code from the CodeCommit repository, build the code,
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703172627606/4b629fa2-7c64-4327-abf9-453a0821fb49.png align="center")
    
9. And deploy the code
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703172818990/cd7abfcc-7317-4115-a1b6-14b589de7bb8.png align="center")
    
10. You can now navigate to the EC2 public URL to check the webpage
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703172932305/f0cef73f-b5d9-4d56-a187-eec3736b31d5.png align="center")
    
    We've now set up a CodePipeline that automates the process of getting code from CodeCommit, building it using CodeBuild, and deploying it to an EC2 instance deployment group using CodeDeploy.
    

We will make some changes to our index.html file, push the changes to the CodeCommit repository and observe the pipeline automatically trigger the build.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703173248337/c4aad574-fe63-465f-9ef6-f2056ca30690.png align="center")

The pipeline is applying the changes

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703173372529/092c574f-4fda-406b-b7f6-b37997bf6057.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703173409148/2f38b08c-ee09-4e20-a0b1-8c78c2e6bb7a.png align="center")

Reload the browser and confirm that the changes have been applied successfully.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703173516914/05f61c3f-602c-42db-8ce2-fe7064e17c21.png align="center")

Thank you!