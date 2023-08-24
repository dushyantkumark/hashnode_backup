---
title: "Configuration Management using Ansible! 🤖🔗📚"
datePublished: Tue Aug 22 2023 15:23:36 GMT+0000 (Coordinated Universal Time)
cuid: cllmghdyt000w09mp1vaactad
slug: configuration-management-using-ansible
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692697451757/ec991a08-2fa5-46e7-b012-af2bea43d5df.png
tags: aws, ansible, devops, 90daysofdevops, trainwithshubham

---

# **🌟 What is Ansible?**

* **Ansible** is a software tool that provides simple but **<mark>powerful automation</mark>** for **cross-platform computer support**. It is primarily intended for **IT professionals**, who use it for **application deployment**, **updates on workstations and servers**, **cloud provisioning**, **configuration management**, **intra-service orchestration**, and nearly anything a systems administrator does on a weekly or daily basis.
    
* **Ansible** doesn't depend on agent software and has **<mark>no additional security infrastructure</mark>**, so it's **easy to deploy**.
    

# 🌟 How Ansible Works?

* **Ansible** works by **<mark>connecting to nodes</mark>** (**clients**, **servers**, or whatever you're `configuring`) on a **network**, and then sending a small program called an **<mark>Ansible module</mark>** to that node. **Ansible** executes these modules over SSH and removes them when finished.
    
* **SSH keys** are the most common way to provide access, but other forms of **<mark>authentication</mark>** are also supported.
    

## 🔱 Ansible Architecture: Nodes and Modules

* **Ansible's Architecture** is based on the concept of a **control node** and a **managed node**. The platform is executed from the <mark>control node</mark> where a user runs the **<mark>ansible-playbook</mark>** command. There must be at least one `control node`; a backup control node can also exist. The devices being automated and managed by the control node are known as **managed nodes**.
    
* **Ansible** automates **<mark>Linux</mark>** and **<mark>Windows</mark>** by connecting to managed **nodes** and pushing out small programs called **<mark>Ansible modules</mark>**. **Ansible** executes these `modules`, which are the resource models of the desired system state, over **Secure Socket Shell (SSH)** by default and `removes` them when finished.
    
* Ansible modules are written in **<mark>Python</mark>** and can be written in any language. `Ansible` modules are reusable, standalone scripts that can be used by the **<mark>Ansible API</mark>**, **<mark>Ansible Playbooks</mark>**, or **<mark>Ansible Galaxy</mark>**.
    

## 🔱 Create **4 Instances on AWS EC2** with the following names:

* ***Ansible\_Master***
    
* ***Server\_1***
    
* ***Server\_2***
    
* ***Server\_3***
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692687786817/e0ac08e3-3679-4f4b-9c12-fdaac6c214be.png align="left")

---

# 🌟**Follow these steps to perform this project**

## 🔱TASK 1: Create Ansible Master Server

### ✔Step 1: Go to AWS Console and search EC2

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692688104039/f0948ee0-9272-4828-a18b-eb6179a23a9a.png align="center")

### ✔Step 2: Select your OS image and Instance Type

You just have to mention what is the name of your server (Ansible\_Master), after that select the type of OS image and number of instances.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692688157837/f34f130f-95ae-4efd-a8be-6415291f9129.png align="center")

### ✔Step 3: Select your Instance type and Create a new Key-pair

Then go to the instance type and select t2.micro free tier eligible. After that select the key pair (login) or you can create a new pair.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692688754169/832858bd-b96f-4ace-be48-f7b3121317a1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692688412853/744b04e2-bf93-486d-bcf8-1d6316360af5.png align="center")

### ✔Step 4: Configure your Network settings and Storage

The next step is the networking setting there is a firewall (security group), select create a security group provide the name of the security group and give a description. Configure the ebs volume storage.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692688525396/1d4462f9-1df0-4f5e-a42a-4e5fdf8916de.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692688566873/2c8e51e7-d26c-4ecf-bab6-5edd35775e3b.png align="center")

## 🔱TASK 2: Create Ansible Node Servers

### ✔Step 1: Go to AWS Console and search EC2

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692688104039/f0948ee0-9272-4828-a18b-eb6179a23a9a.png align="center")

### ✔Step 2: Select your OS image and Instance Type

You just have to mention what is the name of your server (Ansible\_Master), and after that select the type of OS image and number of instances.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692688950885/f9f67b09-951a-4830-9865-856318e204f8.png align="center")

### ✔Step 3: Select your Instance type and Create a new Key-pair

Then go to the instance type and select t2.micro free tier eligible. After that select the key pair (login) or you can create a new pair.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692688754169/832858bd-b96f-4ace-be48-f7b3121317a1.png align="center")

### ✔Step 4: Configure your Network settings and Storage

The next step is the networking setting there is a firewall (security group), select create a security group and provide the name of the security group and give a description. Configure the ebs volume storage.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692688983640/eff2cf28-9292-4843-9e17-633fa3d23400.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692688566873/2c8e51e7-d26c-4ecf-bab6-5edd35775e3b.png align="center")

## 🔱TASK 3: Installing Ansible in Ansible Master Server

### ✔Step 1: SSH your Ansible Master EC2 Instance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692689148641/e49fed0f-a702-4b0d-bc78-24fdfcf3bd13.png align="center")

### ✔Step 2: Install Ansible in the Master Server and Check the Version

* Open **Ansible\_Master\_Server** and run the following commands or create a script for it:
    

```plaintext
#!/bin/bash
sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible
```

* Attach permissions to the script and run it:
    

```plaintext
sudo chmod 700 install.sh
sudo ./ansible_install.sh
```

* Check the **Ansible** version
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692689592835/34670352-b7a6-4b6f-a69d-2b488c2d1134.png align="center")

## 🔱TASK 4: SCP Private Key file for Node Servers

### ✔Step1: SCP Private Key file of Node Server to Ansible Master Server

I am using ansible-key.pem file for an ansible master server and node servers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692690415652/fddc17f2-e6ae-4905-8865-ac7fb4890e35.png align="center")

## 🔱TASK 5: Ansible Host files

### ✔ What is a Host file?

* In the context of **Ansible**, a `host file` (also known as an **inventory file**) is a `configuration file` used to define and organize the list of **target hosts** that **Ansible should manage**.
    

### ✔ Where is the Host file located?

* **Ansible** uses this file to map **target hosts** to **managed nodes**. The **host's file** is usually located in `/etc/ansible/hosts`.
    
* So, open the **host's** file and add the **IP addresses** of the **Nodes**:
    

```plaintext
sudo vim /etc/ansible/hosts
```

### ✔Step1: Add Node Server IP Addresses

Let's add the **Node** **IP addresses** in the **host's** file:

```plaintext
[servers]
Server_1 ansible_host= <Public IP-Adddress of Node-1>
Server_2 ansible_host= <Public IP-Adddress of Node-2>

[servers:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_ssh_private_key_file=/home/ubuntu/.ssh/id_rsa
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692691031462/92f0b5a7-7ab4-4c97-963b-4166cdc67e7e.png align="center")

### ✔Step2: **Try a ping command using Ansible to the Nodes**

We use the following commands to check connectivity between the master server and node servers.

```plaintext
ansible servers -m ping
# ansible is the command line utility used to interact with remote servers
# servers is a group name we created for node servers, shown above
# -m is the module
# ping is the name of module
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692691733628/88140d00-ab7d-4f38-9586-6523c4e53e2a.png align="center")

### ✔Step3: **Testing Linux commands (ad hoc commands)**

We use the following commands to check the memory and disk space of remote servers.

```plaintext
ansible servers -a "free -h"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692691936793/6d29e482-e202-4ae3-a32d-9c929a8cdc64.png align="center")

```plaintext
ansible servers -a "df -h"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692692175888/e7e35318-9444-499c-91a0-ec37514d7355.png align="center")

We have Pinged **Server\_1**, **Server\_2 and Server\_3** from **Ansible\_Master**.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.😊

#aws #cloudcomputing #ansible #configurationmanagement #Devops #TrainWithShubham #90daysofdevops #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)