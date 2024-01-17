---
title: "Terraform and Docker"
datePublished: Wed Jan 03 2024 11:40:20 GMT+0000 (Coordinated Universal Time)
cuid: clqxpiewi000a09idakaxe4z5
slug: terraform-and-docker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704281853666/e9710fcd-42c7-4a41-b9bb-7fbf82834b81.png
tags: docker, aws, terraform, 90daysofdevops

---

Terraform needs to be told which provider to be used in the automation, hence we need to give the provider name with source and version. For Docker, we can use this block of code in your [main.tf](http://main.tf)

## Blocks and Resources in Terraform

## Terraform block

## Task-01

* Create a Terraform script with Blocks and Resources
    

```basic
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 2.21.0"
}
}
}
```

Note: kreuzwerker/docker, is shorthand for [registry.terraform.io/kreuzwerker/docker](https://github.com/LondheShubham153/90DaysOfDevOps/blob/master/2023/day62/README.md#provider-block).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704276838633/16442a8a-8547-41e7-be97-f2abd0f5ba6c.png align="center")

## Provider Block

The provider block configures the specified provider, in this case, docker. A provider is a plugin that Terraform uses to create and manage your resources.

```basic
provider "docker" {}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704277345607/0064a596-8a06-4188-8e19-55baba042910.png align="center")

## Resource

Use resource blocks to define components of your infrastructure. A resource might be a physical or virtual component such as a Docker container, or it can be a logical resource such as a Heroku application.

Resource blocks have two strings before the block: the resource type and the resource name. In this example, the first resource type is docker\_image and the name is Nginx.

## Task-02

* Create a resource Block for an nginx docker image
    

```basic
resource "docker_image" "nginx" {
 name         = "nginx:latest"
 keep_locally = false
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704277397172/dc026ea6-0289-4a74-a8cc-9bb3dc993a7b.png align="center")

* Create a resource Block for running a docker container for nginx
    

```basic
resource "docker_container" "nginx" {
 image = docker_image.nginx.latest
 name  = "tutorial"
 ports {
   internal = 80
   external = 80
 }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704277576912/d4aa6621-50f0-4bf7-95e3-b06625c6977c.png align="center")

Note: In case Docker is not installed

`sudo apt-get install` [`docker.io`](http://docker.io)

`sudo docker ps`

`sudo chown $USER /var/run/docker.sock`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704278167448/f89c0950-75a0-4a74-ad85-408b5f9932ae.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704278206298/c69903bb-aa27-472a-a6ef-c87b7a1bf90c.png align="center")

The command `terraform init` is used to initialize a Terraform working directory.

```basic
  terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704278272852/12bd5316-2ed1-40e6-b24d-dc67226de541.png align="center")

The `terraform plan` command is used to create an execution plan. It analyzes your Terraform configuration and compares it to the current state of your infrastructure to determine what changes need to be made. It doesn't actually apply any changes; it simply outlines what actions Terraform will take when you apply the configuration.

```basic
  terraform plan
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704280271127/fe324ed1-505b-4019-9830-f4ea3bd6e83c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704280345164/7247050a-2ae6-4108-831c-8b680549ed1f.png align="center")

The `terraform apply` command is used to apply the changes defined in your Terraform configuration to your infrastructure.

```basic
terraform apply
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704280959986/d910634b-294f-4da3-a38b-d6494c6a9f19.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704281101631/f736fc09-2225-4351-a3c6-ba68e50bc236.png align="center")

Use the below command to view the docker container that was created:

```basic
docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704281297063/339cfaf2-91c5-4f8f-90c3-e666aa76ab5c.png align="center")

Now, navigate to the public IP to view the nginx welcome page

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704281439509/928f1123-e251-4795-8eb3-41f1eb2a322b.png align="center")