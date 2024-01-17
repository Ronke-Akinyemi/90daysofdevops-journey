---
title: "Your CI/CD pipeline on AWS - Part-1"
datePublished: Mon Dec 18 2023 17:58:03 GMT+0000 (Coordinated Universal Time)
cuid: clqb7yjcx000508lba74u1mr6
slug: your-cicd-pipeline-on-aws-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702919295625/0bef8767-bde4-46bb-bfc2-4fd2ec6dbf53.png
tags: aws, devops, codecommit, trainwithshubham

---

## What is CodeCommit?

CodeCommit is a managed source control service by AWS that allows users to store, manage, and version their source code and artifacts securely and at scale. It supports Git, integrates with other AWS services, enables collaboration through branch and merge workflows, and provides audit logs and compliance reports to meet regulatory requirements and track changes. Overall, CodeCommit provides developers with a reliable and efficient way to manage their codebase and set up a CI/CD pipeline for their software development projects.

# Task-01 :

* **Set up a code repository on CodeCommit and clone it on your local.**
    

Go to the AWS Management Console, open the CodeCommit console

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702912622457/0b3b8535-c37e-49ef-81cd-9314fb3b8371.png align="center")

Click "Create Repository" to create a new repository

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702912483364/c28b8563-e25b-4916-910c-260b732f4fed.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702919663019/4d855194-7411-4a1a-83f3-b493ea5a6f02.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702913882508/200d142c-21cb-4114-878c-d5581e1a1ce9.png align="center")

* **You need to set up GitCredentials in your AWS IAM.**
    

Go to the IAM console and create a new IAM user with programmatic access. Attach the `AWSCodeCommitFullAccess` and `AWSCodeCommitPowerUser` permissions to the user.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702913472898/6fa3f804-3cc5-4a2e-a779-542c4ccf8689.png align="center")

In the "**Security credentials**" tab, scroll down to the HTTPS Git credentials for AWS CodeCommit. Then, click Generate credentials to get a username and password, then note them down.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702915642603/1bd23e9c-33bf-42a5-a321-3031764e8da0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702915664423/badc46bc-c568-4b74-a1a7-fd0e2c7f5b6b.png align="center")

* **Use those credentials in your local and then clone the repository from CodeCommit.**
    

Go to the CodeCommit console and select your repository. Click on "Clone URL" to get the repository URL. Then, in the terminal, run:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702915865494/00afdb81-0a85-48de-8175-4b09deb64771.png align="center")

Then, in the terminal, run:

```bash
git clone <repository-url>
```

You will be prompted for your git credentials i.e your username and password.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702916730225/ef7c163d-cb84-4c0b-a203-090012063972.png align="center")

# Task-02 :

* Add a new file from local and commit to your local branch.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702917175935/21bd7dd7-2746-4bac-82b8-0dd179f39ae8.png align="center")

* Push the local changes to the CodeCommit repository.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702917310923/2cd95aa7-d2eb-40a5-8f85-5e4a968ec529.png align="center")

Let's verify our newly created file is in the repository

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702917459805/bd4519f0-a63b-41d9-b21c-736f02c7b343.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702917521631/c5d8f4bc-4b1b-43de-bef3-6b7996a0c4a9.png align="center")

Thank you
