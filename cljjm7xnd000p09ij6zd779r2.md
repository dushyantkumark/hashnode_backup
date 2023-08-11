---
title: "A Comprehensive Guide to Getting Started with Amazon EC2 - [ LAUNCH YOUR FIRST EC2 INSTANCE ]"
datePublished: Sat Jul 01 2023 06:21:29 GMT+0000 (Coordinated Universal Time)
cuid: cljjm7xnd000p09ij6zd779r2
slug: a-comprehensive-guide-to-getting-started-with-amazon-ec2-launch-your-first-ec2-instance
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1688192407364/823e5c74-5691-4f4a-bd68-8ff55e698aec.png
tags: cloud, ec2, aws, 90daysofdevops, trainwithshubham

---

### **What is AWS EC2 service?**

Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides scalable computing capacity in the cloud. It aims to simplify web-scale cloud computing for developers. With EC2, you can easily launch virtual machines (VMs), also known as instances, with different operating systems and configurations. You have the flexibility to start as many or as few virtual servers as you need, configure networking and security settings, and manage storage. One of the key advantages of EC2 is its ability to scale resources up or down based on your application's demands, allowing you to only pay for the resources you use. This versatility has made EC2 a popular choice for a wide range of applications, from simple websites to complex, data-intensive programs.

***in the story version:***

A business wants to reach more people online and increase its internet visibility. Though building and operating actual servers was expensive, time-consuming, and difficult, they realized they needed to construct more servers to manage the rising traffic.

At that point, they learned about the web service Amazon Elastic Compute Cloud (EC2), which enables them to quickly launch virtual servers, also known as instances, in the cloud. The organization was able to immediately launch as many servers as they required, in a matter of minutes, thanks to EC2. They could select the ideal setup for their particular application from a multitude of configurations and operating systems.

The business could quickly scale up or down the number of servers using EC2 by their traffic, so they only paid for what they needed. The nicest aspect was that EC2 took care of all the complicated networking and security issues, so they could concentrate on creating and running their application.

The business was able to handle the growing demand for its website and accomplish its aim of growing its online presence because of EC2. They continued to prosper and serve their clients effectively as they lived happily ever after.

# **How AWS EC2 works?**

It’s like having your cloud genie with AWS EC2, or Amazon Elastic Compute Cloud. It’s a service that enables you to build up “virtual servers” that you can use and manage just like real, physical servers, but without the effort of actually configuring and maintaining physical hardware.

Think of it as building and configuring virtual blocks, where each block represents a virtual server. You have the freedom to connect these blocks to form a complete system, much like playing with virtual Legos. The beauty is that you can easily disassemble and reassemble these blocks, just like Legos, providing you with unparalleled flexibility in managing your infrastructure.

Here’s how it works in a nutshell:

1. You can select the size, memory, and processing power of the virtual server (often referred to as an “instance”), as well as its configuration.
    
2. You decide which software and operating system you want to install on your server.
    
3. As if it were a real, physical server located in a data center, AWS configures your virtual server and grants you access to it.
    
4. Afterward, you may access, customize, and utilize your server just like you would a real one, but AWS will handle all of the underlying hardware and upkeep.
    
5. The best aspect is that, in contrast to managing physical servers, you only pay for the resources and time that you utilize.
    

Overall, EC2 makes it easy to create your virtual servers and to be flexible with your scaling and resources as needed.

# **AWS EC2 architecture :**

Scalable, on-demand computing resources are made available to customers through the AWS EC2 (Amazon Elastic Compute Cloud) architecture. The architecture comprises the following elements:

1. Regions and Availability Zones: Multiple geographic regions with numerous availability zones make up AWS (AZs). Each region has numerous AZs, which are isolated areas within a region that is designed to be highly available and fault-tolerant. A region is a geographical location (such as US East (N. Virginia)). Customers can do this to launch resources in different places for redundancy and to lessen the effect of outages.
    
2. Virtual Private Clouds (VPCs): Your EC2 instances and other resources can be launched in a VPC, which is a virtual network. Among other things, you can set up security groups, build subnets, and give your instances IP addresses. Your instances can run in a private, secure environment thanks to VPCs.
    
3. EC2 instances: The virtual servers that can be started in a VPC are as follows. There are various instance sizes and types available, each with varying CPU, memory, and storage capacities. A private IP address is given to EC2 instances when they are launched into subnets inside of a VPC.
    
4. Elastic Block Store (EBS): Block-level storage is provided via EBS for EC2 instances. You can retain data even after an instance has been terminated because it offers persistent storage for instances. To safeguard data from errors, EBS volumes are automatically replicated within their availability zone.
    
5. Elastic IP addresses: You can give them static, public IP addresses to your instances. By quickly remapping the address to another instance in your VPC, they enable you to hide the failure of software or instance.
    
6. Auto Scaling: provides you with the option to automatically adjust the number of instances in an Elastic Compute Cloud (EC2) Auto Scaling group in response to variations in application demand.
    
7. Elastic Load Balancing: automatically spreads out incoming website traffic among numerous Amazon EC2 instances.
    

Together, these elements enable the provision of a scalable and adaptable computing environment for users. Customers may simply launch and manage virtual servers, set up networking and security settings, and store and retrieve data thanks to the EC2 service. All of this is accomplished by abstracting the complexity of the underlying hardware and maintenance, giving clients the ability to dynamically scale resources by demand and budget.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686391101895/7285e6f8-1f17-4f1b-9ce5-d3f0d6f68e7c.png?auto=compress,format&format=webp align="left")

# **What are the benefits of AWS EC2?**

Customers can gain from using AWS EC2 (Amazon Elastic Compute Cloud) in several ways.

1. **Scalability**: With EC2, you can quickly adjust the size of your computing resources to meet the demands of your application. Depending on your traffic, you can change the number of instances you’re running and only pay for what you utilize.
    
2. **Flexibility**: A broad variety of instance types, operating systems, and customizations are available using EC2. This enables you to choose the ideal solution for your particular application, whether it’s a straightforward website or a sophisticated, data-intensive program.
    
3. **Cost-Effectiveness**: Using EC2 can be substantially less expensive than operating your physical servers because you only pay for the resources and time that you utilize. You can further cut the cost of running your instances by using services like Reserved instances, Spot instances, and Savings plans.
    
4. **High availability**: Your EC2 instances are redundant and high availability because they are deployed across different Availability Zones (AZs) in a region. This makes it possible to guarantee that your application is always accessible, even if one or more AZs experience an out
    
5. **Security**: To assist safeguard your instances and data, EC2 offers several security features, including security groups and network access control lists. To give your instances a secure environment, it also connects with other AWS services like Amazon Virtual Private Cloud (VPC) and AWS Identity and Access Management (IAM).
    
6. **Elastic load balancing** is a feature of EC2 that makes it simple to divide incoming traffic among several instances, enhancing the performance and availability of your application.
    
7. **Auto Scaling**: EC2 offers the capability of auto-scaling, which dynamically modifies the number of instances in response to variations in demand for your application. This function helps to automatically scale resources based on actual consumption and save money on instances that are not required.
    
8. **Integration with other AWS services**: To offer a comprehensive, end-to-end solution for your application, EC2 instances may simply interface with other AWS services like Amazon S3, Amazon RDS, and Amazon DynamoDB.
    

Overall, EC2 offers users a safe and dependable infrastructure along with a flexible, scalable, and affordable way to execute their applications and meet their computing needs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686391133993/be4c51f2-0aac-482c-b726-f7e118be9898.png?auto=compress,format&format=webp align="left")

# **AWS instances Types:**

Depending on the demands of your workload, you can select from a variety of EC2 instances:

1. **On-Demand instances**: With these instances, you can pay for compute capability on an hourly basis without making an advance purchase. For consumers who don’t want to make an upfront payment or commit to a lengthy contract but still want the affordability and flexibility of Amazon EC2, this is a suitable choice.
    
2. **Reserved instances**: These instances offer sizable savings (up to 75%) compared to On-Demand instances, but a one-time upfront purchase and a one- or three-year term commitment are necessary. Users who have a steady state or predictable consumption are best suited for this choice.
    
3. **Spot instances**: With these instances, you can place a bid for unused Amazon EC2 processing power. This is a wonderful choice for customers who can have unpredictable start and end times.
    
4. **Dedicated Hosts**: By enabling you to use your current server-bound software licensing, these instances let you operate your instances on a dedicated host, which can cut costs.
    
5. **Dedicated instances** are the ideal option for regulatory requirements that might not permit multi-tenant virtualization because they run on single-tenant hardware.
    
6. **Burstable Performance Instances** (T3) are an economical choice for workloads that do not demand continuous high CPU performance because they are made to balance compute, memory, and network resources.
    
7. **Memory-optimized instances** (R4, R5, etc.) are built for memory-intensive applications including high-performance databases, distributed memory caches, and in-memory data stores.
    
8. **Accelerated Computing Instances** (P3, P2, G3, etc.): These instances offer access to hardware-based compute accelerators, such as Graphics Processing Units (GPUs) and Field-Programmable Gate Arrays (FPGAs), to carry out computationally intensive operations.
    
9. The ARM architecture, which is different from the x86 used by the majority of EC2 instances, is used by instances of this type. Although ARM instances cost less than conventional x86 instances, they perform worse, are only offered in a limited number of locations, and have fewer readily available AMIs.
    

There is a lot of overlap in the use cases that each of these instance types can be applied to, but they all have different configurations and can be chosen based on your workloads and requirements. By choosing the proper instance type, you can drastically cut your costs while maintaining the performance of your workload.

# **Start Your First EC2 Instance**

The precise procedures to start an “EC2 instance,” or virtual server, in the Amazon Web Services (AWS) cloud:

1. Visit AWS and Access the AWS Management Console by logging in.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688189554532/46d01167-9c63-4f20-b9be-641d68209f38.png align="center")
    
2. Select “EC2” from the “Compute” menu’s drop-down list.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688162702815/ddf54b48-dce0-4860-95ef-05f2e11b7db1.png?auto=compress,format&format=webp align="left")
    
3. To begin launching a new virtual server, click the “Launch Instance” button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688191216659/41060300-a160-4fea-9883-69c89f295dfc.png align="center")

1. You can give a name to your server, ec2 instance example "docker-server".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688191280074/3853d328-f66a-4648-ab5e-a0ebdf451131.png align="center")
    
    1. The operating system and applications you wish to utilize on the virtual server should be represented by an Amazon Machine Image (AMI), so choose one of those.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688191320352/3c519ff1-a453-4ab7-a644-b950731592ab.png align="center")
    
    1. Select an instance type that outlines your instance’s hardware specifications, such as the number of virtual CPUs, RAM and then the Key pair name.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688191336165/7fcf7884-76db-4894-94de-daf44d43e2b6.png align="center")

1. Create your Key Pair name example "docker"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688191379622/cf0d444d-a6a4-4d3a-a38d-c249406c3a50.png align="center")

1. Set the instance’s parameters, including its number of instances, IAM role, and network configuration
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688191407046/608310bd-1857-4460-80ab-e99f2d0ffb6c.png align="center")

1. Click on Launch Instance, Successfully launched your instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688191424871/a08c012f-de1d-401e-9c7e-c848fa5029ed.png align="center")

1. Click on Instance you see your instance on the dashboard.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688191442911/b7a1bd40-8860-46c8-8897-39fd4e44fa4b.png align="center")

1. Connect your ec2 instance using the ssh command.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688192162769/b4a8341d-d400-456c-a64c-a01a99d3cf54.png align="center")

1. You check your instance detail using the command, for example,
    
    **<mark>curl http://169.254.169.254/latest/meta-data</mark>**
    
    you get your instance detail shown below.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688191514329/66ccabbd-91e7-4079-bd21-3a9ea895a719.png align="center")

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#AWS #cloud computing #ec2 #aws services #TrainWithShubham

#90daysofdevopsc #happylearning

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)