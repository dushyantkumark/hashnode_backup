---
title: "Project Title:- Deploy ChatGPT Clone"
datePublished: Wed Jul 19 2023 12:42:41 GMT+0000 (Coordinated Universal Time)
cuid: clk9prhsb000209l33fwoes3x
slug: project-title-deploy-chatgpt-clone
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689763354122/8aaee5f6-eb24-41af-b950-96f73e182e59.png
tags: aws, devops, aws-fargate, 90daysofdevops, trainwithshubham

---

# **🌟** Project Description

***<mark>📢 The project involves deploying a </mark>* <mark>ChatGPT</mark> *<mark>clone on AWS ECS(Cluster/container orchestration) using Fargate and AWS ECR(Registry can say Dockerhub for AWS</mark>🚀***

### Tools Used:

* ☁ AWS console for EC2 instance
    
* 📦 Git & GitHub
    
* 🔱 Amazon IAM
    
* ⚡ AWS CLI
    
* 🏪 Amazon ECR
    
* 🚀 Amazon ECS
    
* 📊📈 Amazon CloudWatch
    

# **🌟**Setup an ECS cluster

## **<mark>📍Step1: Setup &amp; Launch an EC2 instance</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689752573441/550b2c97-15ac-4e59-a2fd-f1796febdf9a.png align="left")

## **<mark>📍</mark>**<mark>Step2: Clone your code from Github repository</mark>

```plaintext
git clone https://github.com/dushyantkumark/chatgpt-clone
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689752610036/995df166-cf78-43f7-beab-f582817088d0.png align="center")

## **<mark>📍Step3: Create IAM user with attached permissions/policies</mark>**

First, we have to create a user, attach the necessary policy and then create an access key and secret access key. Go to secret credentials to assign access key and secret access key.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689753610370/3c15084b-f030-40c7-8ae5-57d8bbb7ec13.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689753622320/2c600065-7cc3-4e71-82f3-f7467c06fbb4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687878280195/37f33a2e-2737-4c20-9336-57a285a228c8.png?auto=compress,format&format=webp align="left")

## **<mark>📍Step4:Setup AWS CLI &amp; configure your credentials</mark>**

Configure AWS using different commands that are available below

```plaintext
sudo apt update
sudo apt-get install awscli 
aws --version
aws configure
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689754880289/ec1f18e9-8715-416c-b307-860bb1f19809.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689754896900/919922eb-064e-41a2-b15d-e5198ab25604.png align="left")

## **<mark>📍Step5:It's time to setup Amazon ECR</mark>**

*ECR is an acronym for the* ***“<mark>Elastic container registry</mark>”.*** *In simple terms, it is the so-called* ***“<mark>AMAZON DOCKER HUB</mark>”*** *of your containers!*

<mark>Here are the execution steps:</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689755797439/381f299c-710a-4b35-a133-e43dc5b83a21.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689755807998/26058ffa-9efe-4792-a820-26bb10a30c20.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689755944422/e2305a20-73e7-470b-9f00-52640dfac0cc.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689755967682/37741630-447f-4720-be6b-56f18e0eb3fa.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689755984185/804ef0cc-26d8-49cf-bb4b-b2f72af2cf15.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689757370813/41d7564c-d5e9-4685-aa0c-a3f9475949e2.png align="center")

## **<mark>📍Step6:Issue below commands to push your image from local to ECR</mark>**

Your Docker file is available in your LOCAL, first login, build the image, again tag that image and pushed to ECR. It is the home for all your pushed docker images where later it can be used by ECS service to get deployed on the AMAZON platform! Command images show below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689756216958/51900d8f-d8fa-417c-8292-c9f770570523.png align="left")

Get **<mark>first error</mark>** "***<mark>Docker not found</mark>***", which means it's time to install Docker in your running instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689756251183/34e8f1e9-0e59-4106-ab3c-9bf5d647f1bd.png align="left")

Install docker, ecr public login.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689756890870/595dfdb0-4e6e-49e5-9c29-6ba6afc115bc.png align="center")

Docker tagged image, inspect the image for the port number which is required for the security group.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689757017912/4e5d124e-0b68-42a5-ae07-cad46839d891.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689757037027/bef4d87e-e89e-4a8e-8d14-f3b56bb65636.png align="left")

After docker push i.e.pushing to AWS ECR. You can verify the status is reflected in ECR or not!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689757117202/9db2209c-d780-43fa-ad06-ea2293220912.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689758435413/ca2dc0d2-1557-4714-9a8f-6ccc59af96d4.png align="center")

## **<mark>📍Step7:ECS(Amazon Elastic Container Service)</mark>**

* **<mark>CLUSTER</mark>:** ECS cluster is a regional grouping of one or more container instances on which you can run task requests.When an instance launches, the ECS-agent software on the server registers the instance to an ECS Cluster. You can choose an existing VPC, or create a new one to spin up your container instances.
    
* **<mark>TASK DEFINITION</mark>:** It is the complete definition of your tasks(in simple terms, your containers) and describes how containers should be provisioned. Here You need to provide a link to ECR’s saved container images, CPU units, Memory, Container ports to expose, network type and many more. Simple terms, you are defining your containers and how to launch them via Task definitions.
    
* **<mark>TASKS</mark>:** It is nothing but “ A RUNNING CONTAINER “. The description you provided for your containers in TASK DEFINITION, TASKS are the result of that. It can be thought of as a “RUNNING INSTANCE” of a Task Definition.(you can create a service also under the deploy option)
    

> ### ***<mark>✨STEP 1: CREATE ECR CLUSTER</mark>***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689757641097/1427a051-9d19-4ed3-a29d-843af35f3266.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689757632775/9a775758-79db-458a-b826-799fa045f833.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689757554561/3506bfbf-bdb6-4fcf-b8b6-36790f9b3cef.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689757568712/c4ee1b78-4e2e-426d-a6bc-fcb79968c22b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689757581876/c95be52a-1b3b-484f-89b2-9484b2b6d9c9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689757595945/7a3bea83-ded0-4028-bcac-05a305bbb462.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689757609734/1b5c5c91-924b-4add-8aac-aaa7572fa40c.png align="center")

> ### **<mark>✨STEP2: CREATE TASK DEFINATION</mark>**

AWS Fargate is a technology that you can use with Amazon ECS to run [**containers**](https://aws.amazon.com/what-are-containers) without having to manage servers or clusters of Amazon EC2 instances. With Fargate, you no longer have to provision, configure, or scale clusters of virtual machines to run containers. This removes the need to choose server types, decide when to scale your clusters, or optimize cluster packing.

When you run your Amazon ECS tasks and services with the Fargate launch type or a Fargate capacity provider, you package your application in containers, specify the Operating System, CPU and memory requirements, define networking and IAM policies, and launch the application. Each Fargate task has its own isolation boundary and does not share the underlying kernel, CPU resources, memory resources, or elastic network interface with another task.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689758112637/98c295ca-04d6-46f6-b7fe-187ce8627aad.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689758567239/71ca6e9b-9fcb-4fa3-bdbc-985c22cf7f1a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689758259053/3915d786-0f15-455d-8cb3-51f2d47c7a0e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689758294023/c33d724b-fae4-4054-ba3c-cb5aafdd9032.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689758667224/6129d70e-0127-483e-acbf-5a0270524088.png align="center")

> ### **<mark>✨STEP3: RUN TASK NOW!</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689759024378/a0374bb4-9cba-4cef-b264-37f4a5e5bd65.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689759071525/f4fda489-0adb-4b01-8d2e-965e9d9d86ac.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689759088804/d16283bd-a21e-4827-9aed-0636b425ba75.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689759134259/18ed92fc-7e09-4948-9338-d11598dcc6c4.png align="left")

Once you are done with the Run task, click on Running task search for ENI ID and open the port under SG on which your app is running!(FYI: not your instance port as we selected Fargate).

## **<mark>📍</mark>**<mark>Step8: Not access your application</mark>

If the application is not accessible check your security group, which your fargate is using.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689759630667/22e2a455-3b16-4e49-9e5c-92d0bbe843b7.png align="center")

## **<mark>📍Step9:Here you go and access your app over public ip.</mark>**

Access your application in any of your browsers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689759297269/98ff7560-652a-4e0e-a037-985c2821af3b.png align="left")

## **<mark>📍Step10: Logging using Cloud Watch Logs</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689760406846/43090261-0846-48c9-b8a5-85e632c1761c.png align="center")

# **🌟**Conclusion:

This project is important for learning various components of cloud services. It is a combination of vast varieties of tools from basic to advance such as Linux, Git & GitHub, AWS EC2, Docker, ECR, ECS and Clod Watch Logs. In this project, we learn step by step how things are implemented.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.

#aws #EC2 #Fargate #DevOps #TrainWithShubham #cloudcommunity #ecr #ecs

#90daysofdevops #devopscommunity #happylearning

@[Shubham Londhe](@TrainWithShubham)

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)

<mark>GitHub</mark>: [https://github.com/dushyantkumark/chatgpt-clone](https://github.com/dushyantkumark/chatgpt-clone)

\*\*\*Happy Learning :)\*\*\*✌✌

Keep learning, Keep growing🎇🎇

*<mark>Thank you for reading!! Hope you find this helpful.</mark>*