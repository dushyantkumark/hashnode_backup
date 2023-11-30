---
title: "Set up your EKS cluster like a Game🎆🎮"
datePublished: Thu Nov 30 2023 11:27:17 GMT+0000 (Coordinated Universal Time)
cuid: clpl42obz00010aldadui96tk
slug: set-up-your-eks-cluster-like-a-game
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701259762699/0dfcb016-b1ef-4410-854c-fa2747829827.png
tags: aws, k8s, 90daysofdevops, eks-cluster, trainwithshubham

---

Elastic Kubernetes Service (EKS) is the Kubernetes service managed by AWS. It is a managed service that helps simplify the deployment, management, and scaling of the Kubernetes cluster on the AWS cloud platform. It provides seamless integration with various AWS services like CloudWatch, VPC, and IAM, making it easier to utilize AWS resources which helps to improve performance, security, and scaling. This service follows the AWS pricing model where users only need to pay for the used resources required to manage the EKS cluster which helps to optimize pricing.

## 📚 Follow these steps to set up the EKS cluster:

* Configure the EC2 instance which is going to be an entry point of our EKS cluster, you can use t2.micro(free tier) for that.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701329508267/dc821feb-bdfe-44c8-a45e-5aa642f0a443.png align="left")
    
    * Connect your instance using SSH to give commands and interact from your terminal.
        
    * Do the pre-requisites with the newly launched instance `sudo apt update`
        

### 📲 Install AWS CLI:

```plaintext
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

sudo apt install unzip

unzip awscliv2.zip

sudo ./aws/install -i /usr/local/aws-cli -b /usr/local/bin --update
```

* This command basically installs the aws cli which command line tool to interact with AWS.
    

You can confirm your installation with:

```plaintext
aws --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701329565511/c763b929-addc-44d0-ad9e-06edcfd7a016.png align="center")

### 👨‍💻 Configure IAM User:

* Configure your IAM user which will give you the access keys to connect with your AWS securely through the terminal and ensure that to have required specific permissions to create and use AWS resources and services.
    
* Navigate to the IAM settings and click on Create User.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701329634482/846faba6-9829-4506-9417-4251d094be1d.png align="left")
    
* Give a suitable username to the IAM group.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701329663872/3a27f72f-b362-407a-a628-a6dedc5090a3.png align="left")
    
    > ***No need to check the box to provide access to the management console. and click on the next.***
    > 
    > Set permissions as per the requirements to do so <mark>select Attach policies directly</mark>. In this example, I'm giving admin access.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701329686558/efeee156-0ede-429d-bb93-185d863966dd.png align="left")
    
* Now your user is created "<mark>eks-admin</mark>".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701329734442/fa88f175-a054-4a76-85d5-2207f3b05dd4.png align="left")
    
* Go to the security credentials and click on <mark>create credentials</mark>.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701329869905/84d4f351-950f-46e9-89fd-99a4998b5841.png align="left")

* Click on the <mark>Create Access key</mark>.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701329958715/cb9babec-d81d-4256-a03f-2f44aa7d49ed.png align="left")

* Then you will see this interface which will give several types of options to create an access key.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701329974434/331a00f3-bc40-40e1-ae9c-a30ce07abb56.png align="left")
    
    * Select the <mark>Command Line Interface(CLI)</mark> option.
        
    * Then <mark>check</mark> the box of <mark>confirmation</mark> and click next.
        
    * On the next page, you can see the generated access keys.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701329990657/8b6dd50c-40aa-401e-8c57-016061a78761.png align="left")
        
        * Now configure your ec2 instance with the IAM user you have created to give all required permissions to create an EKS cluster.
            
        * Go to the terminal and type the command `aws configure`
            
        * Then the terminal will ask you for <mark>credentials</mark> and <mark>region</mark>, and put in the generated credentials and region.
            
            ```plaintext
            aws configure
            ```
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701330007461/9f08b5a0-e6ea-4a50-b76c-e1620957fb8a.png align="left")
            

## 🎡 Now we are going to set up Kubernetes tools.

### **📜 Install Kubectl:**

```plaintext
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl

chmod +x ./kubectl

sudo mv ./kubectl /usr/local/bin

kubectl version --short --client
```

Confirm your installation `kubectl version --short --client` with this command, you will get the output.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701330035535/0a140d32-eba5-4a5b-9516-2fdea77a31ab.png align="left")

### **📟 Install eksctl :**

```plaintext
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

sudo mv /tmp/eksctl /usr/local/bin

eksctl version
```

* Confirm your installation `eksctl version` with this command, you will get the output: 0.165.0
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701330070056/afa086f4-54a8-421d-8263-56407fff21c9.png align="center")
    
* **Now to create your cluster with this command:**
    
    ```plaintext
    eksctl create cluster --name 2-tier-app-cluster --region us-east-1 --node-type t2.micro --nodes-min 2 --nodes-max 4
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701330109623/ceed1200-12f5-4d73-a4c4-fa39fbf71ab3.png align="left")
    
* It will take 15-20 minutes to create the cluster.
    
* After successfully creating the cluster see the running nodes.
    
    ```plaintext
    kubectl get nodes
    ```
    
* You will see this output where you can see the running nodes.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701330128482/7009c5f2-e636-43e7-9b37-f799e2d6c8c0.png align="left")
    

## 💣Destroying cluster:

* It's easy to destroy clusters through the terminal if you are trying to destroy it from the console it's a bit difficult.
    
* Because the EKS cluster uses AWS's LoadBalancer service in the background
    
* So in case you terminated your entry point instance you will need to manually delete the load balancer service.
    
* So always use the command to destroy the cluster.
    
* A command for destroying cluster
    
    ```plaintext
    eksctl delete cluster --name 2-tier-app-cluster
    ```
    
    > ***Replace the cluster name with your cluster name.***
    > 
    > ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701330342364/c85d2b66-0167-4aff-8e25-22df251760cf.png align="center")
    
    \\...................................................................................................................................................
    
    The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.😊
    
    #aws #cloudcomputing #docker #Devops #TrainWithShubham #90daysofdevopsc #happylearning
    
    **<mark>Follow for many such contents:</mark>**
    
    **<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)
    
    **<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://linkedin.com/in/dushyant-kumar-dk)
    
    **<mark>Github</mark>**: [https://github.com/dushyantkumark/two-tier-flask-app/tree/](https://github.com/dushyantkumark/two-tier-flask-app/tree/helm)main