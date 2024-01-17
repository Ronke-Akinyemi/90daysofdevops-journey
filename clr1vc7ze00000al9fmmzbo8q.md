---
title: "Terraform with AWS"
datePublished: Sat Jan 06 2024 09:34:33 GMT+0000 (Coordinated Universal Time)
cuid: clr1vc7ze00000al9fmmzbo8q
slug: terraform-with-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704520158903/26f915eb-3804-455e-a72c-9874a3d12815.png
tags: aws, terraform, 90daysofdevops

---

Provisioning on AWS is quite easy and straightforward with Terraform.

## Prerequisites

### AWS CLI installed

The AWS Command Line Interface (AWS CLI) is a unified tool to manage your AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts.

```basic
sudo apt-get update && sudo apt-get install -y awscli
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704522256647/085f99a4-329b-4251-9f3d-5327cead4c53.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704522273374/b62f7efa-b7b4-48b2-9969-a596518426be.png align="center")

### AWS IAM user

IAM (Identity Access Management) AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.

* Create an IAM user with suitable permissions and create Access key for the IAM user.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704525294053/d7d12061-9866-4aa7-b440-3191fce2c9a8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704525114086/0edf3186-c2d1-46e3-a729-6f01a56936a8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704525376708/bd24c820-6c94-41d1-a762-582a297907f7.png align="center")

*In order to connect your AWS account and Terraform, you need the access keys and secret access keys exported to your machine.*

```basic
export AWS_ACCESS_KEY_ID=<access key>
export AWS_SECRET_ACCESS_KEY=<secret access key>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704525648376/24631cfb-35a6-49bb-82bb-efd30c7a764e.png align="center")

### Install required providers

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
```

* Create a terraform file to download required providers on the system
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704526329533/8232323f-1924-415b-8065-65df91ac7987.png align="center")

* Add the region where you want your instances to be
    

```basic
provider "aws" {
region = "us-east-1"
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704526546772/f8a0a72d-d251-4a64-9f1e-9f96ce701fe8.png align="center")

## Task-01

* Provision an AWS EC2 instance using Terraform
    

```basic
resource "aws_instance" "aws_ec2_test" {
        count = 4
        ami = "ami-0c7217cdde317cfec"
        instance_type = "t2.micro"
        tags = {
     Name = "TerraformTestServerInstance"
  }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704530009562/a3f8ee67-a627-4d73-9097-81d1805cdf3e.png align="center")

Run `terraform init` after adding this configuration to initialize your Terraform environment and download the required provider.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704531006296/ebb4a348-eeee-4457-a1a4-fe8975283e10.png align="center")

**Run** `terraform plan` to preview the changes that Terraform will make to your infrastructure based on your configuration.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704531119569/f466f120-0e16-4c6c-9893-d487b85881bd.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704531251381/63f9f878-9edd-4490-92f5-923a4b5e920d.png align="center")

Run `terraform apply` to apply the changes

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704531424637/5ca1a8fd-0806-4abf-b37a-8973551b6936.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704533016211/54cec23f-e2bc-4c68-a126-5438d91f8092.png align="center")

Now, checking the console will reveal four created servers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704533285460/077d9dfb-8b56-4a1e-870c-bc0158c2a8bc.png align="center")

Thank you.