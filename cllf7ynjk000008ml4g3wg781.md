---
title: "AWS PROJECT: Seamlessly Set Up and Access Your Private RDS Instance via the Jump Box!""
datePublished: Thu Aug 17 2023 13:50:41 GMT+0000 (Coordinated Universal Time)
cuid: cllf7ynjk000008ml4g3wg781
slug: aws-project-seamlessly-set-up-and-access-your-private-rds-instance-via-the-jump-box
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692256313467/579303d5-e0c3-41e0-979a-eca5ea03659d.png
tags: aws, devops, aws-rds, 90daysofdevops, trainwithshubham

---

# **🌟Introduction:**

In today's technology-driven landscape, efficient management of databases is crucial for the success of any modern application. As a DevOps engineer, I'm excited to introduce a new AWS project that focuses on architecting a robust and secure database infrastructure. In this project, we will be leveraging Amazon Web Services (AWS) to create a Relational Database Service (RDS) instance within a private subnet. To access this RDS instance securely, we will implement a Jump Box (also known as a Bastion Host) that acts as an intermediary between the private subnet and external connections. If you want to know more about RDS you can follow this link.

[RDS\_LINK](https://dushyantkumark.hashnode.dev/amazon-relational-database-service-rds-a-beginners-guide)

# **🌟Project Overview:**

Our primary objective is to design a highly available and secure environment for our application's database. To achieve this, we will adhere to the following key principles:

1. **<mark>Private Subnet Isolation</mark>:** We will place the RDS instance within a private subnet. This isolation ensures that the database is shielded from direct external access, mitigating potential security threats.
    
2. **<mark>Jump Box as Access Point</mark>:** To interact with the RDS instance securely, we will deploy a Jump Box instance within a public subnet. The Jump Box will serve as a gateway through which authorized users can access the private subnet.
    
3. **<mark>Security Groups and Network ACLs</mark>:** We will employ AWS Security Groups and Network Access Control Lists (ACLs) to control inbound and outbound traffic. This helps us maintain granular control over who can access the RDS instance and the Jump Box.
    

## **🔱**Benefits

By implementing this project, we aim to achieve enhanced security, performance, and management of our application's database. The private subnet isolation ensures that sensitive data is shielded from unauthorized access, while the Jump Box provides a secure gateway for legitimate users to interact with the database. Additionally, the use of AWS services such as RDS, VPC well-architected solution.

Stay tuned as we dive deeper into each step of the project, providing detailed instructions and insights into the decision-making process. This project exemplifies our commitment to embracing industry best practices in DevOps and AWS architecture to build reliable and secure solutions for our applications.

## **🔱Prerequisite :**

Here are some prerequisites for this project are given below:

* Linux
    
* Any Cloud Provider in my case, I am using AWS.
    
* AWS VPC
    
* AWS EC2
    
* AWS RDS
    

# **🌟Follow these steps to perform this project**

## **🔱TASK 1: Setup your VPC**

### **✔Step 1: Go to AWS Console and search VPC**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691831475727/566f27d4-b71b-4d37-9848-b32d9fdd3b3e.png?auto=compress,format&format=webp align="left")

### **✔Step 2: Create Private Subnets**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692249774141/1d2280fb-d681-4ef6-8689-fc48600d95ff.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692249788754/4a3d7224-32a3-4aeb-87ff-62aa0017c849.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692249802885/d82df5b6-9e62-4965-8f6f-355b5c650251.png align="center")

### **✔Step 3: Create New Route Table**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692249940169/9aad4863-7ade-4591-a0e7-5538c219dad9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692249983023/286c4f06-5f11-421c-83b2-e566ebbeed84.png align="center")

### **✔Step 4: Subnet Associations**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692250014614/bbf647c6-7f0d-4d0a-a40f-dba53feb704c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692250197562/80574997-6e4c-40d8-a6de-37c0f0bc8cd4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692250212455/79a586fb-68c3-4ca0-9b82-0b5c95c7dd8c.png align="center")

### **✔Step 5: Your Route Table**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692250224155/fbb91b13-fa49-492e-b3be-a26af7e28288.png align="center")

## **🔱TASK 2: Setup your RDS**

### **✔Step 1: Go to AWS Console and search RDS**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692250629180/50c1eec6-964f-4491-8084-429258f18d08.png align="left")

### **✔Step 2: Create a Database subnet group**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692250639462/ff868d2e-f3b3-42f2-aea2-c2bd3e3e2a97.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692250673827/5a4e49ce-5c5d-4ee9-82a2-3f0305ada7e5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692250686407/72b6a8af-9cbe-4ae2-accb-fed3e00b7dda.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692250701268/aefc08a3-7fa5-46b3-94d9-00cc9348a230.png align="center")

### **✔Step 3: Create a Database**

Navigate to the RDS section in the AWS management console and click Create a database.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251032103/39ea4f73-e9d1-4d20-832e-c847fd4362d4.png align="center")

### **✔Step 4: DB creation method**

Select the database creation method you want. Standard creation or Easy Create.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251049791/d9e8b4a2-53d5-4632-9013-da059af42d42.png align="center")

### **✔Step 5: Choose the Engine Option**

Select the database engine you want to use. RDS supports various engines like MySQL, PostgreSQL, SQL Server, Oracle, etc.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251064523/2a00bc27-dfd5-4615-9fc3-c2b70c7000fe.png align="center")

### **✔Step 6: Select a specific engine version**

Choose the engine version for your use case.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251078330/524cc66e-ee0f-4fa3-873d-a59cc0640f6d.png align="center")

### **✔Step 7: Choose the Templates**

Choose the appropriate use case template. This could be Production, Dev/Test, Free tier, etc.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251098370/8007e214-7c4c-4c42-8d4d-04cc063cf5a1.png align="center")

### **✔Step 8: Database Settings**

Connectivity: Set the DB instance identifier, master username, and password.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251124476/3118e718-a2e5-43db-85ec-fb10bd998160.png align="center")

### **✔Step 9: Instance Configuration**

DB Instance Class: Select the compute and memory capacity.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251153336/4bf80df3-d964-41af-94e5-70b74745141c.png align="center")

### **✔Step 10: Storage Configuration**

Storage: Specify the allocated storage space.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251200798/a12785af-8d37-455e-a0f8-e5428236a1bd.png align="center")

### **✔Step 11: Network Configuration**

Virtual Private Cloud (VPC): Choose an existing VPC or create a new one.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251240783/6c77fa1e-315b-46d4-8738-b17090c671ac.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251267100/d136fd34-afd3-4b4c-b9fb-e5f4cd870a1c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251305268/dba8bc47-2292-45c0-8f62-952da65d5fdf.png align="center")

### **✔Step 12: Additional Configuration**

Additional Configuration: Configure advanced settings like backup retention, maintenance window, etc.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251327281/23d6ed5d-65de-406d-9cfa-c7c4498370e0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251362219/babd4e62-8bd0-45f8-b773-d9029f5c5adb.png align="center")

### **✔Step 13: Your Database Created Successfully**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692251461239/552fb6b5-e941-4b37-8772-f392e954f926.png align="center")

## **🔱TASK 3: Setup your Jump Box**

### **✔Step 1: Go to AWS Console and search EC2**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692250629180/50c1eec6-964f-4491-8084-429258f18d08.png align="left")

### **✔Step 2: Click on the launch instance**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253129955/35c7c2e1-27db-4f3e-ba2c-4381b5d624b0.png align="center")

### **✔Step 3: Give a name to your instance(jump\_box)**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253146155/f6eea61d-a5f8-4c50-87e5-ce82ca97c1c7.png align="center")

### **✔Step 4: Choose your OS image, AMI and Architecture**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253159934/a59684f6-9b73-4c59-b98a-da8751c370f6.png align="center")

### **✔Step 5: Choose your instance type and create new key-pair**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253174090/0ada085d-d954-461b-ae58-700f06d03b92.png align="center")

### **✔Step 6: Configure your network settings**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253190453/50b16204-4dbd-4c17-aae1-85e2ab5c14a0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253206333/940790ed-dfd1-4454-9645-0dd2f4a87b26.png align="center")

### **✔Step 7: Configure your storage and launch instance**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253220706/4255ac62-a4a7-4a72-93e9-89a51bf0e81a.png align="center")

### **✔Step 8: Your instance is up and running**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253284853/6605faf2-2d16-4f4c-89d7-4ba23bbaa06a.png align="center")

## **🔱TASK 4: Connect your RDS instance using Jump Box**

### **✔Step 1: Your Jump Box inbound rules**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253413784/9a855304-5c03-457a-99c4-301f0ee4e946.png align="center")

### **✔Step 2: Your Database inbound rules (at the time of db creation)**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253466344/c19d1ed3-fc42-4101-a7b1-b19c280755d7.png align="center")

### **✔Step 3: Modify your Database inbound rules**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253490785/38fba9bc-a4c4-44ca-bcec-71c4ce7ea7f4.png align="center")

### **✔Step 4: SSH your jump box**

```plaintext
ssh -i "jump-box.pem" ubuntu@<public_dns>
or
ssh -i <"key_name"> <user_name>@<public-ip>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253506371/24857102-fe0e-413f-9623-0e32efa152de.png align="center")

### **✔Step 5: Install my-SQL client 8.0**

```plaintext
sudo apt install mysql-client-core-8.0
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253518919/47fbec09-6d8a-41da-87b4-3ae80c2400ec.png align="center")

### **✔Step 6: Setup connection with Database**

```plaintext
mysql -h <enpoin_tURL> -P <port_no.> -u <user_name> -p
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253534946/e66ff28e-35f7-4603-b442-16b2a97b65f2.png align="center")

### **✔Step 7: Play with your Database**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692253546554/00c2199f-411e-4085-ab80-79a399a3a53d.png align="center")

# **Conclusion:**

In this AWS project, we have established a secure database infrastructure with RDS in a private subnet, enhanced by a strategic Jump Box. Our design balances robust security and easy access, safeguarding the database while enabling authorized interaction. By isolating RDS, we've ensured data security and compliance, while the Jump Box serves as a controlled gateway. This project underscores the value of thoughtful architecture, integrating AWS components like VPCs, Security Groups, As DevOps engineers, we're architects of secure solutions, committed to innovation. This achievement exemplifies our dedication to excellence and our readiness to adapt to technology's evolving landscape.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.😊

#cloud computing #aws #rds #Devops #TrainWithShubham #90daysofdevopsc #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)