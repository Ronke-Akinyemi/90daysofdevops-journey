---
title: "Scaling with Terraform"
datePublished: Mon Jan 22 2024 13:30:32 GMT+0000 (Coordinated Universal Time)
cuid: clroytbwo000309l857shh8di
slug: scaling-with-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705929870421/0455b25c-621f-4872-807a-c460e3138258.png
tags: aws, terraform, 90daysofdevops

---

Yesterday, we learned how to AWS S3 Bucket with Terraform. Today, we will see how to scale our infrastructure with Terraform.

## Understanding Scaling

Scaling is the process of adding or removing resources to match the changing demands of your application. As your application grows, you will need to add more resources to handle the increased load. And as the load decreases, you can remove the extra resources to save costs.

Terraform makes it easy to scale your infrastructure by providing a declarative way to define your resources. You can define the number of resources you need and Terraform will automatically create or destroy the resources as needed.

## Task 1: Create an Auto Scaling Group

Auto Scaling Groups are used to automatically add or remove EC2 instances based on the current demand.

* In your [main.tf](http://main.tf) file, add the following code to create an Auto Scaling Group:
    

```basic
resource "aws_launch_configuration" "web_server_as" {
  image_id        = "ami-0c7217cdde317cfec"
  instance_type  = "t2.micro"
  security_groups = [aws_security_group.web_server.name]

  user_data = <<-EOF
              #!/bin/bash
              echo "<html><body><h1>You're doing really Great</h1></body></html>" > index.html
              nohup python -m SimpleHTTPServer 80 &
              EOF
}

resource "aws_autoscaling_group" "web_server_asg" {
  name                 = "web-server-asg"
  launch_configuration = aws_launch_configuration.web_server_lc.name
  min_size             = 1
  max_size             = 3
  desired_capacity     = 2
  health_check_type    = "EC2"
  load_balancers       = [aws_elb.web_server_lb.name]
  vpc_zone_identifier  = [aws_subnet.public_subnet_1a.id, aws_subnet.public_subnet_1b.id]
}
```

Then your [**main.tf**](http://main.tf/) file will look like this:

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

resource "aws_subnet" "public_subnet" {
  vpc_id      = aws_vpc.main.id
  cidr_block  = "10.0.1.0/24"
  tags = {
    Name = "Public Subnet "
  }
}

resource "aws_subnet" "private_subnet" {
  vpc_id     = aws_vpc.main.id
  cidr_block = "10.0.2.0/24"

tags = {
    Name = "Private Subnet"
  }
}

resource "aws_internet_gateway" "gw" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "igw"
  }
}

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

resource "aws_launch_configuration" "web_server_as" {
  name_prefix     = "web-server-asg"
  image_id        = "ami-0c7217cdde317cfec"
  instance_type  = "t2.micro"
  security_groups = [aws_security_group" "ssh_access.id]

  user_data = <<-EOF
              #!/bin/bash
              echo "<html><body><h1>You're doing really Great</h1></body></html>" > index.html
              nohup python -m SimpleHTTPServer 80 &
              EOF
}

resource "aws_autoscaling_group" "web_server_asg" {
  name                 = "web-server-asg"
  launch_configuration = aws_launch_configuration.web_server_asg.name
  min_size             = 1
  max_size             = 3
  desired_capacity     = 2
  health_check_type    = "EC2"
  
  vpc_zone_identifier  = [aws_subnet.public_subnet.id]
}
```

Run `terraform apply` to create the Auto Scaling Group.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705929290589/ac14e18f-c72a-4e67-9e29-d7caff6b5462.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705929317121/d3854bd9-ba47-4f43-8a9c-d57dde9698b9.png align="center")

Navigate to the AWS management console to verify the auto-scaling group.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705929398231/62a2facc-4047-4e60-8885-bd2619e9c863.png align="center")

In the terraform configuration file, the desired capacity was set to 2, so we have 2 newly created instances.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705929551826/77069ba0-01c0-4e76-a059-73967871e98b.png align="center")

## Task 2: Test Scaling

* Go to the AWS Management Console and select the Auto Scaling Groups service.
    
* Select the Auto Scaling Group you just created and click on the "Edit" button.
    
* Increase the "Desired Capacity" to 3 and click on the "Save" button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705929604128/c00ec0a1-2053-4b20-8f4e-438f9465051a.png align="center")

* Wait a few minutes for the new instances to be launched.
    
* Go to the EC2 Instances service and verify that the new instances have been launched.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705929652133/08d6f11b-87dd-40e8-84de-93662457f2a2.png align="center")

* Decrease the "Desired Capacity" to 1 and wait a few minutes for the extra instances to be terminated.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705929691848/5bb3be83-e157-4a4c-b113-633a74a0626c.png align="center")

* Go to the EC2 Instances service and verify that the extra instances have been terminated.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705929731604/27e0944f-c386-4db7-a3fa-43ff122eccf5.png align="center")

Thank you.