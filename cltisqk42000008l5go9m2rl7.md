---
title: "Project 2"
datePublished: Fri Mar 08 2024 15:13:13 GMT+0000 (Coordinated Universal Time)
cuid: cltisqk42000008l5go9m2rl7
slug: project-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1709910601297/9a1f2956-d9b2-4151-bad2-416bba9d983e.png
tags: aws, devops, jenkins, 90daysofdevops

---

# Project Description

The project is about automating the deployment process of a web application using Jenkins and its declarative syntax. The pipeline includes stages like building, testing, and deploying to a staging environment. It also includes running acceptance tests and deploying to production if all tests pass.

### **Deploying web app using Jenkins CI/CD declarative pipeline.**

Steps involved

**Launch an EC2 Instance:** Go to the AWS EC2 Dashboard and launch an instance with the necessary configurations.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709904467039/417c61cd-f053-4356-9933-aff701d9e900.png align="center")

**Connect to Your Instance:**

Install Jenkins and Docker on the EC2 instance.

You can refer [here](https://hashnode.com/post/clsz0tbc0000009jvgy6b2sia)

### **Configure Jenkins for Your Project**

* On the Jenkins dashboard, click "New Item."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709905309915/83b77ede-00f8-4f16-94d2-331def00e195.png align="center")

* Enter a name for your project, select "Pipeline," and click OK.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709905220949/5c911dec-7547-4aa4-99fe-5366def99f6e.png align="center")

Provide a general description, click on "GitHub project" and insert your GitHub Project url.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709905727460/adb2be45-0a7a-4e7e-a966-d27b629a8d18.png align="center")

In the build trigger section select the GitHub webhook trigger option.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709906135984/187aec56-bcf5-4631-b794-e54c602d5a79.png align="center")

**Configure the Webhook in GitHub**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709910478265/1fd07554-eb26-4737-8eae-73ac9e316d2b.png align="center")

```basic

    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/Ronke-Akinyemi/node-todo-cicd.git", branch: "master"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t node-app-test-new"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker tag node-app-test-new ${env.dockerHubUser}/node-app-test-new:latest"
                    sh "docker push ${env.dockerHubUser}/node-app-test-new:latest" 
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
```

In the "Script Path" field, enter the path to your pipeline script.

Click "Save" at the bottom of the page.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709907546422/a96daac2-2843-498d-aa0c-9f3335ae6479.png align="center")

* Click "Build Now" to run your pipeline.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709907700896/61bf0a29-4a92-4d86-966b-00dcb600a819.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709908349270/c9e4fe3c-1b4b-4ba6-87a6-66f413eaa60c.png align="center")

Console output

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709908699613/d25b3ccc-74e9-4ffd-b7ef-9b18143fd9e9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709908723274/d882fd6d-7314-4988-b419-13084181768f.png align="center")

Open port 8000 on the server to access the webpage.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709909369540/6b049564-eee2-4002-8f0f-9e9c2f8b34c4.png align="center")

Navigate to the web URL http://&lt;public url&gt;:8080

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709909736266/98790465-afa3-43f1-b7ad-8a02cb998fbc.png align="center")

Thank you for reading.