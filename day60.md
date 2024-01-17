---
title: "Terraform"
datePublished: Sun Dec 31 2023 15:57:41 GMT+0000 (Coordinated Universal Time)
cuid: clqtodtp1000108kx38evbuw3
slug: terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703949599466/ee44ab30-c9ce-4224-87f4-1e573403f52a.png
tags: aws, terraform, 90daysofdevops

---

## What is Terraform?

Terraform is an infrastructure as code (IaC) tool that allows you to create, manage, and update infrastructure resources such as virtual machines, networks, and storage in a repeatable, scalable, and automated way.

## Task 1:

Install Terraform on your system

Launch an EC2 instance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703944322687/ed636fc4-d20c-4750-b88e-584ca1a286c5.png align="center")

Connect to your EC2 instance using SSH

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703944406815/dd87e4e3-f8fc-47fc-adf5-4d06c751b478.png align="center")

Refer to the official Terraform installation page at [https://www.terraform.io/downloads.html](https://www.terraform.io/downloads.html) for step-by-step guide on how to install Terraform on your specific operating system.

```basic
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703945735418/334318e9-1a12-4f79-b1ea-66fda2497729.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703945754344/014e359b-f5d4-464b-a87f-fe31e944063c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703945772151/a894ade8-658c-47c0-8e25-baaecbac19e1.png align="center")

Verify that Terraform is configured correctly by running this command:

```basic
terraform --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703945913457/3334ca47-2994-4ed2-99f3-23258c44a22d.png align="center")

## Task 2: Answer below questions

* **Why do we use terraform?**
    

We use Terraform to automate infrastructure provisioning, manage resources declaratively through version-controlled code, support multi-cloud environments, and ensure consistent deployments.

* **What is Infrastructure as Code (IaC)?**
    

Infrastructure as Code(IaC) is the practice of managing and provisioning IT infrastructure (virtual machines, networks, storage, etc.) through code rather than manual processes.

* **What is Resource?**
    

A "resource" refers to a declarative definition of a specific infrastructure component or service that you want to create or manage. Resources in Terraform can represent various entities such as virtual machines, networks, storage buckets, databases, and more. Each resource block in Terraform configuration defines a particular piece of infrastructure, and Terraform uses this information to create, update, or delete the corresponding resources in the target environment. with A "resource" in Terraform

* **What is Provider?**
    

In Terraform, a "provider" is a plugin that serves as an interface between Terraform and a specific infrastructure or service provider, such as AWS, Azure, Google Cloud, or others. The provider is responsible for understanding API interactions with the target platform and translating Terraform configurations into actions that provision, manage, or destroy resources in that environment. Users specify the provider they want to use in their Terraform configuration, and each provider has its own set of resource types that can be managed using Terraform.

* **What is State file in terraform? What’s the importance of it ?**
    

In Terraform, the "**state file**" is a critical component that keeps track of the current state of the managed infrastructure. The state file contains information about the resources Terraform manages, their current configurations, and any dependencies between them.The state file ensures consistency, reproducibility, and efficient operations across complex infrastructure deployments.

* **What is Desired and Current State?**
    

**Desired State**

The Desired State represents the intended configuration of your infrastructure as specified in your Terraform configuration files. It describes how you want your infrastructure to be configured, including the resources you want to create, their settings, and any dependencies or relationships between them.

**Current State**

The Current State represents the actual state of your deployed infrastructure, as tracked and recorded by Terraform in its state file (`terraform.tfstate`).
