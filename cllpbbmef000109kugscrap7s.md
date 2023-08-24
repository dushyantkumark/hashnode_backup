---
title: "Ansible Project: Website Hosting using  Playbook📚"
datePublished: Thu Aug 24 2023 15:22:27 GMT+0000 (Coordinated Universal Time)
cuid: cllpbbmef000109kugscrap7s
slug: ansible-project-website-hosting-using-playbook
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692875363687/71d96621-b0ac-4c03-8c9e-48d5741b8d1f.png
tags: aws, ansible, devops, ansible-playbook, trainwithshubham

---

# **🌟 Introduction**

Automation is at the heart of modern DevOps practices, and Ansible has emerged as a powerful tool for streamlining server configuration, deployment, and management. In this blog, we'll walk you through the process of creating your first Ansible playbook step by step. By the end, you'll be well on your way to automating tasks and hosting website or infrastructure management more efficiently.

## **🔱Prerequisites**

Before we dive into creating your first Ansible playbook, make sure you have the following:

* **Servers setup:** If you do not set up the Ansible master server with different node servers and you haven't installed Ansible yet, refer to our [CLICK\_ON\_THIS\_LINK](https://dushyantkumark.hashnode.dev/configuration-management-using-ansible) for installation instructions.
    

**Target Server:** You should have a remote server (physical or virtual) where you want to apply your playbook. Make sure you have SSH access to this server.

## **🔱**Ansible Playbook

Playbooks are Ansible's configuration, deployment, and orchestration language. Written in YAML format, playbooks define a series of tasks to be executed on specific hosts or groups. Each task is associated with a module and contains the desired state that Ansible will ensure on the target systems. Playbooks enable IT teams to automate complex workflows, making them highly valuable for repetitive or multi-step processes.

# **🌟Follow these steps to perform this project**

If you want to know how to set up the Ansible master server and node servers follow this link:

[CLICK\_ON\_THIS\_LINK](https://dushyantkumark.hashnode.dev/configuration-management-using-ansible)

## **🔱TASK 1: Ansible Host files**

* **Ansible** uses this file to map **target hosts** to **managed nodes**. The **host's file** is usually located in `/etc/ansible/hosts`.
    
* So, open the **host's** file and add the **IP addresses** of the **Nodes**:
    

```plaintext
sudo vim /etc/ansible/hosts
```

### **✔Step 1: Add Node Server IP Addresses**

Let's add the **Node** **IP addresses** in the **host's** file:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692856523557/7c4bdfe0-fd01-4a7b-983f-cea93c248e7d.png align="center")

### **✔Step2: Ansible Inventory**

Now, let's check the Ansible inventory using the command:

```plaintext
ansible-inventory --list
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692859774319/01afb95d-b905-4a54-a439-ee229a0ed561.png align="center")

### **✔Step3: Try a ping command using Ansible to the Nodes**

We use the following commands to check connectivity between the master server and node servers.

```plaintext
ansible servers -m ping
# ansible is the command line utility used to interact with remote servers
# servers is a group name we created for node servers, shown above
# -m is the module
# ping is the name of module
```

```plaintext
ansible prod -m "ping"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692856538777/021268f6-5cff-4343-9daf-8b178efc495f.png align="center")

### **✔Step4: Installing docker and checking the version**

```plaintext
ansible prod -m apt -a "name=docker.io state=present update_cache=yes"
ansible prod -a "docker --version"
ansible prod -a "free -h"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692860115366/8fa1acbd-f7d0-45be-8d2e-ad13d4a010bd.png align="center")

## **🔱TASK 2: Ansible Playbook**

### **✔Step 1: Setting Up Your Directory Structure**

Organizing your Ansible project is essential for maintainability. Let's start by creating a directory for your playbook:

```plaintext
mkdir playbooks
cd playbooks
```

### **✔Step 2: Create Your First Playbook**

Now, let's create your very first playbook. In the same project directory, create a file named `date_play.yml`:

```plaintext
ansible-playbook date_play.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692861277801/9b253b66-125d-4f32-ae4a-ff34ce44d215.png align="center")

```plaintext
ansible-playbook -v date_play.yml
```

The `-v` flag indicates that you want to run the playbook in verbose mode, which will provide more detailed output during execution.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692861658212/a945f7f7-3f63-4bd0-a1f9-97957d2b7d25.png align="center")

### **✔Step 3: Create Your Second Playbook (install-nginx)**

Now, let's create your second playbook. In the same project directory, create a file named `install_nginx.yml`:

In this playbook, we have to only install nginx.

```plaintext
ansible-playbook install_nginx.yml
```

```plaintext
- name: Install nginx and start it
  hosts: servers
  become: yes
  tasks:
    - name: install nginx
      apt:
        name: nginx
        state: latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692861797303/84e736d8-84ac-48ef-97e8-033c2ca87243.png align="center")

### **✔Step 4: Create Your Second Playbook (start-nginx)**

Now let's modify this playbook, we have to start nginx.

```plaintext
- name: Install nginx and start it
  hosts: servers
  become: yes
  tasks:
    - name: install nginx
      apt:
        name: nginx
        state: latest
    - name: Start Nginx
      service:
        name: nginx
        state: started
        enable: yes
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692862046275/18925f68-62da-4c9e-8448-8024249d297f.png align="center")

### **✔Step 5: Now verify nginx working**

Now verify server 1 with an IP address.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692862227361/11cca5b3-73b1-4a26-947b-75cd89a57f73.png align="center")

Now verify server 2 with an IP address.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692862240161/6ea6075b-49dc-4366-bb2b-3030f8f4ad4d.png align="center")

## **🔱TASK 3: Static Website hosting using Playbook**

### **✔Step 1: Create Ansible Playbook**

Create a new playbook in the directory known as a "playbooks".

Here you create a YAML file "deploy\_static\_page.yml" and create a new index.html page to serve in the prod group servers.

```plaintext
- name: Install nginx and serve static website
  hosts: prod
  become: yes
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: latest
    - name: Start Nginx
      service:
        name: nginx
        state: started
        enable: yes 
    - name: Deploy web page
      copy:
        src: index.html
        dest: /var/www/html
```

```plaintext
ansible-playbook deploy_static_page_play.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692863361005/5ca85ce3-c879-40bb-99a5-8257d8620d91.png align="center")

### **✔Step 2: Check your Web page**

Now, it's time to check your webpage is visible and working fine.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692863446488/76ac9b17-4328-4ee9-b51c-ea07dd9b0656.png align="center")

Modify your index.html file and reapply the playbook "deploy\_static\_page.yml" in the directory.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692863535042/e9f41f96-59b8-471b-bdb9-49f41530505e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692864808138/33bfd56d-768d-47f7-8f20-211eb1e6646d.png align="center")

# **🌟Conclusion**

Congratulations! We have just created and executed the Ansible playbook. This simple example demonstrates the power of Ansible in automating tasks on remote servers.

I always recommend visiting the official documentation while learning a new skill/tool. Please check this official doc: [**https://docs.ansible.com/ansible/latest/playbook\_guide/playbooks\_intro.html**](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html)

As you continue your Ansible journey, you can explore more advanced playbooks, modules, and features to orchestrate complex infrastructure configurations and deployments.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.😊

#aws #cloudcomputing #ansible #configurationmanagement #ansibleplaybook #Devops #TrainWithShubham #90daysofdevops #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)