---
title: "Getting Started with Jenkins"
datePublished: Mon Nov 06 2023 11:18:23 GMT+0000 (Coordinated Universal Time)
cuid: clomt6sbu000109jrb5a9a5wh
slug: getting-started-with-jenkins
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699391189963/51fd335b-fa29-436d-941d-6e28a21d4ffd.png
tags: jenkins, devops-journey, 90daysofdevops, trainwithshubham

---

# What is Jenkins?

Jenkins is a popular open-source tool for building, testing, and developing software. Jenkins functions as an essential tool in software development, providing Continuous Integration and Continuous Delivery (CI/CD) capabilities. It automates and streamlines the repetitive tasks within the software development process. This enables teams to maintain a smoother and more efficient software development lifecycle. Developers can set up Jenkins to monitor repositories for changes in the source code. When changes are detected, Jenkins can automatically initiate predefined tasks, such as compiling code, running tests, and deploying applications. Jenkins provides a web-based user interface for configuration and management, and it supports a vast array of plugins that extend its functionality. These plugins enable integration with various version control systems, build tools, testing frameworks, and deployment mechanisms, making Jenkins highly adaptable to different workflows and project requirements.

NOTE: I've installed Jenkins on my machine(as it was a part of previous tasks)

*We will be creating a very basic job that will throw some output. So, let us begin. Creating and running a job on Jenkins  is as follows:*

**Step 1:** Sign in to Jenkins

**Step 2:** Click on "New Item"

![Click on "New Item"](https://cdn.hashnode.com/res/hashnode/image/upload/v1699265184186/078f6c8c-827d-4130-9d58-3c3ed1905d1d.png align="center")

**Step 3:** You will have a page on which you have to give your name to your job and choose ‘Freestyle project’ as your project type

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699265202128/deb7cf19-8bdd-4d43-975d-22d120c3ed3a.png align="center")

**Step 4:** Now, we will give some description of our job and now, you have to provide which source code management tool you are using since here we are not using anyone so will choose the "**none**" option.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699268028400/51cab1eb-4669-4f48-a39b-96af82093dd7.png align="center")

**Step 5:** Scroll down to the “Build” section in the configuration section and add an “Execute shell” build step.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699267087683/e08c9ade-a92b-49a0-a9dc-db26904eabbf.png align="center")

**Step 6:** Type the command to print “Hello...this is my first Jenkins demo : $(date)”

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699267191775/f9d83919-e14b-46d3-a69e-c8c961fd342d.png align="center")

To create the project, click the “Save” button at the bottom of the screen.

**Step 7:** To launch the project after it has been built, click the “Build Now” option.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699268658195/7a2e376b-6b12-4b8e-a739-a4f311e5752c.png align="center")

**Step 8:** Check the console output and see whether your job has failed or been successful.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699267462004/681f3c04-ecd6-4774-9dcb-b5381aee3cef.png align="center")