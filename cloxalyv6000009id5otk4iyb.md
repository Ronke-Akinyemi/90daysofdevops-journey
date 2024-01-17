---
title: "Jenkins Declarative Pipeline"
datePublished: Mon Nov 13 2023 19:23:47 GMT+0000 (Coordinated Universal Time)
cuid: cloxalyv6000009id5otk4iyb
slug: jenkins-declarative-pipeline
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699903192161/64c478e3-dd02-424f-9af4-f52b709d2d3f.png
tags: devops, jenkins, learning-journey, 90daysofdevops

---

Jenkins Pipeline is a comprehensive set of plugins designed to facilitate the implementation and automation of continuous delivery and continuous integration (CI/CD) pipelines within Jenkins. A pipeline in Jenkins is a set of instructions for orchestrating software applications, building, testing, and deployment. It allows you to define the entire build process, from source code to deployment, as code in a script.

Jenkins Pipeline supports two main syntaxes for defining pipelines: Declarative and Scripted Pipeline.

1. **Declarative Pipeline:** Uses a structured, more human-readable syntax. Declarative pipelines define pipelines using a domain-specific language (DSL) with a predefined structure. This structure includes stages, steps, and other key elements that help define the Pipeline's flow. Declarative pipelines are typically written in a Jenkinsfile, a text file describing the entire build process. It is also easier to read and write, especially for simple use cases and standard build processes.
    
    Example of a Declarative Pipeline:
    
    ```plaintext
    pipeline {
        agent any
        stages {
            stage('Build') {
                steps {
                    //
                }
            }
            stage('Test') {
                steps {
                    //
                }
            }
            stage('Deploy') {
                steps {
                    //
                }
            }
        }
    }
    ```
    
2. **Scripted Pipeline:** Uses a more flexible, Groovy-based scripting syntax and allows for more complex and dynamic build processes using Groovy scripting. Scripted Pipeline is suitable for advanced use cases requiring fine-grained control and flexibility. It requires more scripting knowledge compared to the Declarative Pipeline.
    
    Example of a Scripted Pipeline:
    
    ```plaintext
    node {
        stage('Build') {
            // Code to build the project
        }
        stage('Test') {
            // Code to run tests
        }
        stage('Deploy') {
            // Code to deploy the application
        }
    }
    ```
    
    ### Task-01
    

* Create a New Job, this time select **Pipeline** instead of Freestyle Project.
    
* Follow the Official Jenkins [Hello world example](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
    
* Complete the example using the Declarative pipeline
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699898117428/4a29cf7b-6444-480b-9360-a15f3714a571.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699898370767/d2b12655-4f7b-429c-b0ff-10e4f2c5122a.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699898391840/6d89a435-8012-4755-9a68-7bfa63ef971d.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699898437028/948af2c2-2c17-4242-ac13-4c96405fde2b.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699898465398/72f51cf1-a6e3-4a34-afaa-820ff637f010.png align="center")
    
    Console Output:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699898561062/fd831ac5-431e-4fa1-aa42-24447d9015b2.png align="center")
    
    Now, to complete the example using a declarative pipeline
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699899592911/09009365-6350-4dd8-a73d-cb6f0d413bb5.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699900111989/cf30202d-46f2-43a5-a83d-aa228cc0bfc9.png align="center")
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699900138560/418a0cfb-1f25-4ce4-86cc-10205cb182b3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699900641520/eb45b092-32f2-4aa2-8318-ba929efa761c.png align="center")