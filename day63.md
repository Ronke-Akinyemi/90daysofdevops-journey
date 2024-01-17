---
title: "Terraform Variables"
datePublished: Sat Jan 06 2024 00:37:11 GMT+0000 (Coordinated Universal Time)
cuid: clr1c55r4000108l5g7qo0czi
slug: terraform-variables
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704500781380/194aa235-01ea-4854-a58a-75856be468c6.png
tags: aws, terraform, 90daysofdevops

---

Variables in Terraform are quite important, as you need to hold values of names of instance, configs , etc.

Terraform variables are a powerful feature that allows you to define reusable and configurable values within your Terraform configuration. They are used to decouple your infrastructure configuration from specific values, making it easier to maintain, share, and reuse your configuration.

We can create a [variables.tf](http://variables.tf) file which will hold all the variables.

```basic
variable "filename" {
default = "/home/ubuntu/terrform-tutorials/terraform-variables/demo-var.txt"
}
```

```basic
variable "content" {
default = "This is coming from a variable which was updated"
}
```

These variables can be accessed by var object in [main.tf](http://main.tf)

## Task-01

* Create a local file using Terraform
    

Hint:

```basic
resource "local_file" "devops" {
filename = var.filename
content = var.content
}
```

* Create a [`variable.tf`](http://variable.tf) file
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704447259731/5fa7368b-192a-4ffb-ac5a-0d039c73f529.png align="center")

Create a [`main.tf`](http://variable.tf) file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704447410135/0d1733c5-2cb6-44d1-ab47-69c507d75214.png align="center")

After defining your `variable.tf` and [`main.tf`](http://main.tf), you can run the following Terraform commands:

```basic
terraform init
terraform plan
terraform apply
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704447657148/65b3c55f-9a04-41ea-8306-cb9ca5910b77.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704447818763/5b7549de-4adf-463c-9739-b7dad2dad997.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704448241194/ccc79fe4-3253-4e4c-8178-d041320af992.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704448266726/a5b3731a-62be-495e-9214-5c95b5f57968.png align="center")

Verify the file is created

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704475288049/94cf9937-ebe0-4bcd-853d-53eb5e64ab43.png align="center")

## Data Types in Terraform

**Map:** Represents a collection of key-value pairs.

**List:** Represents ordered sequences of values.

**Set:** Represents an unordered collection of unique values.

**Object:** Represents a complex data structure with multiple attributes.

**String:** Represents sequences of characters.

**Number:** Represents numeric values (integers or floating-point numbers).

**Bool:** Represents boolean values (true or false).

**Tuple:** Represents an ordered collection of values with fixed types and a fixed number of elements.

### Map

A map is a collection of key-value pairs where each key and value can be of any data type.

Example of a map:

```basic
variable "file_contents" {
type = map
default = {
"statement1" = "this is cool"
"statement2" = "this is cooler"
}
}
```

Create a `variable.tf` file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704476827244/2a01b049-e71e-44bd-894f-55f9e9e10092.png align="center")

Create a `main.tf` file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704476939560/8f545505-21a5-46cd-ad51-f0d9a33e437e.png align="center")

Now run the command `terraform init` to initialize the Terraform.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704477486224/2ceaeb49-7e6f-4583-80c8-4304e2a66a54.png align="center")

Run `terraform plan` command to create an execution plan.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704477603281/f0614563-c58e-4f66-b658-031d200f17f2.png align="center")

Run `terraform apply`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704478082145/0697e5c4-5cc7-4cc9-852b-ff0b85cb1f1c.png align="center")

Verify

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704478176598/b24efcc2-a9f5-4b9c-a3b0-b3739b51344b.png align="center")

## Task-02

* Use terraform to demonstrate usage of List, Set and Object datatypes
    
* Put proper screenshots of the outputs
    

Use `terraform refresh`

To refresh the state by your configuration file, reloads the variables

### List

In Terraform, a list is a data type that represents an ordered sequence of values. Lists are useful when you need to work with a collection of elements where the order matters. You can define a list variable, use it in resource configurations, and access individual elements by their index.

Lists are represented by enclosing values within square brackets.

Example of a list:

```basic
variable "example_list" {
  type    = list(string)
  default = ["item1", "item2", "item3"]
}
```

### **Object**

In Terraform, an object is a collection of named attributes, each of which has a specific value. It's a flexible way to organize and store structured data within Terraform configurations.

Objects are declared using curly braces `{}` followed by a comma-separated list of attribute-value pairs.

```basic
variable "aws_ec2_object" {
  type = object({
    name     = string
    instance = number
    keys     = list(string)
    ami      = string
  })
  default = {
    name     = "Terraform"
    instance = 1
    keys     = ["Terraformkeypair.pem"]
    ami      = "ami-0c7217cdde317cfec"
  }
}
```

Create a [`variables.tf`](http://variables.tf/) file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704479541954/40e54e91-760c-42be-91c8-349bb86f377d.png align="center")

Create a `main.tf` file

```basic
output "aws_ec2_object" {
  value = var.aws_ec2_object
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704479666207/88623910-1655-495c-8ed6-541cc9753398.png align="center")

Run `terraform init`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704480160325/a5f760db-dfc6-48bd-902a-1ab1ee2f9f4f.png align="center")

Run `terraform plan`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704480196487/3156b6db-dc33-4197-9e55-af0d6650cffa.png align="center")

Run `terraform apply`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704480693191/2323a161-9914-4afb-ad1d-e1d1683ba023.png align="center")

### **Set**

In Terraform, a set ia s data type that represents an unordered collection of unique values. Sets are useful when you want to ensure that a group of elements contains only distinct values. Sets do not preserve the order of elements, and each element must be unique within the set.

Create a [`variables.tf`](http://variables.tf/) file

```basic
variable "sercurity_groups" {
  type    = set(string)
  default = ["sg-135791112", "sg-246810124"]
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704481318591/ee073ed5-8f40-48b7-b682-cf507a0ec013.png align="center")

Create a [`main.tf`](http://variables.tf/) file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704481389130/adcb0657-d2ab-423e-be48-2aac229104a4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704481767707/62c4c97b-c66d-453c-828a-943a54273309.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704481858726/1eb6b350-c025-4d46-b459-7f10cc15bc9e.png align="center")

Use `terraform refresh` to refresh the state by your configuration file, and reload the variables.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704481987537/d08b393e-6c43-40d0-8867-a82f68e2b0c6.png align="center")

The `terraform refresh` command is typically used to update the state file before running a `terraform plan` or `terraform apply` command. This ensures that Terraform is aware of any changes that have been made to your infrastructure outside of Terraform.
