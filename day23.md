---
title: "Jenkins Freestyle Project for DevOps Engineer"
datePublished: Wed Nov 08 2023 09:45:59 GMT+0000 (Coordinated Universal Time)
cuid: clopkrnkn000908jo7z1r5msc
slug: jenkins-freestyle-project-for-devops-engineer
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699391078568/57addf2a-2d39-4925-9e79-2db909f9388e.png
tags: devops, jenkins, 90daysofdevops, trainwithshubham

---

# What is CI/CD?

**Continuous Integration(CI)** is the practice of automating the integration of code changes from multiple developers into a single codebase. It is a software development practice where the developers commit their work frequently to the central code repository (Github or Stash). Then, there are automated tools that build the newly committed code and do a code review, etc, as required upon integration. The key goals of Continuous Integration are to find and address bugs quicker, make the process of integrating code across a team of developers easier, improve software quality and reduce the time it takes to release new feature updates.

**Continuous Delivery(CD)** is carried out after Continuous Integration to make sure that we can release new changes to our customers quickly in an error-free way. This includes running integration and regression tests in the staging area (similar to the production environment) so that the final release is not broken in production. It ensures to automate the release process so that we have a release-ready product at all times and we can deploy our application at any point in time.

## What is a Build Job?

A build job, in the context of continuous integration or continuous delivery (CI/CD), refers to a specific task or a set of tasks executed by an automation tool like Jenkins GitLab CI/CD. Its primary purpose is to automate the process of compiling, testing, and packaging software applications, among other things.

Build jobs are a fundamental part of the CI/CD pipeline, automating the process of converting source code into a usable form and allowing for continuous integration, testing, and delivery of software.  
Jenkins and other CI/CD tools provide mechanisms to define and execute these build jobs through a series of automated steps or scripts. They enable developers to trigger these jobs when source code changes are pushed to a repository, ensuring the application is continuously built and tested as the codebase evolves.

### What is a Freestyle Project?

A freestyle project in Jenkins is a type of project that allows you to build, test, and deploy software using a variety of different options and configurations.

### Task-1

* create an agent for your app. ( which you deployed from docker in the earlier task)
    
    **Step 1: Setting up a new node**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699430026229/b6e287c6-fcc6-4724-aa01-62bc351a65cf.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699430942901/c0abea90-6e52-4c8b-a98d-cc022cb85a6c.png align="center")
    
    **Step 2: Input the required details and save**
    
* Create a new Jenkins freestyle project for your app.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699431801193/805a0f67-11a8-4c52-9ad1-e2891d500e45.png align="center")
    
    **Step 1:** Enter the name you want for the freestyle project and click save
    
* In the "Build" section of the project, add a build step to run the "docker build" command to build the image for the container.
    
* Add a second step to run the "docker run" command to start a container using the image created in step 3.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699433252493/0a61aff1-03b4-4bc8-ace7-365d7bbc9ed3.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699433356780/d3baa922-9597-4f5c-8337-84b396772081.png align="center")
    
    ### Task-2
    
    * Create a Jenkins project to run `docker-compose up -d` command to start the multiple containers defined in the compose file (Hint- use day-19 Application & Database docker-compose file)
        
        Docker-compose file
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699433986085/a01d12c1-1a3d-4e74-89cc-36300a0a81b2.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699434366729/886cd477-f1d8-447a-b5dc-0a62a63b053d.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699434801533/97972c20-ed69-41ba-b8c4-cded5b715a4c.png align="center")
        
    * Set up a cleanup step in the Jenkins project to run `docker-compose down` command to stop and remove the containers defined in the compose file.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699434828842/2d3939ec-0362-4392-9150-b137bb91ccde.png align="center")
        
    
    I'm open to receiving any suggestions, feedback, or further insights regarding the topic discussed in this article. Please share your thoughts or ideas, as I'm always open to learning.
