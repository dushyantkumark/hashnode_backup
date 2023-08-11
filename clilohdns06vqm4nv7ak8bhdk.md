---
title: "Day 3 of #TerraWeek - Managing Resources"
datePublished: Wed Jun 07 2023 12:20:39 GMT+0000 (Coordinated Universal Time)
cuid: clilohdns06vqm4nv7ak8bhdk
slug: day-3-of-terraweek-managing-resources
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686114885235/3321ad14-46dd-4188-a413-e76c3847ccd9.png
tags: aws, terraform, iac, trainwithshubham, terraweekchallenge

---

## 🌟**Introduction:**

In this blog post, we will explore how to manage resources using Terraform, focusing on various resource types and their configurations, such as AWS EC2 instances, Azure Virtual Machines, and Google Compute Engine. We will also discuss resource dependencies, provisioners, and lifecycle management.

### **🔹 Defining and Managing Resources with Terraform**

To define a resource in Terraform, you need to use the **resource** block followed by the resource type and a unique name. The resource type determines the kind of infrastructure object you want to create, while the unique name is used to reference the resource within your Terraform configuration.

Here's is a basic example of a resource block:

```plaintext
resource "aws_instance" "my-ec2-instance" {
  ami           = "ami-08c40ec9ead489470"
  instance_type = "t2.micro"
}
```

In this example, we're defining an AWS EC2 instance with the <mark>provider</mark> **aws** <mark>resource type</mark> **aws\_instance** and a <mark>unique name</mark> **my-ec2-instance**. The **ami** and **instance\_type** <mark>arguments</mark> are used to configure the instance.

### **🔹 AWS EC2 Instance Configuration**

```plaintext
# Define provider configuration but this is not best practice, try to use AWS CLI instead

provider "aws" {
  access_key = "<your-access-key>"
  secret_access_key = "<your-secret-access-key>"
  region = "<your-preferred-region>"
}

# Create an EC2 instance
resource "aws_instance" "my_ec2_instance" {
  count = 2
  ami = "<your-ami-id>"
  instance_type = "t2.micro"
  key_name = "<your-key-pair-name>"

  # Specify security group(s)
  vpc_security_group_ids = ["<your-security-group-id>"]

  # Configure networking
  subnet_id = "<your-subnet-id>"
  associate_public_ip_address = true

  # Define tags
  tags = {
    Name = "my-instance"
    Environment = "Production"
  }
}
```

Make sure to replace the placeholder values with your own information:

* `<your-access-key>` and `<your-secret-access-key>`: You have to specify the AWS access key and secret access key.
    
* `<your-preferred-region>`: The AWS region in which you want to launch your aws EC2 instance.
    
* `<count>`: The `count` parameter is used to create multiple instances of a resource based on a numeric value or condition. It allows you to dynamically create or manage multiple instances of a resource based on the provided count value.
    
* `<your-ami-id>`: The ID of the Amazon Machine Image (AMI) you want to use for the instance.
    
* `<your-key-pair-name>`: The name of the key pair you want to use to SSH into your instance.
    
* `<your-security-group-id>`: The ID of the security group(s) you want to associate with the instance.
    
* `<your-subnet-id>`: The ID of the subnet in which you want to launch the instance.
    

Once your code is ready, you can run the following Terraform commands in the directory containing the code:

```plaintext
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
```

The **<mark>terraform init</mark>** command initializes the working directory, downloading the necessary provider plugins.

The **<mark>terraform fmt</mark>** command is used to automatically format Terraform configuration files.

The **<mark>terraform validate</mark>** command to validate the syntax and configuration of your Terraform files. It checks for errors and potential issues in your configuration without making any changes to your infrastructure.

The **<mark>terraform plan</mark>** command shows you an execution plan for the infrastructure changes.

Finally, the **<mark>terraform apply</mark>** command applies the changes and creates the EC2 instance.

### **🔹 Azure Virtual Machine Configuration**

To create an Azure Virtual Machine using Terraform, you need to define the resource block with the **<mark>azurerm_virtual_machine</mark>** resource type. Here's an example configuration:

```plaintext
resource "azurerm_virtual_machine" "my_vm" {
  name                  = "myvm"
  location              = "East US"
  resource_group_name   = "myresourcegroup"
  network_interface_ids = ["${azurerm_network_interface.my_nic.id}"]
  vm_size               = "Standard_DS1_v2"

  storage_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "16.04-LTS"
    version   = "latest"
  }

  storage_os_disk {
    name              = "myosdisk"
    caching           = "ReadWrite"
    create_option     = "FromImage"
    managed_disk_type = "Standard_LRS"
  }

  os_profile {
    computer_name  = "myvm"
    admin_username = "ubuntu"
    admin_password = "P@ssw0rD19/23!"
  }

  os_profile_linux_config {
    disable_password_authentication = false
  }
}
```

In this example, we're creating an Azure Virtual Machine with various configurations, such as the VM size, storage image reference, OS disk, and OS profile.

### **🔹 Google Compute Engine Configuration**

To create an Azure Virtual Machine using Terraform, you need to define a provider and resource block with the **<mark>google</mark>** and **<mark>google_compute_instance</mark>** resource type. Here's an example configuration:

```plaintext
provider "google" {
  credentials = file("<PATH_TO_KEY_FILE>")
  project     = "<YOUR_PROJECT_ID>"
  region      = "<YOUR_REGION>"
}
```

```plaintext
resource "google_compute_instance" "my_instance" {
  name         = "my-instance"
  machine_type = "n1-standard-1"
  zone         = "<YOUR_ZONE>"

  boot_disk {
    initialize_params {
      image = "<IMAGE_FAMILY>"
    }
  }

  network_interface {
    network = "default"
    access_config {
      // Ephemeral IP
    }
  }
}
```

In this example, replace `<YOUR_ZONE>` with the desired zone for your instance and `<IMAGE_FAMILY>` with the desired operating system image.

### **🔹 Resource Dependencies**

Resource dependencies in Terraform are used to specify the order in which resources should be created, updated, or destroyed. By default, Terraform automatically detects dependencies between resources based on their configuration. However, you can also explicitly define dependencies using the **<mark>depends_on</mark>** argument.

Here's an example of using **<mark>depends_on</mark>** to create a dependency between an AWS EC2 instance and a security group:

```plaintext
resource "aws_security_group" "sg-example" {
  name = "my-sg"
}

resource "aws_instance" "my-instance" {
  ami           = "ami-0c94855ba95b798c7"
  instance_type = "t2.micro"

  vpc_security_group_ids = ["${aws_security_group.sg-example.id}"]

  depends_on = [aws_security_group.sg-example]
}
```

### **🔹 Provisioners**

Provisioners in Terraform are used to execute scripts or other actions on a local or remote machine as part of the resource creation or destruction process. Here's an example of using a **<mark>remote-exec</mark>** provisioner to run a script on an AWS EC2 instance:

```plaintext
resource "aws_instance" "my-instance" {
  ami           = "ami-0c94855ba95b798c7"
  instance_type = "t2.micro"

  key_name = "my_new_key_pair"

  provisioner "remote-exec" {
    inline = [
      "sudo apt-get update",
      "sudo apt-get install -y nginx"
    ]
  }
}
```

In this example, the **<mark>remote-exec</mark>** provisioner runs a script to update the package index and install the Nginx web server on the EC2 instance.

### **🔹 Lifecycle Management**

Terraform allows you to manage the lifecycle of resources using the **<mark>lifecycle</mark>** block. This block can be used to configure how Terraform should handle resource creation, updates, and destruction. Here's an example of using the **<mark>lifecycle</mark>** block to prevent the accidental destruction of an AWS EC2 instance:

```plaintext
resource "aws_instance" "my-instance" {
  ami           = "ami-0c94855ba95b798c7"
  instance_type = "t2.micro"

  lifecycle {
    prevent_destroy = true
  }
}
```

In this example, the **<mark>prevent_destroy</mark>** argument is set to **<mark>true</mark>**, which means that Terraform will not allow the EC2 instance to be destroyed.

## 🌟**Conclusion:**

In this blog post, we've explored how to manage resources using Terraform, focusing on various resource types and their configurations, such as AWS EC2 instances, Azure Virtual Machines, and Google Compute Engine. We've also discussed resource dependencies, provisioners, and lifecycle management. By understanding these concepts, you'll be better equipped to manage your cloud infrastructure using Terraform effectively.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#terraform #aws #DevOps #TrainWithShubham #TerraWeekChallenge

#90daysofdevopsc #happylearning

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn: </mark> [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog:</mark>[**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)