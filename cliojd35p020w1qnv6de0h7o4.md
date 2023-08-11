---
title: "Day 5 of #TerraWeek - Terraform Modules"
datePublished: Fri Jun 09 2023 12:20:39 GMT+0000 (Coordinated Universal Time)
cuid: cliojd35p020w1qnv6de0h7o4
slug: day-5-of-terraweek-terraform-modules
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686285042225/0ea643e3-0f8d-4ed1-9949-2400fb7291fa.png
tags: terraform, terraform-module, trainwithshubham, terraweekchallenge

---

## **🌟Introduction**

In this post, we will explore the concept of Terraform modules, their benefits, how to create and use modules to encapsulate reusable infrastructure configuration and explain module composition and versioning.

### **🔹 Understanding Terraform Modules**

Terraform <mark>modules </mark> are self-contained packages of Terraform configurations that encapsulate a set of resources and their dependencies. Modules allow you to create reusable infrastructure components that can be shared across multiple projects or environments. By using modules, you can simplify your Terraform code, improve maintainability, and promote best practices.

To create a Terraform module, you typically organize your code into a directory with a specific structure. Here's an example of a basic module structure:

```plaintext
module/
  ├── main.tf
  ├── variables.tf
  └── outputs.tf
```

### **🔹 Benefits of Using Terraform Modules**

Using Terraform modules offers several benefits, including:

* **Code reusability**: Modules enable you to create reusable infrastructure components that can be shared across multiple projects or environments, reducing code duplication and improving maintainability.
    
* **Simplified code**: By encapsulating complex infrastructure configurations in modules, you can simplify your Terraform code and make it easier to understand and manage.
    
* **Consistency**: Modules help ensure that your infrastructure is consistent across different environments, reducing the risk of configuration drift and making it easier to enforce best practices.
    
* **Collaboration**: Modules facilitate collaboration among team members working on infrastructure projects. Modules act as building blocks that can be shared, reviewed, and improved collectively. They enable different teams or individuals to work independently on different parts of the infrastructure while maintaining a cohesive and consistent overall architecture.
    
* **Versioning**: Terraform modules support versioning, allowing you to track changes to your modules over time and roll back to previous versions if needed.
    

### **🔹 Creating and Using Terraform Modules**

To create a Terraform module, you'll need to create a new directory containing a set of **<mark>.tf</mark>** files that define the resources and variables for your module. Here's an example of a simple module that creates an AWS S3 bucket:

**modules/s3\_bucket/**[**main.tf**](http://main.tf/):

```plaintext
resource "aws_s3_bucket" "my_bucket" {
  bucket = var.bucket_name
  acl    = var.acl
}

variable "bucket_name" {
  description = "The name of your S3 bucket"
  type        = string
}

variable "acl" {
  description = "The access control list for the S3 bucket"
  type        = string
  default     = "private"
}
```

To use this module in your Terraform configuration, you'll need to add a **<mark>module block</mark>** that references the module's directory:

[**main.tf**](http://main.tf)**:**

```plaintext
provider "aws" {
  region = "us-east-1"
}

module "s3_bucket" {
  source      = "./modules/s3_bucket"
  bucket_name = "my-demo_123-bucket"
}
```

### **🔹 Module Composition**

Module composition refers to the practice of using one module within another module to create more complex infrastructure configurations. By composing modules, you can build modular and scalable infrastructure components that can be easily managed and updated.

Here's an example of module composition using the S3 bucket module we created earlier:

**modules/static\_website/**[**main.tf**](http://main.tf/):

```plaintext
module "s3_bucket" {
  source      = "./s3_bucket"
  bucket_name = var.bucket_name
  acl         = "public-read"
}

resource "aws_s3_bucket_policy" "my_bucket_policy" {
  bucket = module.s3_bucket.my_bucket.id

  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action   = ["s3:GetObject"]
        Effect   = "Allow"
        Resource = "${module.s3_bucket.my_bucket.arn}/*"
        Principal = "*"
      }
    ]
  })
}

variable "bucket_name" {
  description = "The name of the S3 bucket for the static website"
  type        = string
}
```

### **🔹 Module Versioning**

Terraform modules support versioning, allowing you to track changes to your modules over time and roll back to previous versions if needed. To version your modules, you can use a version control system like <mark>Git </mark> and tag your module releases with semantic versioning.

To reference a specific version of a module in your Terraform configuration, you can use the **version** argument in the **<mark>module </mark>** block:

[**main.tf**](http://main.tf)**:**

```plaintext
provider "aws" {
  region = "us-east-1"
}
module "s3_bucket" {
  source      = "git::https://example.com/your-repo.git?ref=v1.0.0"
  bucket_name = "my-example-bucket"
}
```

Terraform uses a versioning scheme called <mark>Semantic Versioning</mark> (SemVer) to manage module versions. SemVer consists of three components: MAJOR, MINOR, and PATCH.

* **<mark>MAJOR</mark>** version increment indicates incompatible changes. This means there might be breaking changes in the module, and you may need to update your configuration to use the new version.
    
* **<mark>MINOR</mark>** version increment adds new features or functionality to the module but maintains backward compatibility. You can safely update to a new minor version without expecting any breaking changes.
    
* **<mark>PATCH</mark>** version increment includes backward-compatible bug fixes or patches. These updates address issues without introducing any new features or breaking changes.
    

To specify a module version in your Terraform configuration, you can use the `source` attribute along with the version constraint. Here are a few examples:

* Exact version constraint:
    
    ```plaintext
    module "example" {
      source  = "github.com/example/module?ref=v1.2.3"
      # ...
    }
    ```
    
* Version constraint range:
    
    ```plaintext
    module "example" {
      source  = "github.com/example/module?ref=1.2.*"
      # ...
    }
    ```
    
* Latest version constraint:
    
    ```plaintext
    module "example" {
      source  = "github.com/example/module?ref=latest"
      # ...
    }
    ```
    

## **🌟Conclusion**

Terraform modules are a powerful feature that enables you to create reusable infrastructure components and promote code reusability and maintainability. By understanding the concept of Terraform modules, learning how to create and use them, and exploring module composition and versioning, you can build modular and scalable infrastructure components that can be easily managed and updated. This will help you create more efficient and maintainable Terraform configurations.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#terraform #terraform module #module versoning #aws #DevOps #TrainWithShubham #TerraWeekChallenge

#90daysofdevopsc #happylearning

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn: </mark> [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog:</mark>[**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)

<mark>Github</mark>:[https://github.com/dushyantkumark](https://github.com/dushyantkumark)