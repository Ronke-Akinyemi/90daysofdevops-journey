---
title: "Some Interview Questions & Answers of Terraform"
datePublished: Thu Jan 25 2024 18:28:52 GMT+0000 (Coordinated Universal Time)
cuid: clrtjsj4m00000al67vmqbogg
slug: some-interview-questions-answers-of-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706207147592/582b0e68-532a-4750-b955-47e95f372bf8.png
tags: aws, terminal, 90daysofdevops

---

**Question1: What is Terraform and how it is different from other IaaC tools?**

Terraform is an infrastructure as code (IaC) tool that allows you to create, manage, and update infrastructure resources such as virtual machines, networks, and storage in a repeatable, scalable, and automated way.

Terraform is different from other IaaC tools due to the following

**Declarative approach:** Terraform is declarative. With Terraform, you describe the desired outcome (e.g., servers with specific configurations, networks with certain connections) in your code. Terraform determines how to achieve that state in your chosen cloud or platform. This makes Terraform code easier to understand, maintain, and reuse, especially for complex infrastructure.

**Multi-cloud support:** Terraform is platform-agnostic, meaning it can work with multiple cloud providers like AWS, Azure, Google Cloud Platform, and many others. This flexibility allows you to manage your infrastructure in a hybrid environment or easily migrate between providers without rewriting your code.

**State management:** Terraform maintains a state file that keeps track of the current configuration of your infrastructure. This makes it easy to understand what's deployed, track changes, and revert to previous versions if needed.

**Modularity and reusability:** You can break down your infrastructure into reusable modules in Terraform, making managing and maintaining large and complex configurations easier. This modularity also promotes code sharing and collaboration between teams.

**Version control:** Terraform code can be stored in version control systems like Git, allowing you to track change, collaborate with others, and roll back to previous versions if needed.

**Plan and Apply Workflow:** Terraform employs a "plan" and "apply" workflow, allowing users to preview changes before applying them. This helps prevent unintended modifications and provides a controlled deployment process.

**Community and Ecosystem:** Terraform has a large and active community, providing a wealth of modules, documentation, and support.

**Question 2: How do you call a**[**main.tf**](http://main.tf)**module?**

In Terraform, the [main.tf](http://main.tf) file is the default configuration file where you define the primary infrastructure resources for a module. To "call" a module in another Terraform configuration, you can use the module block and provide the necessary source information.

Create a [main.tf](http://main.tf) file, define a module block and specify a name

```basic
#main.tf

    module "example" {
      source = "./path/to/main.tf"
    }
```

The module "example" block is used to create the module, and the "source" specifies the path to the directory containing the [main.tf](http://main.tf) module configuration (./path/to/main.tf in this case)

**Question 3: What exactl**[**y**](http://main.tf/)**is Sentinel? Can you provide few examples where we can use for Sentinel policies?**

Sentinel is a **Policy as Code (PaC)** framework. It allows you to define and enforce organisational policies throughout your Terraform workflow, ensuring compliance and best practices for infrastructure provisioning.

1. **Naming Conventions:** Sentinel helps to enforce a specific naming convention for resources to maintain consistency and improve readability.
    
2. **Tagging Requirements:** Sentinel ensure all resources are tagged with specific key-value pairs for tracking and categorization purposes.
    
3. **Security Controls:** Sentinel helps define security controls to prevent insecure configurations, such as allowing public access to specific resources.
    
4. **Resource Size Limits:** Sentinel enables you to set limits on the size or capacity of specific resources to prevent over-provisioning.
    
5. **Environment-specific Policies:** Sentinel helps to define rules that vary based on the environment (e.g., development, production) to allow for policy flexibility.
    

**Question 4: You have a Terraform configuration file that defines an infrastructure deployment. However, there are multiple instances of the same resource that need to be created. How would you modify the configuration file to achieve this?**

In Terraform, when you need to create multiple instances of the same resource, you can use a resource block with a `count` parameter or, `for_each` parameter.

Use the `count` parameter when you have a fixed number of instances and when the instances are similar and can be identified by an index.

Use `for_each` when you need more dynamic control over the instances and the instances have unique identifiers that are not based on an index.

**Question 5:** You want to know from which paths Terraform is loading providers referenced in your Terraform configuration (\*.tf files). You need to enable debug messages to find this out. Which of the following would achieve this?

A. Set the environment variable TF\_LOG=TRACE

B. Set verbose logging for each provider in your Terraform configuration

C. Set the environment variable TF\_VAR\_log=TRACE

D. Set the environment variable TF\_LOG\_PATH

The correct option to enable debug messages in Terraform and find out from which paths Terraform is loading providers is:

A. Set the environment variable TF\_LOG=TRACE

**Question 6:** Below command will destroy everything that is being created in the infrastructure. Tell us how would you save any particular resource while destroying the complete infrastructure.

```basic
terraform destroy
```

To save any particular resource from destruction, you can use the `-target` option to specify the resource you want to destroy individually. The `-target` allows you to destroy specific resources while leaving others intact.

```basic
terraform destroy -target=resource_type.resource_name
```

For example:

```basic
terraform destroy -target=aws_instance.example_instance
```

This command will only destroy the AWS instance named `example_instance` while leaving other resources untouched.

**Question 7: Which module is used to store .tfstate file in S3?**

Terraform Module

Terraform module to provision an S3 bucket to store terraform. tfstate file.

**Question 8: How do you manage sensitive data in Terraform, such as API keys or passwords?**

**Environment Variables:** Use environment variables to pass sensitive information to Terraform. Terraform automatically picks up environment variables with a specific naming convention, like TF\_VAR\_variable\_name.

**Provider-Specific Credential Configuration:** Various Terraform providers allow you to configure credentials securely, such as using profiles or credential files. For example, AWS credentials can be managed through the AWS CLI configuration or environment variables.

**Secret Vault:** Use external management tools like HashiCoorp Vault, Azure Key Vault, AWS Secret Manager, or Google Cloud KMS to store and manage your secrets securely.

**Question 9:You are working on a Terraform project that needs to provision an S3 bucket, and a user with read and write access to the bucket. What resources would you use to accomplish this, and how would you configure them?**

To provision an S3 bucket and a user with read and write access to the bucket using Terraform, you will need the following resources:

* The aws\_s3\_bucket: This creates an S3 bucket with a specified name.
    
* The aws\_iam\_user and aws\_iam\_user\_policy: These resources create the IAM user and grant them access to the S3 bucket:
    
* The aws\_iam\_access\_key resource creates an access key for the IAM user, which can be used for programmatic access.
    

**Question 10: Who maintains Terraform providers?**

Terraform providers are maintained by the respective cloud service or infrastructure platform providers.

**Question 11: How can we export data from one module to another?**

In Terraform, you can export data from one module to another using output variables. Define an output block in the first module that exposes the data you want to share. In the second module, use an input block with the corresponding name to receive the exported data.

Thank you.