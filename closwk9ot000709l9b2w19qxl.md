---
title: "Day 24 Task: Complete Jenkins CI/CD Project"
datePublished: Fri Nov 10 2023 17:39:28 GMT+0000 (Coordinated Universal Time)
cuid: closwk9ot000709l9b2w19qxl
slug: day-24-task-complete-jenkins-cicd-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699640030686/acc02aed-45cc-4a13-b647-1eab9d0276e1.png
tags: github, continuous-integration, jenkins, 90daysofdevops, trainwithshubham

---

# **Setting up a CICD Pipeline for Node JS Application**

# Task-01

* Fork [this](https://github.com/LondheShubham153/node-todo-cicd.git) repository
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699629025594/17f4fed7-266c-472f-9686-bcdfe1968ed6.png align="center")

Now, to connect GitHub repository and Jenkins. Install GitHub Integration. Connecting a GitHub repository to Jenkins can be done in several ways, and whether you need SSH keys depends on the method you choose.

### **SSH Key Authentication:**

This method involves using SSH keys for authentication.

**Generate SSH Key:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699630189128/0f2b1c4c-940e-486e-90b8-200425ca52a7.png align="center")

**Add SSH Key to GitHub:** Copy the public key (`~/.ssh/id_rsa.pub` ) and add it to your GitHub account under "Settings" &gt; "SSH and GPG keys."

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699630469381/844b5476-793c-480f-85e0-f16ffbae7357.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699637763757/b7825d85-61d1-49b9-9cd6-cf1080752332.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699630809927/8f49817b-19d9-4ade-9c18-6d7a9de8d156.png align="center")

**Jenkins Credentials:** In Jenkins, create a new item and choose a free-style project.

Now, go to **Source code management**, and choose "Git" to configure GitHub to Jenkins. Provide a description and the GitHub URL where the code exists, and select the SSH key credential you created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699631999102/d5a97e2a-210e-4a22-9896-f7938e0727e9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699632121095/b1f7fcf0-8873-4ba2-bc21-6dcf6da00525.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699632150977/b950a48d-bc94-4f7e-919c-0da49c1f187e.png align="center")

Now, go to Build Steps and choose the execute shell build option.

Provide the docker commands to build an image from the docker file and build the container.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699633086235/d320f9ef-9d01-486a-a5e5-a365fb0434a2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699633578456/aca8ef66-395a-4a40-ae00-b9708e3ee941.png align="center")

Navigate to the URL

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699633868304/dbebc437-8922-4fe8-9ec3-71b502d7e64e.png align="center")

### GitHub Webhook

GitHub Webhook is a feature that allows GitHub to send HTTP POST requests to a specified URL when certain events occur in a repository. These events can include code pushes, pull requests, issues, releases, and more. Webhooks enable external services, such as Jenkins or CI/CD systems, to be notified automatically when changes or events happen in a GitHub repository.

### To set up a webhook in a GitHub repository:

1. In your GitHub repository, go to "Settings", navigate to "Webhook", and click on "Add Webhook"
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699636425291/d5de5217-b60f-4235-ab51-025b965730c1.png align="center")
    
2. Provide the Payload URL: Add the Jenkins URL to the field labelled "Payload URL", then add "/github-webhook" to the end of the URL.
    
3. Choose the events you want to trigger the webhook.
    
4. Add the webhook.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699637395631/4c7b7920-1e81-423f-a6c5-cd30073dcfc7.png align="center")
    

# Task-02

* In the Execute shell run the application using Docker compose
    
* You will have to make a Docker Compose file for this Project
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699634381263/a97dd102-de64-4e3b-90f3-76ea1d8b9a3c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699634734924/18491b32-4f5f-4927-bfa1-8ca670876a0c.png align="center")

* Run the project
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699635582852/b654c118-ff4a-44e5-abfe-26e3ce06b9cc.png align="center")

I'm open to receiving any suggestions, feedback, or further insights regarding the topic discussed in this article. Please share your thoughts or ideas, as I'm always open to learning.