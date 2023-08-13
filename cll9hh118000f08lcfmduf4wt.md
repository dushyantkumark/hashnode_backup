---
title: "AWS PROJECT: Setup VPC  with Public - Private Subnet in Production"
datePublished: Sun Aug 13 2023 13:30:18 GMT+0000 (Coordinated Universal Time)
cuid: cll9hh118000f08lcfmduf4wt
slug: aws-project-setup-vpc-with-public-private-subnet-in-production
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691868002069/c8be5afb-7a27-48df-8af9-3f2d7d1559fd.png
tags: aws, devops, vpc, 90daysofdevops, trainwithshubham

---

# **🌟Introduction**

🔥 About the project:

✅ This example demonstrates how to create a VPC that you can use for servers in a production environment.

✅ To improve resiliency you deploy the server in two availability zones by using an auto scaling group and an application load balancer.

✅ For additional security you deploy the server in private subnets. The server receives requests through the load balancer.

✅ The server can connect to the internet by using a NAT gateway. To improve resiliency you deploy the NAT gateway in both availabilty zones.

✅ Run two Python servers to check how the load balancer redirects the traffic on both instances, these instances running in a private subnet.

🔥 Overview:

✅ The VPC has public subnets and private subnets in two availability zones.

✅ Each public subnet contains a NAT gateway and a load balancer node.

✅ The server run in the private subnet are launched and terminated by using an auto-scaling group and receive traffic from the load balancer.

✅ The servers can connect to the internet by using the NAT gateway.

# 🌟Follow these steps to perform this project

## 🔱TASK 1: Setup your VPC

### ✔Step 1: Go to AWS Console and search VPC

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691831475727/566f27d4-b71b-4d37-9848-b32d9fdd3b3e.png align="left")

### ✔Step 2: Create VPC

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691831616873/0ea97574-89ad-40aa-a102-45cfb54648a3.png align="left")

### ✔Step 3: Go with PVC and more.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691831700144/cdee187c-eeb7-4f46-9736-2e973720eedc.png align="left")

### ✔Step 4: Select no of AZ, Public-Private Subnet, Netgateway and VPC endpoint

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691831857336/c750022e-2ab6-40e9-b213-3b79b4aa969e.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691831936120/914195d2-6cba-4f89-b03b-845790e905db.png align="center")

### ✔Step 5: Preview your VPC Flow Diagram

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691832018114/6ab8faad-0b7f-47e2-9130-afd2a11c99dc.png align="left")

### ✔Step 6: Your VPC Workflow

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691832148525/c7073563-4851-4ce0-a0ab-24e36cb60bae.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691832161781/4533285c-eb5e-4bf5-b452-f4bb09c90dc6.png align="center")

### ✔Step 7: Your VPC Final Output

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691832247902/a0fc6442-13db-4953-9834-18e93f93090e.png align="left")

## 🔱Task 2: Create Launch Template before AutoScaling Group

### ✔Step 1: Now click on EC2, and let's go for Auto Scaling group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691833559567/a3180f1e-a136-4f0c-91bf-2c9d6546baf8.png align="center")

### ✔Step 2: Create Launch Template for Auto Scaling group

You just have to mention what is the name of this launch template and after that give the same template version description about it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691833710276/87d05b67-3b43-48b9-b102-a007ad0cf9c2.png align="left")

### ✔Step 3: Select your OS image

Then scroll down to the application and os images (Amazon Machine Image) required and select Browse more AMIs and select Ubuntu.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691833826110/90fded16-32a7-4b5c-93a4-2ae6682a3497.png align="left")

### ✔Step 4: Select your Instance type and Key-pair

Then go to the instance type and select t2.micro free tier eligible. After that select the key pair (login) or you can create new pair.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691833891510/dafdd02c-8d30-48a0-b16b-128d6b13cdd7.png align="center")

### ✔Step 5: Select your Network settings

The next step is the networking setting there is a firewall (security group), select create a security group and provide the name of the security group and give a description.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691834041116/642e4b01-cef9-4562-97d6-ae604089d2eb.png align="center")

### ✔Step 6: Create Security group rules

In the type section, we have to set up inbound security rules such as ssh and in the source type section select anywhere.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691834205700/97af1747-8211-4a33-a709-2fdca939ac4f.png align="center")

### ✔Step 7: Check your Launch Template

click on create launch template and finally, you check your launch template.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691834415287/3d07de4c-7982-401e-9680-9040389b7c6b.png align="center")

## 🔱Task 3: Create AutoScaling Group

### ✔Step 1: Now click on EC2, and let's go for Auto Scaling group

Click on Create an auto-scaling group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691835010805/ecc919f7-d3cc-4169-bcea-c189fce225a7.png align="center")

### ✔Step 2: Choose Launch Template for ASG

Go to the previous tab choose the launch template or configuration and give the name to the auto-scaling group and select the launch template that you just created after that click on next.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691835273430/02c50f51-b56a-4c66-b7f4-b0e8925bd706.png align="center")

### ✔Step 3: Choose instance launch options

Select VPC, private subnet with availability zone.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691835468264/d48f42f6-3115-47ef-a463-116c9ca51871.png align="center")

### ✔Step 4: Configure Advanced options with a health check

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691835598508/8194f3e8-e758-491d-97f3-bd55c0371b6c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691835617863/5441fa7c-be45-400e-87e2-2cf941a29c75.png align="center")

### ✔Step 5: Configure group size and scaling policy

In the group size optional section select desired capacity 2 and maximum capacity 4.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691835712963/35ed9ff3-c263-43f2-8a83-ff4e4f11454b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691835728260/4e9c7395-cf83-4743-93fc-033591235f2b.png align="center")

### ✔Step 6: Check your ASG

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691835790032/00f32ef1-e813-46a7-9edf-e8c6982243aa.png align="center")

### ✔Step 7: Two instances running

These two instances are running in a private subnet with a private ipv4 address.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691836380117/ff005c5f-c9bc-4c0d-a883-87b03559b535.png align="center")

## 🔱Task 4: Create Bastion/Jump (Server or Host) and Run Python Server on Private Subnet Instance -1

### ✔Step 1: Now launch a Bastion host

Select an instance type (t2.micro) and key-pair.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691836369368/50ade946-3e26-4c80-9eef-8d939bf75154.png align="center")

### ✔Step 2: Select your Network settings

The next step is the networking setting there is a firewall (security group), select create a security group and provide the name of the security group and give a description.

Select the vpc you create, a public subnet with an availability zone, enable auto-assign public IP, etc.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691836578505/a9f9af7d-87c9-448d-b085-e863bdf54105.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691836733030/12e562f0-8f27-4157-bcbf-00590ecb060f.png align="center")

### ✔Step 3: SCP a private key of a private subnet instance

Use this command to copy a private key (ex key. pem) of a private subnet instance, and copy this private key to the bastion host/machine/server.

```plaintext
scp -i <path_with_bastion-host_key> <path_with_private-subnet-instance_key> user_name@<public-ip-bastion-host>:/home/ubuntu
```

### ✔Step 4: SSH Bastion Host/Server

```plaintext
ssh-i <path_with_bastion-host_key> user_name@<public-ip-bastion-host>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691837440471/878b6b3c-aa00-4c5f-9bee-105e9beb3559.png align="center")

### ✔Step 5: SSH Private Subnet Instance

```plaintext
ssh-i <path_with_private-subnet-instance_key> user_name@<private-ip-private-subnet-instance>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691837755318/1bc0540f-d2a2-4fb2-a257-b49b64ee57d5.png align="center")

### ✔Step 6: Checking Connectivity of Private Subnet Instance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691837834788/55f0ef43-d65e-409e-9f54-54d077e4753b.png align="center")

### ✔Step 7: Setup Python HTTP Server

After that create a file in the terminal vim index.html and run the following command.

```plaintext
<!DOCTYPE html>
<html>
<body>

<h1>My MY AWS VPC Project in private subnet ap-south-1a</h1>

</body>
</html>
```

```plaintext
python3 -m http.server 8000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691838154510/4bcfa7e9-0a78-401c-a7f4-8e8939a3f4cc.png align="center")

## 🔱Task 5: Create a Load Balancer

### ✔Step 1: Select which type of LB you want

Search ec2 and scroll down and select the load balancer. click on an application load balancer and click on create button.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689250722613/d85bb0f7-1b53-499d-8122-0c5c108aa796.png?auto=compress,format&format=webp align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691838395927/e567563f-a043-4cce-a8e4-a4ec3b820cea.png align="center")

### ✔Step 2: Enter basic configuration

After that in basic configuration go to the load balancer name and provide a name.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691838667702/fdb4969f-0f27-4bd2-bb8d-dc95786df7ea.png align="left")

### ✔Step 3: Network Mapping

Go to the network mapping section and in that select the vpc that you have just created. Select both the availability zones it should be public.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691838750582/e9b5ec48-f2a7-4763-9fe6-0fd7390a6d69.png align="left")

### ✔Step 4: Add Security Group and Listeners

Go to the security groups section and select the security groups that you just created, listeners and routing section.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691838801746/4c90d9c3-c136-4d38-8c00-4b1b7070b6e8.png align="center")

### ✔Step 5: Create a Target Group

Go to the target group name and provide a group name and select port 8000 with a health check.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691839094240/85f55bc5-ddc9-49d0-9afd-6f1352209952.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691839252428/a9d4fef8-aa6d-4f4c-b774-5b646cd91acf.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691839264938/4a497316-eeaa-4b8f-8c91-66ca178a83f8.png align="center")

In available instances and select two instances that you created do not select bastion-host instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691839278538/6e19417a-6dbe-4478-bade-c98aec948421.png align="center")

### ✔Step 6: Check Target Group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691839409081/10976647-4d7b-4673-a3f6-8b273f1620d7.png align="center")

### ✔Step 7: Check the Load Balancer

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691841172451/6d72feb6-1bb7-44f7-a540-a74e68bbdd0e.png align="center")

### ✔Step 8: Troubleshooting Listener Error

Go to the security group and click on the security group id.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691839728490/d653ab51-93ed-4f17-a2a3-145b23bf6e34.png align="center")

### ✔Step 9: Solved Listener Error

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691841189131/07985ab4-ff0b-4b64-ab9e-255fef63e03c.png align="center")

### ✔Step 10: Access your Private Subnet Instances

Then copy this DNS name and search in your browser.

SERVER 1 OUTPUT

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691840055234/d3f67b9d-d5ba-433b-95f0-91accabe81be.png align="center")

SERVER 2 OUTPUT

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691840081635/ce222261-51cf-4ff8-a668-b3209a3d0be9.png align="center")

## 🔱Task 6: Setup Server 2 in Private Subnet (ap-south-1b)

Repeat TASK 4 (Create Bastion/Jump Server in the public subnet of ap-south-1b).

### ✔Step 1: SCP a private key of a private subnet instance

Use this command to copy a private key (ex key. pem) of a private subnet instance, and copy this private key to the bastion host/machine/server.

```plaintext
scp -i <path_with_bastion-host_key> <path_with_private-subnet-instance_key> user_name@<public-ip-bastion-host>:/home/ubuntu
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691840464540/7f2d5b8f-cb0f-44b1-8ce4-f49484716f03.png align="center")

### ✔Step 2: SSH Bastion Host/Server

```plaintext
ssh-i <path_with_bastion-host_key> user_name@<public-ip-bastion-host>
```

### ✔Step 3: SSH Private Subnet Instance

```plaintext
ssh-i <path_with_private-subnet-instance_key> user_name@<private-ip-private-subnet-instance>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691840519586/44b4a6af-d2c4-4c55-b3b7-73c926711407.png align="center")

### ✔Step 4: Checking Connectivity of Private Subnet Instance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691840534687/5073fd06-cf58-435c-9a65-b72eeeb57d00.png align="center")

### ✔Step 5: Setup Python HTTP Server

```plaintext
<!DOCTYPE html>
<html>
<body>

<h1>MY AWS VPC Project in private subnet ap-south-1b</h1>

</body>
</html>
```

```plaintext
python3 -m http.server 8000
```

## 🔱Checking Output of Both the Servers

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691840690804/7434d4e5-92d6-4ffe-b761-28edd13fc0f3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691840703160/257caf70-29e0-4c9b-b2a8-a6a8bdde5de8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691840721314/7877d27c-d007-4ae7-a59e-4585ce6f9e80.png align="center")

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.😊

#cloud computing #aws #vpc #Devops #TrainWithShubham #90daysofdevopsc #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)