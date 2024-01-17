---
title: "Jenkins Declarative Pipeline with Docker"
datePublished: Tue Nov 14 2023 19:16:42 GMT+0000 (Coordinated Universal Time)
cuid: cloypsqcx000208l9e08scuht
slug: jenkins-declarative-pipeline-with-docker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699989928673/1e04ca2c-3676-45c9-b837-3342c397a9fa.png
tags: docker, devops, jenkins, 90daysofdevops, trainwithshubham

---

Day 26 was all about a Declarative pipeline; now it's time to level up things; let's integrate Docker and our Jenkins declarative pipeline.

To integrate Docker and our Jenkins Declarative Pipeline, we will make use of our `docker build` and `docker run` knowledge.

**docker build -** you can use `sh 'docker build . -t <tag>'` in your pipeline stage block to run the docker build command. Make sure you have docker installed with the correct permissions.

**docker run:** you can use `sh 'docker run -d <image>'` in your pipeline stage block to build the container.

Here is an example of how the stage will look like:

```plaintext
stages {
        stage('Build') {
            steps {
                sh 'docker build -t trainwithshubham/django-app:latest'
            }
        }
    }
```

Task-1

* Create a docker-integrated Jenkins declarative pipeline
    
* Use the above-given syntax using `sh` inside the stage block
    
* You will face errors in case of running a job twice, as the docker container will be already created, so for that do task 2
    
    First, we sign in to the Jenkins dashboard where you will click on the "New Item", provide a name for your project, and click on "Pipeline", then "ok" to create a new Jenkins Pipeline.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699979714548/1875cb35-eaac-4767-9948-04741e5c8fc5.png align="center")
    

Then you will be directed to the configuration section where you will go to the pipeline section to write a pipeline script

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699980247164/7ab5f85c-f130-45b0-af20-ea91b2e56b7a.png align="center")

```bash
 pipeline {
     agent any
     stages {
         stage('Clone Code') {
             steps {
                 // Build steps go here
                 git url: 'https://github.com/Ronke-Akinyemi/node-todo-cicd.git', branch: 'master'
             }
         }
         stage("Build"){
             steps{
                 sh '/usr/local/bin/docker build . -t node-todo-cicd'
             }
         }
         stage("Run"){
             steps{
                 sh '/usr/local/bin/docker run -d -p 8001:8000 node-todo-cicd'
             }
         }

     }
 }
```

Click on "save". Then by the side click on "Build Now"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699982220147/06f821d6-8d8e-4d99-bb81-2c99cb2ddb94.png align="center")

The job was run successfully. Click on "Full stage view" and below is the stage view.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699982053188/175b531e-2313-4d77-9bae-9312261eb997.png align="center")

* You will face errors in case of running a job twice, as the docker container will be already created, so for that do task 2
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699982739559/ccbee56d-1d41-4117-b0a5-2950d87c4e4a.png align="center")

Task-2

* Create a docker-integrated Jenkins declarative pipeline using the `docker` groovy syntax inside the stage block.
    
* You won't face errors
    
* Complete your previous projects using this Declarative pipeline approach
    

Now, you can create a new job or make use of the existing one.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699985775758/db649738-3599-431b-9f97-a4d8f5900c97.png align="center")

Click on "Save" and click on build now

```bash
pipeline {
    agent any
    environment {
        PATH = "$PATH:/usr/local/bin"
    }
    stages {
        stage('Clone Code') {
            steps {
                git url: 'https://github.com/Ronke-Akinyemi/node-todo-cicd.git', branch: 'master'
            }
        }
        stage("Build") {
            steps {
                sh '/usr/local/bin/docker build . -t node-todo-cicd'
            }
        }
        stage("Deploy") {
            steps {
                sh '/usr/local/bin/docker-compose down && docker-compose up -d'
            }
        }
    }
}
```

When this pipeline is run, it won't encounter any error because included is a step that will shut down existing containers before creating new ones. We can now run the job multiple times.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699986152253/2e749254-81e2-4692-8830-82a2e9d0fbff.png align="center")

I'm open to receiving any suggestions, feedback, or further insights regarding the topic discussed in this article. Please share your thoughts or ideas, as I'm always open to learning. Thank you.