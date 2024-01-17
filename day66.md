---
title: "Day 66 - Terraform Hands-on Project - Build Your Own AWS Infrastructure with Ease using Infrastructure as Code (IaC)"
datePublished: Wed Jan 17 2024 12:21:24 GMT+0000 (Coordinated Universal Time)
cuid: clrhr55wv000608jv0q1i655t
slug: day-66-terraform-hands-on-project-build-your-own-aws-infrastructure-with-ease-using-infrastructure-as-code-iac
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705493863321/ca0ba745-ba46-43e7-9d33-9fe500b5f8aa.png
tags: aws, terraform, 90daysofdevops

---

Welcome back to your Terraform journey.

In the previous tasks, you have learned about the basics of Terraform, its configuration file, and creating an EC2 instance using Terraform. Today, we will explore more about Terraform and create multiple resources.

**Task 1:**

**Create a VPC (Virtual Private Cloud) with CIDR block 10.0.0.0/16**

Connect to our EC2 instance and add the following code to our Terraform configuration in main.tf file

```basic
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "main"
  }
}
```

Then our main.tf file will look like this:

```basic
terraform{
 required_providers {
        aws = {
        source = "hashicorp/aws"
        version = "~> 4.16"
                }
  }
        required_version = ">=1.2.0"
}

provider "aws" {
region = "us-east-1"
}

resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "main"
  }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705396994779/afdf3491-9dd4-4d56-91c0-1ff5a6027424.png align="center")

Run `terraform init` , `terraform plan` , and `terraform apply` to build the VPC

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705397186795/aab050a1-d871-4bce-8acc-9385d27e3430.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705397313770/d8985935-38d9-417b-9aa4-da2f82b5bd81.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705397374452/9db35ac9-355f-43aa-a25c-b6b0f4adb048.png align="center")

Verify the newly created VPC named 'main' in the AWS VPC Management Console.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705397993224/a6d769b1-81c3-4e27-aae8-abb5058cde50.png align="center")

**Task 2:**

Create a public subnet with CIDR block 10.0.1.0/24 in the above VPC.

* Add the following to your [**main.tf**](http://main.tf/) terraform configuration file
    

```basic
resource "aws_subnet" "public_subnet" {
  vpc_id      = aws_vpc.main.id
  cidr_block  = "10.0.1.0/24"
  tags = {
    Name = "Public Subnet"
  }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705397777047/a1f461bc-033a-4349-9bfc-868aa5c3de84.png align="center")

This code creates a public subnet resource named “public\_subnet” with the specified CIDR block

Run `terraform apply` to create the public subnet in your AWS account.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705398094741/e1a7ec61-b4ad-4b94-ab52-238009ea0b88.png align="center")

Go to VPC console and click on "subnets" to verify that the public subnet is created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705398256530/083b90c3-a8a0-4132-b080-a3a75ca62548.png align="center")

**Task 3:**

Create a private subnet with CIDR block 10.0.2.0/24 in the above VPC.

```basic
resource "aws_subnet" "private_subnet" {
  vpc_id     = aws_vpc.main.id
  cidr_block = "10.0.2.0/24"

tags = {
    Name = "Private Subnet"
  }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705398557050/b2d3d620-fe54-4f9f-83c8-ee4225b37a4b.png align="center")

Run `terraform apply` to build the VPC.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705398918887/87b930e1-f03a-403f-8457-d2dbd6c38ac4.png align="center")

Go to VPC console and click on "subnets" to verify that the private subnet is created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705398975413/169f0d60-3b75-4ced-b491-2510445d29e0.png align="center")

**Task 4:**

Create an Internet Gateway (IGW) and attach it to the VPC.

```basic
resource "aws_internet_gateway" "gw" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "igw"
  }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705399159508/e9e48aa0-61c4-4778-b4e7-64cbad49c6bd.png align="center")

Run `terraform apply` to create the VPC

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705399369460/7fffd8fb-781d-47f6-867d-20a6e2c38687.png align="center")

Go to VPC console and click on "internet gateways" to verify that the internet gateway is created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705399443062/29acc4a3-0a75-4e4e-9126-76a92239e14e.png align="center")

Task 5:

Create a route table for the public subnet and associate it with the public subnet. This route table should have a route to the Internet Gateway.

```basic
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block  = "0.0.0.0/0"
    gateway_id  = aws_internet_gateway.gw.id
  }

  tags = {
    Name = "route-table"
  }
}

resource "aws_route_table_association" "public" {
  subnet_id      = aws_subnet.public_subnet.id
  route_table_id = aws_route_table.public.id
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705399636817/429fd296-a5d5-47f9-bbe8-df4264b84a43.png align="center")

First create a route table for public subnet.

**aws\_route\_table** block creates a new route table in the VPC specified by vpc\_id attribute. It also defines a route that sends all traffic with destination CIDR 0.0.0.0/0 to the internet gateway specified by gateway\_id attribute. The tags attribute sets a name for the route table for easy identification.

**Then associate route table with public subnet.**

**aws\_route\_table\_association** block associates the newly created route table with a public subnet specified by the subnet\_id attribute. The route\_table\_id attribute refers to the ID of the route table created in the previous block.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705399736657/4967af4f-ac5c-4a41-9d0b-76f2794ac4e8.png align="center")

Run `terraform apply` to create the route table.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705399828491/bf3264ee-6ca4-4458-973a-225ad2df2038.png align="center")

The route table is successfully created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705399929557/1e513321-8977-4644-9e32-78aa1e06cbfc.png align="center")

Route table is associated with public subnet using terraform.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705400088719/7da945b4-8a0e-4dec-9509-e26135a1158b.png align="center")

**Task 6:**

Launch an EC2 instance in the public subnet with the following details:

* AMI
    
* Instance type: t2.micro
    

**aws\_instance block** creates a new EC2 instance in the public subnet specified by subnet\_id attribute. It uses the Amazon Machine Image (AMI) ID ami-0c7217cdde317cfec, which is a Ubuntu 22.04.3 LTS image. The key\_name attribute specifies the name of the key pair used to SSH into the instance. The vpc\_security\_group\_ids attribute specifies a list of security groups to attach to the instance, in this case, it refers to the ID of the security group created in the next block.

```basic
resource "aws_instance" "web_server" {
 ami = "ami-0c7217cdde317cfec"
 instance_type = "t2.micro"
 subnet_id = aws_subnet.public_subnet.id
 vpc_security_group_ids = [aws_security_group.ssh_access.id]
```

Security group: Allow SSH access from anywhere

**aws\_security\_group block** creates a new security group that allows inbound traffic on ports 22 (SSH) and 80 (HTTP) from any source (0.0.0.0/0). The name\_prefix attribute sets a name prefix for the security group, and the vpc\_id attribute specifies the ID of the VPC where the security group will be created.

```basic
resource "aws_security_group" "ssh_access" {
   name_prefix = "ssh_access"
   vpc_id = aws_vpc.main.id
   ingress {
     from_port   = 80
     to_port     = 80
     protocol    = "tcp"
     cidr_blocks = ["0.0.0.0/0"]
   }
   ingress {
     from_port   = 22
     to_port     = 22
     protocol    = "tcp"
     cidr_blocks = ["0.0.0.0/0"]
 }
   egress {
     from_port   = 0
     to_port     = 0
     protocol    = -1
     cidr_blocks = ["0.0.0.0/0"]
 }
 }
```

**Task 7:**

**User data: Use a shell script to install Apache and host a simple website**

The **user\_data attribute** specifies the script to run when the instance is launched. This script updates the package manager, installs Apache web server, creates a basic HTML file, and restarts Apache.

```basic
user_data = <<-EOF
    #!/bin/bash

    # Update the package list
    sudo apt update

    # Install Apache
    sudo apt install -y apache2
    sudo cat <<HTML > /var/www/html/index.html
    <!DOCTYPE html>
    <html><body><h1>Welcome to my website</h1></body></html>
    HTML

    sudo systemctl restart apache2
  EOF
```

**Task 9:**

Create an Elastic IP and associate it with the EC2 instance.

**aws\_eip block** creates a new Elastic IP address and associates it with the instance created in the first block by specifying the instance ID in the instance attribute. The tags attribute sets a name for the Elastic IP for easy identification.

```basic
resource "aws_eip" "eip" {
   instance = aws_instance.web_server.id
   vpc      = true
   tags = {
     Name = "elastic-ip"
   }
```

**Task 10:**

Combine all the configurations to spin up the EC2 instance

* Launch an EC2 instance in the public subnet with the following details:
    
* AMI: ami-0c7217cdde317cfec
    
* Instance type: t2.micro
    
* Security group: Allow SSH access from anywhere
    
* User data: Use a shell script to install Apache and host a simple website
    
* Create an Elastic IP and associate it with the EC2 instance.
    

```basic
resource "aws_security_group" "ssh_access" {
   name_prefix = "web-server-sg"
   vpc_id = aws_vpc.main.id
   ingress {
     from_port   = 80
     to_port     = 80
     protocol    = "tcp"
     cidr_blocks = ["0.0.0.0/0"]
   }
   ingress {
     from_port   = 22
     to_port     = 22
     protocol    = "tcp"
     cidr_blocks = ["0.0.0.0/0"]
 }
 egress {
     from_port   = 0
     to_port     = 0
     protocol    = -1
     cidr_blocks = ["0.0.0.0/0"]
 }
 }

resource "aws_instance" "web_server" {
  ami                    = "ami-0c7217cdde317cfec"
  instance_type          = "t2.micro"
  subnet_id              = aws_subnet.public_subnet.id
  vpc_security_group_ids = [aws_security_group.ssh_access.id]

  user_data = <<-EOF
    #!/bin/bash

    # Update the package list
    sudo apt update

    # Install Apache
    sudo apt install -y apache2
    sudo cat <<HTML > /var/www/html/index.html
    <!DOCTYPE html>
    <html><body><h1>Welcome to my website</h1></body></html>
    HTML

    sudo systemctl restart apache2
  EOF

  tags = {
    Name = "terraform-instance"
  }
}

resource "aws_eip" "ip" {
  instance = aws_instance.web_server.id
  vpc      = true
  tags     = {
    Name = "elastic-ip"
  }
}
```

Run `terraform apply`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705401216871/a1ce2ca3-7d46-4dcd-ad57-432dbd58a511.png align="center")

We can now view the new EC2 instance (terraform-instance) in the AWS console.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705401383322/d6884680-8039-4ca6-9a42-2fc4d035c726.png align="center")

**Open the website URL in a browser to verify that the website is hosted successfully.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705493353825/9a78ce99-349a-46fc-b216-d8c2e712403e.png align="center")

Thank you...
