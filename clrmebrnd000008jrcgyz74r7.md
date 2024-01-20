---
title: "Meta-Arguments in Terraform"
datePublished: Sat Jan 20 2024 18:21:28 GMT+0000 (Coordinated Universal Time)
cuid: clrmebrnd000008jrcgyz74r7
slug: meta-arguments-in-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705774673322/e995ec55-06dc-4e78-88d7-adef86ecc24b.png
tags: aws, terraform, 90daysofdevops

---

When you define a resource block in Terraform, by default, this specifies one resource that will be created. To manage several of the same resources, you can use either **count** or **for\_each**, which removes the need to write a separate block of code for each one. Using these options reduces overhead and makes your code neater.

Count is what is known as a ‘meta-argument’ defined by the Terraform language. Meta-arguments help achieve certain requirements within the resource block.

In Terraform, **meta-arguments** are special arguments that add another layer of configuration, allowing you to define dependencies, manage resource count, and customize behavior beyond the standard resource-specific options. Meta-arguments influence the overall configuration or resource behavior. They are applied outside the resource block itself, often using a specific syntax like meta = { ... }.

## **Commonly used meta-arguments**

1. The "count" meta-argument allows you to create a fixed number of resource instances based on an integer value. The "count" meta-argument is useful when you need a specific number of identical resource instances and don't require the flexibility of for\_each.
    
2. The "for\_each" meta-arguments creates multiple instances of a resource or module based on a collection of values (a set or map). It makes sure each resource is unique and can be managed on its own.
    
3. The depends\_on meta-argument is used to explicitly define dependencies between resources, ensuring the order in which they are created or updated. The primary purpose of depends\_on is to specify that a particular resource depends on the completion of another resource. It is especially useful when creating resources where the order of resource creation matters, and certain resources need to be in place before others can be successfully created or updated.
    
4. The "provider" meta-argument is used in Terraform configurations to specify the provider(AWS, Google Cloud, Azure, and many others) that should be used to manage a particular set of resources.
    

Using meta-arguments in Terraform helps you write code that's easy to understand, saves time by reusing code, and makes your infrastructure flexible and adaptable to various scenarios.

### Count

The count meta-argument accepts a whole number and creates the number of instances of the resource specified. When each instance is created, it has its own distinct infrastructure object associated with it, so each can be managed separately. When the configuration is applied, each object can be created, destroyed, or updated as appropriate.

Example:

```basic
terraform {
required_providers {
aws = {
source = "hashicorp/aws"
version = "~> 4.16"
}
}
required_version = ">= 1.2.0"
}

provider "aws" {
region = "us-east-1"
}

resource "aws_instance" "server" {
count = 4

ami = "ami-0c7217cdde317cfec"
instance_type = "t2.micro"

tags = {
Name = "Server ${count.index}"
}
}
```

### for\_each

Like the count argument, the for\_each meta-argument creates multiple instances of a module or resource block. However, instead of specifying the number of resources, the for\_each meta-argument accepts a map or a set of strings. This is useful when multiple resources are required that have different values. Consider our Active directory groups example, with each group requiring a different owner.

```basic

terraform {

required_providers {

aws = {

source = "hashicorp/aws"

version = "~> 4.16"

}

}

required_version = ">= 1.2.0"

}



provider "aws" {

region = "us-east-1"

}



locals {

ami_ids = toset([

"ami-0b0dcb5067f052a63",

"ami-08c40ec9ead489470",

])

}



resource "aws_instance" "server" {

for_each = local.ami_ids



ami = each.key

instance_type = "t2.micro"

tags = {

Name = "Server ${each.key}"

}

}



Multiple key value iteration

locals {

ami_ids = {

"linux" :"ami-0b0dcb5067f052a63",

"ubuntu": "ami-08c40ec9ead489470",

}

}



resource "aws_instance" "server" {

for_each = local.ami_ids



ami = each.value

instance_type = "t2.micro"



tags = {

Name = "Server ${each.key}"

}

}
```

## Task

* Create the above Infrastructure as code and demonstrate the use of Count and for\_each.
    

The count meta-argument: Create a main.tf file with the following.

```basic
  terraform {
  required_providers {
  aws = {
  source = "hashicorp/aws"
  version = "~> 4.16"
  }
  }
  required_version = ">= 1.2.0"
  }
  provider "aws" {
  region = "us-east-1"
  }

  locals {
  ami_ids = toset([
  "ami-0c7217cdde317cfec",
  "ami-0e9107ed11be76fde",
  ])
  }

  resource "aws_instance" "server" {
  for_each = local.ami_ids
  ami = each.key
  instance_type = "t2.micro"
  tags = {
  Name = "Server ${each.key}"
  }
  }
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705764849665/a77efda8-665b-4523-8789-be5add8eb059.png align="center")

Run `terraform init` to initialize terraform

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705765051492/7f82ac6d-ec91-4626-9be8-e29b225c1620.png align="center")

Run `terraform plan`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705765120366/8259aad3-af92-4348-8099-877b6f7ec09b.png align="center")

Run `terraform apply` to create the 4 instances.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705765358623/c86b7808-a02f-4a78-9525-ed09532e15e2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705765375808/99ac3da4-10cb-4b25-94f9-7ef170834c3a.png align="center")

Navigate to the AWS EC2 console to verify the 4 newly created instances (server 0, server 1, server 2, server 3).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705765753992/cef1141e-e6ab-4275-a01b-5f4510ccdfc0.png align="center")

## for\_each

```basic
terraform {
required_providers {
aws = {
source  = "hashicorp/aws"
version = "~> 4.16"
}
}
required_version = ">= 1.2.0"
}

provider "aws" {
region = "us-east-1"
}

locals {
  ami_ids = toset({
  "ami-0e9107ed11be76fde",
  "ami-0c7217cdde317cfec",
  })
  }

  resource "aws_instance" "server" {
  for_each = local.ami_ids
  ami = each.value
  instance_type = "t2.micro"

  tags = {
  Name = "Server ${each.key}"
}
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705766400985/19131006-26d4-4890-b358-5184fe5a5fb3.png align="center")

Run `terraform apply` to create the 2 servers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705766466645/9a5f733a-0245-410b-aba3-ee0d3b92f5a4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705766493586/a84783ee-c25a-4543-8c3f-18f9f85289ad.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705766524787/25debb3d-3257-4cb3-8390-2874160950d6.png align="center")

Navigate to the AWS EC2 console to verify the 2 newly created instances.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705766662678/5a7e4497-b8ac-4a51-a152-e5af66501253.png align="center")

* **Multiple key value iteration**
    

```basic
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }
  required_version = ">= 1.2.0"
}

provider "aws" {
  region = "us-east-1"
}

#Multiple key value iteration

locals {
  ami_ids = {
    "linux"  = "ami-0e9107ed11be76fde",
    "ubuntu" = "ami-0c7217cdde317cfec",
  }
}

resource "aws_instance" "server" {
  for_each = local.ami_ids

  ami           = each.value
  instance_type = "t2.micro"

  tags = {
    Name = "Server ${each.key}"
  }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705767518707/c247ccf1-78bc-4aa5-a090-75e7dc57bc60.png align="center")

Run `terraform apply` to create the 2 instances that was just renamed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705767570458/9c9b7ca4-24d2-4a92-bcf6-2f4ee44d4b6b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705767589333/83e20fd4-fc0e-4388-a59b-e79d8873ed20.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705767615067/80b762a8-26d1-45e1-9e5b-05892d5714fe.png align="center")

Thank you.