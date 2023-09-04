---
title: "Part 3: AWS CodeDeploy with Automated CI/CD Pipeline 🚀 ☁"
datePublished: Mon Sep 04 2023 15:33:40 GMT+0000 (Coordinated Universal Time)
cuid: clm51kewf000m09jk3ejse05a
slug: part-3-aws-codedeploy-with-automated-cicd-pipeline
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693809159490/22bb1b53-fcf7-4b7c-99f1-a7e4cf2419c8.png
tags: aws, devops, codepipeline, 90daysofdevops, trainwithshubham

---

# **🌟** Introduction

In a journey of making a CI/CD pipeline on AWS with these tools, we have done AWS CodeCommit, CodeBuild and some parts of the CI pipeline. Now in this blog, we have moved to CodeDeploy with automated CICD pipeline workflow.

If we change a single dot or any change in the code, the pipeline starts automatically.

Let's learn these tools/services also:

* Github
    
* CodeDeploy
    
* CodePipeline
    
* S3
    

# **🌟** What is CodeDeploy?

AWS CodeDeploy is a deployment service that automates application deployments to Amazon EC2 instances, on-premises instances, serverless Lambda functions, or Amazon ECS services.

CodeDeploy can deploy application content that runs on a server and is stored in Amazon S3 buckets, GitHub repositories, or Bitbucket repositories. CodeDeploy can also deploy a serverless Lambda function. You do not need to make changes to your existing code before you can use CodeDeploy.

# **🌟 What is CodePipeline?**

CodePipeline builds, tests, and deploys your code every time there is a code change, based on the release process models you define. Think of it as a CI/CD Pipeline service.

# **🌟Follow these steps to perform this hands-on Project**

## **🔱TASK 1: Create new IAM Roles**

### **✔Step 1: Create the first IAM role**

Go to IAM service and click on roles.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693810741260/a60e037b-acc4-4f1c-96b3-11152ab5c5b3.png align="center")

Create an IAM role for the ec2 instance to communicate with code deploy.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811027487/4cac2925-3bf8-46a4-82a2-7e2e942b065f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811036879/26b2986d-bdd5-4c3a-a282-fde597a639d5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811049407/62458878-c629-4754-86e0-bf69db9707d2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811060691/84c91d30-746e-4670-9694-175cebb101bb.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811070038/630c9f69-e89f-4771-a56b-713472f1053e.png align="center")

### **✔Step 2: Create a second IAM role**

Create an IAM role for the code deploy to call AWS service on your behalf.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811101942/8c2db44d-540f-466d-a866-2cdd40e240e1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811112858/813c96fd-cdb7-4da6-bd08-221ac63fdc3b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811121161/fd2fc4a9-8479-48b4-be72-fed4398835fe.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811129753/05b9e3e2-16ba-4f0e-989e-7678a11552cc.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811136987/5eceb995-c5a1-4d94-9284-c982040d9dac.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811158313/39924343-8d5d-4b34-bdad-b26972e0bb01.png align="center")

Finally, roles that we create.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811176245/6f61c159-e797-4cbc-8b84-a5cb1d1e6449.png align="center")

## **🔱TASK 2: Launch an EC2 Instance**

### **✔Step 1: Launch new ec2 instance**

Go to aws console and search for ec2 then click on launch instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693809952836/1d95ae07-b4aa-4572-ad40-650d3747b359.png align="center")

You can give a name to your server, ec2 instance example "sample-python-app".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693810014777/19efa77f-537e-46d1-8cfa-af723099baed.png align="center")

The operating system and applications you wish to utilize on the virtual server should be represented by an Amazon Machine Image (AMI), so choose one of those.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693810029255/58fcf36b-e81e-45b1-82b4-1d80f47606ae.png align="center")

Select an instance type that outlines your instance’s hardware specifications, such as the number of virtual CPUs, RAM and then the Key pair name.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693810045712/19018c15-2e53-4930-893d-8fb2b112de38.png align="center")

Set the instance’s parameters, including its number of instances and network configuration

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693810062506/bb9b9747-458b-41c8-8c7e-4794fd472a59.png align="center")

Configure the EBS storage

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693810072672/611b8bf5-cfe3-42f9-b74d-2610858171c7.png align="center")

Add user data script, run at the time of server creation.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693810094906/9d3c7e1d-1cb9-42db-b7c9-652d29616a04.png align="center")

### **✔Step 2: Attach the IAM role to an instance**

Attach a new role to your instance, after attaching this role your instance talks to the code deploy service.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811246753/36eb129f-493d-4312-b293-b433abcb3aae.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811262730/65f7ce97-bb04-459e-8cb7-fa1a646a5282.png align="center")

### **✔Step 3: Setup CodeDeploy agent on your instance**

Follow this URL to set up your agent on ec2.

[SETUP\_AGENT](https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-ubuntu.html)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693810528752/a00e653f-fede-4bc3-bc38-8e41db69abea.png align="center")

```plaintext
sudo apt update
sudo apt install ruby-full
sudo apt install wget
cd /home/ubuntu
```

For the bucket name follow this URL

[BUCKET\_URL](https://docs.aws.amazon.com/codedeploy/latest/userguide/resource-kit.html#resource-kit-bucket-names)

```plaintext
Example	  - wget https://<bucket-name>.s3.<your-region>.amazonaws.com/latest/install
Practical - wget https://aws-codedeploy-ap-south-1.s3.ap-south-1.amazonaws.com/latest/install
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693810545795/c890944f-049d-4138-8650-2ad4f6d1d016.png align="center")

```plaintext
chmod +x ./install
#To install the latest version of the CodeDeploy agent on any supported version of Ubuntu Server except 20.04
sudo ./install auto
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693810559823/3f9f5ac5-b36e-4f9c-a780-86d1c0a9606e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693810567577/338d518b-ec04-4514-a390-9d7639d7e596.png align="center")

```plaintext
# a> To check that the service is running
sudo service codedeploy-agent status
```

```plaintext
# b> If you see a message like error: No AWS CodeDeploy agent running, start the service and run the following two commands, one at a time:
sudo service codedeploy-agent start
sudo service codedeploy-agent status
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693810578812/d784092b-912e-4fa7-94e9-428fc32e352c.png align="center")

### **✔Step 4: New S3 bucket created automatically**

A bucket is created after the agent setup is completed on an ec2 instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693818490735/e4ec59b9-5c39-41b2-a7e2-daa18d8012a2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693818500945/6db08818-4f3e-4038-a895-e4165789e12e.png align="center")

Here your source artifact is stored.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693818506063/ef4019cc-b679-4ffc-be62-c026339c1f13.png align="center")

## **🌟 Task3: Setup CodeDeploy**

### **✔Step 1: Create an Application**

Go to the AWS console search for CodeDeploy and first create an application name before the code deployment group.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693811928293/c5ee3a5b-5f40-4ad2-9f5a-7874e4095fb5.png align="center")

### **✔Step 2: Create Deployment Group**

Create a new deployment group.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812032138/1788d267-a173-4847-927d-803c2115bd41.png align="center")

Provide a suitable name for your deployment group

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812040122/1b241548-311f-4f14-9ed3-c5d887036181.png align="center")

Attach a service role you created at the time of IAM role creation "Code-deploy-role".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812047992/fa3c946e-6f61-4820-ba05-72ed57d804ed.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812056203/7edd6bd5-b7f1-49d1-915a-966f04d42053.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812062900/a23ffc13-9208-4a87-bfe5-87b3429e0b7d.png align="center")

Click on Create Deployment Group.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812071480/d19bc7c8-1d02-4423-b067-c0d4749f234a.png align="center")

### **✔Step 3: Create Deployment**

Create a deployment for your application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812207499/9cfe4192-66f7-4bb0-830d-c29351a2031c.png align="center")

Now establish a connection with Github. Authorize AWS CodeDeploy with GitHub. Generate a GitHub token with a suitable name.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812236654/504356b9-89ae-421e-aca4-0d0125317431.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812243735/1f12026a-dff7-48f6-a913-522f20ded59c.png align="center")

Copy the Commit ID and paste it on the deployment configuration with the repository name.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812441553/f8c03fd0-db54-4498-ba1d-e09f3143ddc5.png align="center")

Enter the repository name and commit ID for the deployment process.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812411422/de40def3-28bc-4311-90ce-9850c4fb3d3b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812405645/b9548436-40c5-4827-a6f4-808b63b9e087.png align="center")

### **✔Step 4: Start Deployment**

Your deployment starts automatically.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812654975/31931657-9276-422d-912f-b341125336e5.png align="center")

Deployment failed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812675633/e16cd62a-7b44-417a-b8f3-d924c5d25c8f.png align="center")

Code deploy phase details.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812684276/f8d70e81-d426-4a84-bf83-cab282614f30.png align="center")

Checking Logs "docker not found".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812698816/6d64b075-5ae8-4793-88bc-fa358c1813a9.png align="center")

### **✔Step 5: Install Docker (Solving Errors)**

SSH your instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812778839/9dfaf7a3-9a9d-433a-8681-e89ec4ff7542.png align="left")

Install Docker and check the status of Docker.

```plaintext
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
sudo systemctl reboot docker
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812719354/8f42f5ba-c0f0-439f-ac1c-d42fbef04a94.png align="center")

### **✔Step 6: Start Deployment Again**

Now deployment is successful.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812743877/4573321b-d565-4ecb-9a89-9e01f12fe496.png align="center")

Code deploy phase details.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812834815/cae063d3-630b-4f0b-bf97-3e6eb42cc87b.png align="center")

docker container running successfully.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693812850793/3cecb851-172a-466c-874c-f266d0be7c0b.png align="center")

## **🌟 Task4: Create Pipeline integration**

### **✔Step 1: Integrate Code Deploy with Code Pipeline**

Search Code Pipeline in the AWS console

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813103770/bb670126-f9ed-401e-b59b-bafc8663bd19.png align="center")

### **✔Step 2:** Reexecution of previously built Pipeline (Source and Build) stages

Follow this blog link to learn how to integrate code build with code pipeline.

[CODEBUILD\_&\_CODEPIPELINE](https://dushyantkumark.hashnode.dev/part-2-aws-code-build-pipeline-integration)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813169917/6d37496a-6f4a-4e5f-8c7c-1cb5c4c4131c.png align="center")

### **✔Step 3: Add a new stage in the pipeline**

Add a new stage in the code pipeline "code-deploy".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813164615/bdcde429-aed1-4c70-bba3-0b1904adc07a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813220724/bde83ef9-bad7-4b26-8e46-443e800095aa.png align="center")

Now edit the code-deploy action. Add the action provider "AWS CodeDeploy" with the application name and deployment group.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813253746/1126eb1c-376b-4d54-84e9-38f485cc2f80.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813277050/b70c5a30-c6eb-4f1e-90b7-f70500822403.png align="center")

Click on save stages.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813290150/95b7edef-52ec-4ed2-b17e-fa72eea39441.png align="center")

### **✔Step 4: Start Pipeline Execution**

Now start the pipeline execution to check the "Source, Build and code-deploy" stage.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813316598/bcb365f0-2fb7-49bd-beec-6ddc6186986d.png align="center")

"Build" Stage Successful.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813437538/f7733ae6-0c72-48df-8a84-03446fdea5ae.png align="center")

The "code-deploy" stage failed. Now check the reason for the failure.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813463605/9733ec04-82cc-47a2-9c25-fe96b7b99b0e.png align="center")

Checking logs of the "code-build" stage. The reason for failure is "port is already allocated"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813477663/1bd1cd10-eda5-42ac-a876-30f8189c5d41.png align="center")

### **✔Step 5: Create Script in Github**

First, kill/ remove the previous running container "at the time of code deploy".

```plaintext
docker ps
docker rm -f <container_id>
or
docker rm -f <container_name>
docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813496031/0d38e131-435d-41aa-99c3-65eb4796d457.png align="center")

Create a script for stopping a running container and creating a new container with the same port number "stop\_container.sh"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813515471/2325dc72-1642-4105-a765-875fefb5cc25.png align="center")

The pipeline starts automatically.

The "source" stage is successful.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813531246/74481d8a-b36d-4a6b-8c86-b7489a773987.png align="center")

The "Build" stage is successful.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813548265/cd3972f1-0f66-47ef-b2d7-7737f6030fa6.png align="center")

The "code-deploy" stage is successful.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813557993/4417db65-e4c8-4450-bd91-0383acb07c38.png align="center")

Check running container

```plaintext
docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813670443/8faf37af-dd92-46ab-9783-7531755a4328.png align="center")

Code Pipeline has succeeded.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813696720/6f67140f-1276-4105-953f-c1947cfd64b8.png align="center")

Updated Docker Image

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813682284/0274aa48-5d24-4d11-bd43-650da566bec8.png align="center")

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.😊

#aws #cloudcomputing #codecommit #github #git #Devops #TrainWithShubham #90daysofdevops #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)

**<mark>Github</mark>**: [**https://github.com/dushyantkumark/aws\_cicd\_simple\_python\_app.git**](https://github.com/dushyantkumark/aws_cicd_simple_python_app.git)