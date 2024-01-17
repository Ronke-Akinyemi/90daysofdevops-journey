---
title: "IAM Programmatic access and AWS CLI"
datePublished: Thu Dec 07 2023 19:58:27 GMT+0000 (Coordinated Universal Time)
cuid: clpvmeztn000507l5cy7u142b
slug: iam-programmatic-access-and-aws-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701978059934/eae9d567-bdea-4e61-a813-1e4165f03f28.png
tags: aws, devops, devops-journey, trainwithshubham

---

## IAM Programmatic access

**IAM (Identity and Access Management) programmatic access** refers to the ability to interact with AWS (Amazon Web Services) resources programmatically, typically using APIs (Application Programming Interfaces) or the AWS Command Line Interface (CLI) rather than through the AWS Management Console. When you enable programmatic access for an IAM user or role, you are giving that entity the ability to request AWS services and resources using code. This is particularly useful for automating tasks, managing resources, and integrating AWS services into custom applications or scripts.

## AWS CLI

The Amazon Web Services Command Line Interface (AWS CLI) is a powerful tool enabling users to interact directly with various AWS services from the command line. It provides a comprehensive set of commands to manage AWS resources, automate tasks, and integrate AWS functionalities into scripts and workflows.

The AWS CLI v2 offers several new features including improved installers, new configuration options such as AWS IAM Identity Center (successor to AWS SSO), and various interactive features.

## Task-01: Create AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY from AWS Console.

* Login to AWS Console: Navigate to the AWS Management Console
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701976653179/bf8fb09b-110e-4a8c-8b35-28f86c450945.png align="center")

* On the left side, click on "Users."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701976722210/a4b03aaa-e0ea-4adf-aa09-48cb9353358b.png align="center")

* Generate Access Key: Select a user from your list of users.
    
* Navigate to the "Security credentials" tab. Under "Access keys," click "Create access key." Choose "Command Line Interface (CLI)" as the use case.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701976821340/497f3b49-c206-44b1-a173-2288d6582b5f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701976891207/cfbadee8-dd7b-48cb-a01d-0d41f3af682d.png align="center")

* Note the Access key ID and Secret access key that are generated. You will need these for AWS CLI configuration.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701977109327/51524c18-7b52-4167-8db1-0192009b828d.png align="center")

## Task-02: Setup and install AWS CLI and configure your account credentials

* **Install AWS CLI:** Download and install the AWS CLI for your operating system. You can find the installation instructions [here](https://aws.amazon.com/cli/)
    
* **Configure AWS CLI:** Open a terminal or command prompt and run the following command:
    

```plaintext
aws configure
```

* Enter the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` from task 1 when prompted.
    
* Specify your preferred region (e.g., `us-east-1`) and default output format (e.g., JSON)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701977593852/1a2245e5-f010-4bda-8fde-ed18be9052f8.png align="center")

I've created AWS access keys, installed AWS CLI, and configured my account credentials. I can use AWS CLI commands to interact with my AWS resources.

Thank you!