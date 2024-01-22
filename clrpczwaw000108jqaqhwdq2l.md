---
title: "Terraform Modules"
datePublished: Mon Jan 22 2024 20:07:33 GMT+0000 (Coordinated Universal Time)
cuid: clrpczwaw000108jqaqhwdq2l
slug: terraform-modules
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705951776287/b8804bee-58b8-4da1-acfe-47441bb844a1.png
tags: aws, terraform, 90daysofdevops

---

* Modules are containers for multiple resources that are used together. A module consists of a collection of .tf and/or .tf.json files kept together in a directory
    
* A module can call other modules, which lets you include the child module's resources into the configuration in a concise way.
    
* Modules can also be called multiple times, either within the same configuration or in separate configurations, allowing resource configurations to be packaged and re-used.
    

### Below is the format on how to use modules:

**Creating an AWS EC2 Instance Module**

```basic
# Creating a AWS EC2 Instance
resource "aws_instance" "server-instance" {
  # Define number of instance
  instance_count = var.number_of_instances

  # Instance Configuration
  ami                    = var.ami
  instance_type          = var.instance_type
  subnet_id              = var.subnet_id
  vpc_security_group_ids = var.security_group

  # Instance Tagsid
  tags = {
    Name = "${var.instance_name}"
  }
}
```

**Module for Variables**

```basic
# Server Module Variables
variable "number_of_instances" {
  description = "Number of Instances to Create"
  type        = number
  default     = 1
}

variable "instance_name" {
  description = "Instance Name"
}

variable "ami" {
  description = "AMI ID"
  default     = "ami-xxxx"
}

variable "instance_type" {
  description = "Instance Type"
}

variable "subnet_id" {
  description = "Subnet ID"
}

variable "security_group" {
  description = "Security Group"
  type        = list(any)
}
```

**Module for Output**

```basic
# Server Module Output
output "server_id" {
  description = "Server ID"
  value       = aws_instance.server-instance.id
}
```

### Different Modules in Terraform:

There are three main categories of modules in Terraform:

1. **Root Module:** The root module is the main module representing your whole infrastructure configuration and is responsible for initialising Terraform, configuring providers, defining core resources, and calling child modules. The root module is where you define the overall structure of your infrastructure.
    
2. **Child Module:**A child module is a self-contained unit of Terraform configuration focused on a specific set of resources or functions. Child modules can be called from the root module or other child modules, promoting modularity and reuse.
    
3. **Published Modules:** refers to modular units of infrastructure code that can be share, made publicly accessible, and are available for use by the Terraform community.
    

Differences between Root Module and Child Module

1. Root Module is the main module representing your whole infrastructure configuration while Child Module is a self-contained unit of Terraform configuration focused on a specific set of resources or functions.
    
2. Root Module is responsible for initializing Terraform while Child Module groups related resources and configuration together for easier management.
    
3. Root Module declares resources for the entire infrastructure while Child Module can declare and use resources and variables specific to its scope.
    
4. Root Module cannot access variables defined within child modules while Child Module can access variables defined in the parent module or other accessible child modules.
    
5. Root Module can be used as a standalone module in multiple configurations while Child Module is primarily used within the parent configuration, but can be reused in other configurations if desired.
    

### Is modules and Namespaces are same? Justify your answer for both Yes/No

No, Modules and Namespaces are not the same.

Modules represent actual infrastructure code, while namespaces provide a way to categorize and locate published modules.

Thank you.