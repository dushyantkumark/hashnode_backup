---
title: "Day 6 of #TerraWeek - Terraform Providers"
datePublished: Sat Jun 10 2023 12:20:42 GMT+0000 (Coordinated Universal Time)
cuid: clipyszro05kpzknvaphw1hgb
slug: day-6-of-terraweek-terraform-providers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686376055472/5ed5c321-5b29-4d03-b9ee-44d3a1c644eb.png
tags: devops, terraform, 90daysofdevops, trainwithshubham, terraweekchallenge

---

## **🌟 Introduction:**

In this post, we will dive into <mark>Terraform providers</mark>, explore provider configuration and authentication, and practice using providers for platforms such as <mark>AWS</mark>, <mark>Azure</mark>, and <mark>Google</mark> Cloud.

### **🔹 Understanding Terraform Providers**

Terraform providers are <mark>plugins</mark> that enable Terraform to interact with various cloud platforms, infrastructure services, and APIs. Providers are responsible for understanding API interactions and exposing resources that can be managed using Terraform. Some popular providers include AWS, Azure, Google Cloud, and many others.

To use a provider, you need to declare it in your Terraform configuration file (usually a **<mark>.tf</mark>** file). Here's an example of declaring the AWS provider:

```plaintext
provider "aws" {
  region = "us-east-1"
}
```

Terraform providers are plugins that allow Terraform to interact with various cloud platforms and infrastructure services. They are responsible for understanding API interactions and exposing resources to be managed by Terraform. Some popular Terraform cloud providers include:

* AWS: [**Terraform AWS Provider**](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
    
* Azure: [**Terraform AzureRM Provider**](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)
    
* Google Cloud: [**Terraform Google Cloud Provider**](https://registry.terraform.io/providers/hashicorp/google/latest/docs)
    

### **🔹** Comparing Providers

Each provider has its own set of supported resources and features. To compare them, visit the respective provider's documentation and explore the available resources and data sources.

### **🔹 Provider Configuration and Authentication**

Each provider has its own set of configuration options, which are used to authenticate and interact with the respective cloud platform or service. These options can include API keys, access tokens, or other credentials required for authentication.

For example, the AWS provider requires an access key and a secret key for authentication. You can provide these credentials in several ways, such as environment variables, shared credentials file, or directly in the provider configuration block:

```plaintext
provider "aws" {
  region     = "us-west-2"
  access_key = "your_access_key"
  secret_key = "your_secret_key"
}
```

However, it's recommended to use environment variables or shared credentials files to avoid exposing sensitive information in your Terraform configuration files.

### **🔹 Working with AWS Provider**

The AWS provider allows you to manage resources in your AWS account. To get started, declare the AWS provider in your Terraform configuration file:

```plaintext
provider "aws" {
  region = "us-east-1"
}
```

Next, let's create an Amazon S3 bucket using the AWS provider:

```plaintext
resource "aws_s3_bucket" "my_bucket" {
  bucket = "my-example_2023-bucket"
  acl    = "private"
}
```

After defining the resource, run **<mark>terraform init</mark>** to initialize your Terraform working directory and download the required provider plugins. Then, run **<mark>terraform plan</mark>**, **<mark>terraform apply</mark>** to generate a plan of action and then create the S3 bucket.

### **🔹** Working with Azure Provider

The Azure provider allows you to manage resources in your Azure account. To get started, declare the Azure provider in your Terraform configuration file:

```plaintext
provider "azurerm" {
  features {}
}
```

Next, let's create a resource group using the Azure provider:

```plaintext
resource "azurerm_resource_group" "my_resource_group" {
  name     = "my-test-resource-group"
  location = "West US"
}
```

After defining the resource, run **<mark>terraform init</mark>**, **<mark>terraform plan</mark>** and **<mark>terraform apply</mark>** to create the resource group.

### **🔹 Working with Google Cloud Provider**

The Google Cloud provider allows you to manage resources in your Google Cloud account. To get started, declare the Google Cloud provider in your Terraform configuration file:

```plaintext
provider "google" {
  project = "my-example-project"
  region  = "us-central1"
  zone    = "us-central1-a"
}
```

Next, let's create a Google Cloud Storage bucket using the Google Cloud provider:

```plaintext
resource "google_storage_bucket" "my_bucket" {
  name     = "my-example_2023-bucket"
  location = "US"
}
```

After defining the resource, run **<mark>terraform init</mark>, <mark>terraform plan</mark>** and **<mark>terraform apply</mark>** to create the storage bucket.

## **🌟 Conclusion**

In this post, we explored Terraform providers and their role in interacting with different cloud platforms and infrastructure services. We also discussed provider configuration, and authentication and practiced using providers for AWS, Azure, and Google Cloud. By mastering Terraform providers, you can efficiently manage and provision infrastructure across multiple cloud platforms, making your infrastructure management more streamlined and consistent.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#terraform #terraform module #module versoning #aws #DevOps #TrainWithShubham #TerraWeekChallenge

#90daysofdevopsc #happylearning

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)