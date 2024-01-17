---
title: "Working with Terraform Resources"
datePublished: Wed Jan 10 2024 08:28:22 GMT+0000 (Coordinated Universal Time)
cuid: clr7iqi70000009infa3zfm8c
slug: working-with-terraform-resources
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704874915264/d2ce6564-a2c9-4145-af0d-564b7c02aacb.png
tags: aws, terraform, 90daysofdevops

---

## Understanding Terraform Resources

A resource in Terraform represents a component of your infrastructure, such as a physical server, a virtual machine, a DNS record, or an S3 bucket. Resources have attributes that define their properties and behaviors, such as the size and location of a virtual machine or the domain name of a DNS record.

When you define a resource in Terraform, you specify the type of resource, a unique name for the resource, and the attributes that define the resource. Terraform uses the resource block to define resources in your Terraform configuration.

## Task 1: Create a security group

To allow traffic to the EC2 instance, you need to create a security group. Follow these steps:

In your main.tf file, add the following code to create a security group:

```basic
resource "aws_security_group" "web_server" {
  name_prefix = "web-server-sg"

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

* Run `terraform init` to initialize the Terraform project.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704872054260/62170190-9fec-404f-94b2-1ea21e902b35.png align="center")

* Run `terraform apply` to create the security group.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704872218875/1980fee7-5d48-45cd-b815-8f958611fe71.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704872336250/da01056f-d9eb-4931-b496-01591f961e7a.png align="center")

* Verify the newly created security group
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704872712626/87df5709-19e0-4a37-a2cc-f5470116b87f.png align="center")

## Task 2: Create an EC2 instance

* Now you can create an EC2 instance with Terraform. Follow these steps:
    
* In your main.tf file add the following code to create an EC2 instance:
    

```basic
resource "aws_instance" "web_server" {
  ami           = "ami-0c7217cdde317cfec"
  instance_type = "t2.micro"
  key_name      = "TerraformKeypair"
  security_groups = [
    aws_security_group.web_server.name
  ]
  user_data = <<-EOF
              #!/bin/bash
              echo "<html><body><h1>Welcome to my website!</h1></body></html>" > index.html
              nohup python3 -m http.server 80 &
              EOF
}
```

Note: Replace the ami and key\_name values with your own. You can find a list of available AMIs in the AWS documentation.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704873740900/525daa73-8b06-454f-a197-f6a90df1421c.png align="center")

Note: Python3 is used here

Run `terraform apply` to create the EC2 instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704874110348/01d398db-d881-4ddf-a5c2-fe884fbb1c0c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704874199033/b17c6e8b-9daf-42c0-9418-70fa9b77aa58.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704874371330/fdc8aef4-e00c-4909-8dff-36dc51b18931.png align="center")

## Task 3: Access your website

* Now that your EC2 instance is up and running, you can access the website you just hosted on it.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704874531366/a5c6a60e-d52e-49bf-8d31-7b0244514901.png align="center")

Open a web browser and navigate to the public IP address of your instance to view the webpage.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704874726963/f05b65e3-845d-44cd-aa8b-0d9846ee6ce1.png align="center")

Thank you.
