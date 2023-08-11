---
title: "Day 2 of #TerraWeek - Terraform Configuration Language (HCL)"
datePublished: Tue Jun 06 2023 12:25:39 GMT+0000 (Coordinated Universal Time)
cuid: clik97yfm0um4amnvcg8s34z4
slug: day-2-of-terraweek-terraform-configuration-language-hcl
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686034807234/70132dc9-49a4-4c28-b45d-ead9921b5011.png
tags: devops, terraform, 90daysofdevops, trainwithshubham, terraweekchallenge

---

## 🌟**Introduction**

In this blog, we will explore the HashiCorp Configuration Language (HCL) syntax used in Terraform and learn how to write Terraform configurations using HCL syntax. We will also cover variables, data types, and expressions in HCL, as well as some best practices for testing and debugging your Terraform configurations.

### 🔹 HCL Syntax

HCL is a configuration language used by Terraform to define infrastructure as code. It is a simple, human-readable language that allows you to define resources and data sources in a declarative way.

### 🔹 Blocks

In HCL, resources and data sources are defined using blocks. A block is a collection of <mark>parameters</mark> and <mark>arguments</mark> that define a specific resource or data source. Here is an example of a block that defines an AWS EC2 instance:

```plaintext
resource "aws_instance" "my-aws-instance" {
  ami           = "ami-08c40ec9ead489470"
  instance_type = "t2.micro"
}
```

In this example, the **resource** is the <mark>block name</mark>, **aws\_instance** is the <mark>block type</mark>, **my-aws-instance** is the <mark>block label</mark>, and **ami** and **instance\_type** are the <mark>parameters</mark>.

### 🔹 Parameters and Arguments

Parameters are the names of the attributes that define a resource or data source. Arguments are the values assigned to those attributes. In the example above, **ami** and **instance\_type** are the <mark>parameters</mark>, and **"ami-0c55b159cbgjg6c52g4"** and **"t2.micro"** are the <mark>arguments</mark>.

## 🌟Variables, Data Types and Expressions

Variables are an important part of Terraform configurations. They allow you to define values that can be reused throughout your configuration. In HCL, variables are defined using the **<mark>variable</mark>** block.

### 🔹 Defining Variables

To define a variable, create a **<mark>variable.tf</mark>** **file and add the following code:**

```plaintext
variable "filename" {
  type = string
}
```

In this example, we are defining a variable called **filename** with a data type of **string**.

### 🔹 Using Variables

To use a variable in your Terraform configuration, you can reference it using the **<mark>${var.variable_name}</mark>** syntax. Here is an example of how to use the **filename** variable in a **main.tf** **file:**

```plaintext
resource "local_file" "example" {
  filename = "${var.filename}"
  content  = "Hello, World!"
}
```

In this example, we are creating a **<mark>local_file</mark>** resource and using the **filename** variable as the name of the file.

### 🔹 Data Types and Expressions

HCL supports several data types, including strings, numbers, booleans, lists, and maps. You can also use expressions to manipulate data types. Here is an example of how to use data types and expressions in Terraform:

```plaintext
 variable "senior" {
   type    = number
   default = 7
 }

 variable "is_exp" {
   type    = bool
   default = var.senior >= 3
 }

 variable "greeting" {
   type    = string
   default = "Hello"
 }

 resource "aws_instance" "instance-example" {
   ami           = "ami-12345678"
   instance_type = var.is_exp ? "t2.large" : "t2.micro"
   tags = {
     Name = "my-instance"
     Senior  = var.senior
   }
 }

 output "message" {
   value = "${var.greeting}, ${aws_instance.instance-example.tags.Name}! You are ${var.senior} in experience."
 }
```

In this example, we have three variables: `senior`, `is_exp`, and `greeting`. The `senior` variable is of type `number` with a default value of 7. The `is_exp` variable is of type `bool` and its value is derived based on whether the senior is greater than or equal to 7. The `greeting` variable is of type `string` with a default value of "Hello".

The `aws_instance` resource creates an AWS EC2 instance. The `instance_type` attribute is set conditionally based on the value of `is_exp`. If `is_exp` is true, it sets the instance type to "t2.large"; otherwise, it sets it to "t2.micro". The resource also includes tags where the `Name` tag is set to "my-instance" and the `Senior` tag is set to the value of `senior`.

The `output` block defines a message that uses string interpolation to include the values of variables and attributes. It combines the `greeting` variable, the `Name` tag from the `aws_instance` resource, and the `senior` variable to create a personalized message.

When you run Terraform with this configuration, it will provision an AWS EC2 instance and display the output message with the interpolated values.

## 🌟 Writing Terraform Configurations

Now that we have covered the basics of HCL syntax, variables, data types, and expressions, let's write a Terraform configuration using HCL syntax.

### 🔹 Adding Required Providers

The first step is to add the required providers to your configuration. In the first example, if you want to use the Docker provider, you can add the following code to your **main.tf** **file:**

```plaintext
provider "docker" {
  host = "tcp://localhost:2375/"
}
```

In this example, we are adding the Docker provider and specifying the host URL.

In the second example, if you want to use the AWS provider, you can add the following code to your **main.tf** **file:**

```plaintext
provider "aws" {
    default     = "us-east-1"
    description = "AWS region where resources will be created"
}
```

In this example, we are adding the AWS provider and specifying the region.

### 🔹 Creating Resources

Next, we can create resources using HCL syntax. Here is an example of how to create a Docker container:

```plaintext
resource "docker_container" "docker-example" {
  image = "nginx:latest"
  name  = "nginx-container"  
  ports {
    internal = 80
    external = 8080
  }
}
```

In this example, we are creating a Docker container called **<mark>nginx-container</mark>** with the latest version of the **nginx** image and mapping port 80 to port 8080.

### 🔹 Creating Data Sources

Data sources allow you to retrieve information about existing resources. Here is an example of how to create a data source that retrieves information about an AWS EC2 instance:

```plaintext
data "aws_instance" "instance-example" {
  instance_id = "i-0123456789abcdef0"
}
```

In this example, we are creating a data source that retrieves information about an AWS EC2 instance with the <mark>ID </mark> **<mark>i-0123456789abcdef0</mark>**.

## 🌟Testing and Debugging

Testing and debugging your Terraform configurations is an important part of the development process. Here are some tips and best practices for testing and debugging your configurations:

* Use the **<mark>terraform plan</mark>** command to preview changes before applying them.
    
* Use the **<mark>terraform apply</mark>** the command to apply changes to your infrastructure.
    
* Use the **<mark>terraform destroy</mark>** command to destroy resources created by your configuration.
    
* Use the **<mark>terraform state</mark>** command to view the current state of your infrastructure.
    
* Use the **<mark>terraform validate</mark>** command to check your configuration for syntax errors.
    
* Use the **<mark>terraform fmt</mark>** command to format your configuration for consistency.
    

## 🌟Conclusion

In this blog, we have explored the basics of HCL syntax and learned how to write Terraform configurations using HCL syntax. We have also covered variables, data types, and expressions in HCL, as well as best practices for testing and debugging your Terraform configurations. By following these guidelines, you can write efficient and effective Terraform configurations that will help you manage your infrastructure as code.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#terraform #aws #DevOps #TrainWithShubham #TerraWeekChallenge

#90daysofdevopsc #happylearning

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn: </mark> [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog:</mark>[**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)