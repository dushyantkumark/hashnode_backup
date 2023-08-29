---
title: "Part 1: CI/CD Pipeline on AWS"
datePublished: Tue Aug 29 2023 15:18:38 GMT+0000 (Coordinated Universal Time)
cuid: cllwgdyv600130alcf8ab5i78
slug: part-1-cicd-pipeline-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693314310276/fb6acaf2-091d-433a-9066-f8fcb7d37df1.png
tags: aws, codecommit, 90daysofdevops, trainwithshubham, aws-services

---

# 🌟 Introduction

Continuous Integration and Continuous Deployment (CI/CD) on AWS (Amazon Web Services) involves automating the process of building, testing, and deploying software applications. This ensures that changes to your codebase are integrated smoothly and deployed to production efficiently. AWS offers a range of services and tools that can be used to implement a CI/CD pipeline

We'll be learning to make a CI/CD pipeline on AWS with these tools.

* CodeCommit
    
* CodeBuild
    
* CodeDeploy
    
* CodePipeline
    
* S3
    
* IAM (user and role)
    

# **🌟 What is CodeCommit?**

CodeCommit is a managed source control service by AWS that allows users to store, manage, and version their source code and artifacts securely and at scale. It supports Git, integrates with other AWS services, enables collaboration through branch and merge workflows, and provides audit logs and compliance reports to meet regulatory requirements and track changes. Overall, CodeCommit provides developers with a reliable and efficient way to manage their codebase and set up a CI/CD pipeline for their software development projects.

# 🌟**Follow these steps to perform this hands-on**

## 🔱TASK 1: **Create an AWS CodeCommit repository**

### ✔Step 1: Go to AWS Console and search CodeCommit

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693245195175/190d4bad-6add-4e87-99be-f2212e924096.png align="center")

### ✔Step 2: Create Repository

Go to the CodeCommit from the AWS search box. Click on `Create repository`.

Enter the details like the "Repository name" and "Description" and click on `Create` button.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693245343500/2eaa06b0-abb1-4e3d-816b-35442973ade9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693245314980/c55eac8a-c1e6-40fd-a445-870dd1fc6ced.png align="left")

Click on the clone URL that is **"HTTPS".** Now set iam user for **"HTTPS Git Credentials for AWS CodeCommit".**

The repository will be created successfully as shown below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693245363166/68a0baa4-5e5c-4770-a66b-a0fd1e36bd6a.png align="center")

### ✔Step 3: Uploading some files

select Clone URL type such as "**Clone HTTPS**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693245981722/5d4835e9-b24b-41b0-bb42-e7f52ce4b99a.png align="center")

First, add the file and then upload your file. **You only select and upload only one single file at a time only**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693246026242/60272bcb-14c0-4359-92e3-befcac303fe8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693246039816/94774204-126a-4b5a-bcf2-69fb7a6e0a97.png align="center")

Your file output is present in the repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693246058990/55d5720c-5b9a-413b-a126-43c1a8d1e969.png align="center")

## 🔱TASK 2: Set up GitCredentials in AWS IAM

### ✔Step 1: Create a new user

First, create a new user and then click on the user.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693245709651/c7b7c58f-0fb3-48a2-8244-192b24185533.png align="left")

Provide a username for the new user.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693245722134/1f0f879a-af0b-45cd-8bd8-0c068e2c2d03.png align="center")

Provide a custom password for the new user.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693245735036/328cf993-814e-4caf-982a-a8762fb7cc3c.png align="center")

Attaching policies directly, or customizing their access.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693245760853/978aa6ad-4f46-4a54-b352-ff75ddb593ce.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693245789329/a487ba43-2200-4a88-8ba5-aa9baabd3b47.png align="center")

You get a Username and custom Password for signing into the AWS Management Console.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693245808618/b9d61f77-fdbd-4b78-96b3-251b671e5690.png align="center")

### ✔Step 2: Setup HTTPS Git Credentials

Navigate to the "**Security Credentials**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693246624032/caab80a9-061c-4732-81b1-c33632557f81.png align="center")

Come down to the **"HTTPS Git Credentials for AWS CodeCommit".** Click on `Generate credentials`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693246661450/2d129004-c7be-4954-8e49-2551aeffb495.png align="left")

Make sure to download these credentials in the system for further use.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693246753719/5a215824-784d-43ab-84d5-1f191b3d36a5.png align="left")

## 🔱TASK 3: Perform Git-related Operations

### ✔Step 1: Login into IAM user

Login to your IAM user and check your code commit repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693247091849/4c43f866-d08d-4363-a3bb-685b83d46ab9.png align="center")

Search for code commit service in the "Mumbai" region.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693247107689/5a5abc9e-1b4f-4b47-96e9-212c7b743023.png align="center")

Here you get your repository created in the root account.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693247847813/bf40f5e8-e835-4b9e-bbb3-f24309d31e0a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693247150713/cd879066-8d38-4bf9-a2af-55d5a7f789c4.png align="center")

### ✔Step 2: Clone "demo\_repo\_codecommit" repository

Open the **Git Bash Terminal**. Paste here cloned `HTTP URL` and enter.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693247312235/e0b5ca90-f750-4bad-a135-8a629156378f.png align="center")

Enter your credentials and set up the connection between your local repository and the code commit repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693247376311/21e86c73-1a39-4c0c-90fe-f6086f2631ea.png align="center")

Clone repository from code commit. You get your "deploy\_static\_page\_play.yml" file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693247409018/2203d0c1-c859-45f9-963a-5e14c6ae137e.png align="center")

Add some more files to your local repository and perform the git operations task.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693247431161/09ad182e-7a1f-46c7-acd7-8d4e707b38c1.png align="center")

After adding some more files to your local repository check your status of the local repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693247446541/a38dea7c-2e5f-488b-be65-01d706c7ad63.png align="center")

Perform the adding operation and then check your local repository status. Now you tracked your files.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693247461694/41ebb0bf-0dd8-4ef8-bdc4-c0e7b5fac1db.png align="center")

Push your files from the local repository to the code-commit repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693247476469/b2d48926-744d-4b62-a514-dd715af2aac7.png align="center")

Your files uploaded successfully and are present in the code commit repository, which is shown below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693248150154/f3180703-498f-4e4a-9743-73e23cb3aa62.png align="center")

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.😊

#aws #cloudcomputing #codecommit #github #git #Devops #TrainWithShubham #90daysofdevops #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)