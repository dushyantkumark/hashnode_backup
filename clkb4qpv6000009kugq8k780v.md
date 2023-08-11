---
title: "EC2: Auto-Scaling"
datePublished: Thu Jul 20 2023 12:29:45 GMT+0000 (Coordinated Universal Time)
cuid: clkb4qpv6000009kugq8k780v
slug: ec2-auto-scaling
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689840247742/f099420a-f618-4f86-a7db-f16a32ca0b7d.png
tags: aws, automation, devops, 90daysofdevops, trainwithshubham

---

# **🌟** Introduction

Automation, a capability of AWS Systems Manager, simplifies common maintenance, deployment, and remediation tasks for AWS services like Amazon Elastic Compute Cloud (Amazon EC2), Amazon Relational Database Service (Amazon RDS), Amazon Redshift, Amazon Simple Storage Service (Amazon S3), and many more.

Let's start with hands-on in which, I want to autoscale my instance. If the load increases at a particular limit or the instance is down for some reason, a new instance is created automatically.

## **📍** Flow

* Create Launch Template
    
* Create Autoscaling group
    

## **📍 Create a Launch Template for your instance**

* You can make a launch template with the configuration information you need to launch an instance. You can save launch parameters in launch templates so you don't have to type them in every time you start a new instance.
    
* For example, a launch template can have the launch template name, AMI ID, instance type, and network settings that you usually required to launch instances.
    
* You can tell the Amazon EC2 console to use a certain launch template when you start an instance.
    

# **🌟 Task 1: Create a template**

* Go to the Launch template section in AWS and create a template.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681614313881/e31fb0e7-0c97-4350-aabf-01b9e45216ca.png?auto=compress,format&format=webp align="left")
    
* Provide the AMI as Amazon Linux 2 as per project/requirement.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681614342872/f5c42fdb-61eb-48d3-9d89-ff4bdda02499.png?auto=compress,format&format=webp align="left")
    
* Provide the shape of the EC2 instance as per the required CPU and Memory, Create key pair for login to your instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681614854904/e6331c3e-d933-44a7-ac14-3201bef2994b.png?auto=compress,format&format=webp align="left")
    
* Select the subnet and security group.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681614448641/f193c8cf-3498-483f-86dc-a199be218eb8.png?auto=compress,format&format=webp align="left")
    
* In the additional section, you can provide a shell script to install docker and Jenkins as pre-requisite to the server.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681614486078/82106ac5-9eaa-4e43-a4d9-56265c3a6b03.png?auto=compress,format&format=webp align="left")
    
* Now click to create a template and then navigate to the Action section to launch an instance out of the created template.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681614657084/5ba53e7e-b4ac-4d59-b3b1-5aac5e871a71.png?auto=compress,format&format=webp align="left")
    
* Provide the desired number of instances as shown.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681614750502/74401283-c446-4012-86a1-1b8a92838824.png?auto=compress,format&format=webp align="left")
    
* Navigate to the instance section in the EC2 dashboard and the instances will be now created. Here we have created 3 instances.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681615023661/e97ea64e-00b7-476b-a862-be9ebf9892d5.png?auto=compress,format&format=webp align="left")
    

# **🌟 Task 2: Create an Auto Scaling group**

* Navigate to the Autoscaling group section and give a name to the group that will be created. Select the template that we have created in the above task.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681615291529/f4b66837-d9c2-433c-985e-e9855bddc24a.png?auto=compress,format&format=webp align="left")
    
* Provide the subnet you want to keep your servers at.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681615669521/5f92129d-5f3e-4163-99ba-1ebacb1b5085.png?auto=compress,format&format=webp align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681625657636/5680d6fb-aeb6-44bd-a02b-9b319b991216.png?auto=compress,format&format=webp align="left")
    
* Provide the desired capacity and maximum capacity of the group to create servers.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681626009721/2a888a44-9a76-499b-8086-8cb502e0257d.png?auto=compress,format&format=webp align="left")
    
* Review and now create the group.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681626282613/e628d07e-cc05-4141-8805-d3f17e0df128.png?auto=compress,format&format=webp align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681626408124/a5941d26-0565-4376-b54c-0a9a77598270.png?auto=compress,format&format=webp align="left")
    
* Now, navigate to the instance section and you can see 6 servers.
    
    Out of 6, 3 servers were created for above task 1 and the rest 3 are spun up by the Auto-Scaling group as the desired field we gave is 3.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681626653826/a7136c53-80aa-452c-92ba-3205734d5918.png?auto=compress,format&format=webp align="left")
    

# **🌟**Conclusion:

In this article, we learn how to use a shell script to install docker, Jenkins in your instance automatically. By using the script we save some more time and increase efficiency. To scale up your instances you use autoscaling, which provides high availability, fault tolerance, managing different types of workloads and many more.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.

#aws #EC2 #autoscaling #DevOps #TrainWithShubham #cloudcommunity

#90daysofdevops #devopscommunity #happylearning

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)