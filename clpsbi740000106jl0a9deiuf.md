---
title: "Terraform Advance: Creating & Managing AWS Resources With Best Practice"
datePublished: Tue Dec 05 2023 12:29:42 GMT+0000 (Coordinated Universal Time)
cuid: clpsbi740000106jl0a9deiuf
slug: terraform-advance-creating-managing-aws-resources-with-best-practice
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701684311027/1c088b93-cc48-4eff-b480-eb1845825104.png
tags: aws, devops, terraform, 90daysofdevops, trainwithshubham

---

# **🌟 Introduction**

Hello DevOps enthusiasts! Welcome back. Today, we're diving deep into working with Terraform and AWS. We'll cover essential topics AWS topics EC2, S3, DynamoDB, KMS, and VPC. In Terraform we cover state management, validation, provisioners, lifecycle management and minimize issues and increase security practices using SNYK. So, let's get started!

### **📜 Prerequisites:**

* Install AWS CLI
    
* AWS Account
    
* Code Editor (I have used VS Code for this deployment)
    
* Code Editor ( Go to extensions and install snyk, then create snyk account)
    

## **📚 Steps for Implementation:**

Summary view of the terraform files in VS code:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701628391813/a2d51a26-e5a0-430c-b948-0af8e86bfa14.png align="center")

# 👨‍💻 Create AWS Services using Terraform:

## 🤖 Create terraform.tf and provider.tf file

We will start with declaring (**<mark>terraform.tf)</mark>** and (**<mark>provider.tf)</mark>** file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701627617079/c9c3b4ec-aac0-405d-8bc6-de50b6beeb58.png align="center")

Then we configure terraform in **<mark>terraform.tf</mark>** file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701627641022/af9778a9-e5b8-49eb-a204-ca2cd22bcab0.png align="left")

## 🤖 Create network vpc.tf file

Now, we want to create **<mark>vpc.tf</mark>** file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701627685167/c9d0e140-5689-401e-89ac-3f4e890211fd.png align="left")

## 🤖 Create Security aws\_sg.tf

Now, we want to create **<mark>aws_sg.tf</mark>** file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701627729975/faa4a8e9-211a-4786-8209-4b37c8e0060a.png align="center")

## 🤖 Create s3\_state\_bucket.tf file

Now, we want to create **<mark>s3_state_bucket</mark>** file for storing the terraform state file ( terraform.tfstate ).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701627749740/593f11b3-1fe2-4ef4-8b0a-6d8418af6b9c.png align="center")

## 🤖 Create kms.tf file

Now, we want to create **<mark>kms.tf</mark>** file for encrypting the dynamo db table, with a key rotation facility in 7 days.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701627761003/e1419e34-d7aa-4447-9b91-1e08af615341.png align="center")

## 🤖 Create dynamo\_lock\_table.tf file

Now, we want to create **<mark>dynamo_lock_table</mark>** file, it creates a dynamo db table and locks the state. This prevents others from acquiring the lock and potentially corrupting your state

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701627765916/6a6f31b7-3e6a-40b4-8ed8-d4e761c22eea.png align="center")

## 🤖 Create ec2\_instance.tf file

Now, we create **<mark>ec2_instance.tf</mark>** file. Configuration file specifically designed for defining and provisioning AWS EC2 instances.

## 📲 Provisioners:

Provisioners allow us to configure resources after they are created. For instance, we may need to install software on an EC2 instance. Here's a simplified example of a provisioned:

* The **<mark>file provisioner</mark>** is used to copy files or directories from the machine executing the terraform apply to the newly created resource.
    
* **<mark>remote-exec</mark>** provisioner to run commands on the instance after it's created
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701627778952/95296e65-06ef-42cc-a734-a62d21e780bb.png align="left")

We want to see the output such as subnet ID, we will mention it in **<mark>output.tf</mark>** file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701627890613/8fe1fb1d-5c2c-44f6-9b5f-b3446adeac88.png align="center")

## 🤖 Create variable.tf & dev.tfvars file

Now, we create variable.tf and dev.tfvars file.

* **<mark>variable.tf</mark>** for the declaration of variables, name, type, description, default values and additional meta data.
    
* The default name is (**<mark>terraform.tfvars</mark>**), but I customise it to **<mark>dev. tfvars</mark>** is for giving the actual variable values during execution.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701628549768/6c622a3e-44b1-40bd-9209-37273768b043.png align="center")

You must have to change **<mark>dev.tfvars</mark>** file values.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701628609394/22306a3e-1e7f-49b9-967a-98bc1a01e785.png align="center")

# 🎡 Terraform Life Cycle:

The terraform life cycle consists of **<mark>INIT, PLAN, APPLY, DESTROY</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701615564547/48f37589-19b4-41fc-a32e-705b8f0de2b9.png align="center")

### 📟 Terraform INIT

```plaintext
terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626264886/8cb1e6c5-62a2-4991-9d73-81a748223275.png align="left")

### 📺 Terraform VALIDATE & FMT

```plaintext
terraform fmt
terraform validate
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626338959/3757b64c-5bcd-460b-8399-3be659ad5a89.png align="center")

### 💡Terraform PLAN

```plaintext
terraform plan -var-file=dev.tfvars
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626375462/3ca32152-a136-4197-84da-999fc4b88cb1.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626387768/9747a003-e714-4cc8-ab35-7a2d5b861f49.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626400165/00e69813-afc1-4d1c-aabd-eb7b3783855d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626427972/7366d3e8-a12c-49ff-b8c1-42c9eb0784cd.png align="center")

### 🎢 Terraform APPLY

```plaintext
terraform apply -var-file=dev.tfvars
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626461940/34ec99a6-3aaf-40d6-850d-40f679692b54.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626492852/ed0cf5fa-21dc-43a7-8062-727cc9db7df5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626510079/09cef5e3-9f5b-4654-af14-20a47636187f.png align="center")

## Resources Created

VPC created

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701682867109/8559928d-b08c-4a14-b5a9-151fc70ac86c.png align="center")

Ec2 instance created

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701682874602/bdea2083-50e5-473d-9469-fe03d8b95161.png align="center")

S3 bucket created

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701682883938/7a39abaf-f69b-4b8a-8d85-5732bcdff081.png align="center")

KMS created

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701682894864/3cb96ffd-b7ae-44de-869a-694920650e46.png align="center")

Dynamodb table created

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701682906432/c548b579-e802-4e24-9dff-cdad1749e038.png align="center")

# 🔗Configure Backend:

Uncommit the **<mark>backend block</mark>** in **<mark>terraform.tf</mark>** file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701627003484/a20577c0-5fb1-43af-adfb-4a04977b0328.png align="center")

### 📟 Terraform INIT

```plaintext
terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626540179/7d563c63-9a22-4a0e-954b-8d38a91da9ef.png align="left")

### 💡 Terraform PLAN

```plaintext
terraform plan -var-file=dev.tfvars
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626561998/e92c6b2a-0a9a-4155-a6fa-37254f11df1b.png align="left")

### 🎢 Terraform APPLY

```plaintext
terraform apply -var-file=dev.tfvars
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626595612/e352b945-e4de-46f5-ba65-0b5c772a947b.png align="center")

If you check **<mark>terraform.tfstate</mark>** file which is present locally (in my case my Windows laptop) is empty. state move into s3 bucket.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626742616/b437b825-510d-46b5-a720-8fcd0d1b780f.png align="center")

If you want to check your state file use the below command. It pulls the state file from the s3 bucket.

```plaintext
terraform state pull
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626823789/1c92d013-0a25-42e4-8380-6284ce07e287.png align="center")

output of dev-server

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701628028570/355b656b-7ec5-4833-967f-ec4b03648796.png align="center")

### 💣Terraform Destroy

To remove the resource, use:

```plaintext
terraform destroy -var-file=dev.tfvar
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626862981/51d7ded8-c417-460e-bc1a-fe71112d7c92.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626873536/183735a3-6337-47f5-8ae0-3da01a51a1c8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701626879257/00d99328-a76d-449f-b9a4-dc877c0924e7.png align="center")

## 🎇 NOTE:

When you write a terraform file for your project, click on the extension, add snyk plugin and create your account in snyk. It automatically gives suggestions to overcome vulnerabilities.

The **<mark>Snyk Visual Studio Code plugin</mark>** scans and provides analysis of your code including open source dependencies and infrastructure as code configurations.

# 📦 Conclusion

Today, we've learned the importance of checking state files, validating configurations, adding provisioners for resource configuration, and state loking and remote backend. These are essential concepts when working with Terraform and AWS.

Remember, DevOps is all about continuous learning, so keep exploring and experimenting with Terraform to become the best DevOps engineer you can be.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.😊

#aws #cloudcomputing #terraform #Devops #TrainWithShubham #90daysofdevopsc #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Github</mark>**: [https://github.com/dushyantkumark/terraform-advance-projects](https://github.com/dushyantkumark/terraform-advance-projects)