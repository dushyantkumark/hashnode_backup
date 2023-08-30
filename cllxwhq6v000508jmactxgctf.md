---
title: "Part 2: AWS CODE BUILD & PIPELINE INTEGRATION🚀"
datePublished: Wed Aug 30 2023 15:37:13 GMT+0000 (Coordinated Universal Time)
cuid: cllxwhq6v000508jmactxgctf
slug: part-2-aws-code-build-pipeline-integration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693399064042/1bd4dd26-1b94-42b3-98c7-8e90d92e408d.png
tags: aws, devops, codepipeline, 90daysofdevops, codebuild

---

# **🌟 What is CodeBuild?**

***AWS CodeBuild*** is a fully managed build service in the cloud. CodeBuild compiles your source code, runs unit tests, and produces artifacts that are ready to deploy. CodeBuild eliminates the need to provision, manage, and scale your own build servers.

# **🌟 What is CodePipeline?**

CodePipeline builds, tests, and deploys your code every time there is a code change, based on the release process models you define. Think of it as a CI/CD Pipeline service.

# **🌟Follow these steps to perform this hands-on Project**

## **🔱TASK 1: Perform your GitHub Operations**

### **✔Step 1: Create a new repository**

Create a new repository for your project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693385906063/02612862-ab28-4272-8d21-30cd1ee5358d.png align="center")

### **✔Step 2: Clone "AWS\_CICD\_simple\_python\_app" repository**

Clone your newly created repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386145665/6f8005b7-93fd-441e-a066-6bba2a082b79.png align="center")

Add new files for your Python-related project. After adding some more files to your local repository check your status of the local repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386193608/f4f6b2c2-6dd5-45fd-8bd9-3138dd9b65a4.png align="center")

Perform the adding operation and then check your local repository status. Now you tracked your files.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386210677/b0a966df-7970-4764-a0de-18a6e821797a.png align="center")

Give specific commits to the files you added.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386224903/43e0791e-79dc-4188-acfa-3233a57d4cdc.png align="center")

Push your files from the local repository to the code-commit repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386232450/259b4da2-9ecf-42ab-be92-56d73eef5483.png align="center")

## **🔱TASK 2: AWS Code Build (Build, Test and Push Code to Docker Hub)**

### **✔Step 1: Go to AWS Console and search CodeBuild**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386477541/32aac3db-78ec-4a50-9fc1-1fd2a0f2f726.png align="center")

### **✔Step 2: Create a new Project for CodeBuild**

Create a project for a Python application where you build, test and push code to the docker hub), It is a CI (continuous integration) process in AWS.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386600484/8af04704-4a29-4dd8-8567-5ec12e0da0ba.png align="center")

Create a project configuration, you define every detail regarding the project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386684326/7ee857b3-8531-40fa-a5af-afc19999a422.png align="center")

Change your source provider from AWS CodeCommit to GitHub.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386698270/39deff91-59fd-4a43-8604-c3e926b82a13.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386783120/a8cba635-1fb7-40cd-9b3d-f7614236e1fb.png align="center")

Authorize your AWS CodeBuild to access your GitHub account.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387275910/e1e9e8be-8957-4656-b0df-bbf073568cb7.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387300921/5778a131-43cd-42ff-a340-7635965aa26d.png align="center")

Create an environment for your code build to run the application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386848108/0230c212-4811-4ebf-9060-7d9bf83d98d7.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386867814/afc46cc2-f5fa-47c9-8276-74ae046aea3e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386884618/ad303636-d98f-4c43-bf01-6cde70113ada.png align="center")

You write your custom pipeline for the project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386908071/9397c62e-f964-41ab-bd11-1910a4070f7b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386923347/7cd325b8-6ab9-4a8c-bda8-f40d8aaeda97.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386935217/3b176bc9-4fcf-43bb-9e45-017be077972f.png align="center")

Now your code build project is created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693386964474/09c64c21-50f3-4d22-9440-e98482cdddf4.png align="center")

The new role is created when your code build project is created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387010263/138bd5ec-c40a-4aae-b387-65938cf2d548.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387016781/ee3f6e9c-7b94-460a-bb55-03a1b71a92c2.png align="center")

### **✔Step 3: AWS System Manager (Parameter Store)**

Go to the AWS console and search system manager.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387675898/0733f5fa-e15e-46cd-b1f4-c143afa7a10b.png align="center")

AWS Systems Manager simplifies cloud infrastructure management. It centralizes resource control, automates tasks, and enhances security. It offers tools for configuration management, software inventory, patching, and more, streamlining operations and ensuring consistent performance across AWS resources while maintaining a secure and compliant environment.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387691779/e376c372-eb60-47cb-9e27-ca50b4e97ac6.png align="center")

Create the first parameter for the docker username.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387708693/7d20951b-6d54-49da-9824-d1f4165ec744.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387717666/27013571-4df5-422a-8a96-c12e89642e41.png align="center")

Create the second parameter for the docker login password.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387726970/e85327db-1ebe-402e-ade0-c31359afe51c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387735049/9ebe196c-a95b-4d70-acf7-78cbc7d76743.png align="center")

Create the third parameter for the docker registry URL.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387745962/8c419948-37e9-4435-b5b0-d670d05a4b31.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387754294/efa4d608-fe9e-45f6-a43c-c03fd6de8631.png align="center")

Environment variables (parameters) output for your "buildspec.yml" file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693387765268/a089564a-c224-4f3d-aac4-86ae8bf79756.png align="center")

### **✔Step 4: Start your Build**

Go to build details and modify insert build commands.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693391167598/f275d036-dc5e-46be-9456-faf80890a7d4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693391176026/0b631655-45bc-434b-8269-a93de8424fa7.png align="center")

Modify your build commands for your project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693391221952/e690b108-e193-4a25-9ed1-a9222ecebad8.png align="center")

Checking Build logs, the reason for failure.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693391259415/befb76ed-b6c4-43e5-b0ea-df90fdcdca03.png align="center")

Go to IAM roles "codebuild-s-service-role" and attach the new policy "AmazonSSMFullAccess".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693391338936/7182d2ab-1121-49ad-8b83-90dc04428d00.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693391352168/d4c2d535-88ff-4e07-a0ac-7c2c2e956bd8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693391359228/623706e8-4d33-4c3a-a8ad-c0452dbcbf3d.png align="center")

After the pipeline starts, we get another error and now checking build logs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693391512721/fafbcd39-b7b2-4c9d-a4f7-0936f4ff4d8b.png align="center")

Modify your build commands(buildspec) for your project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693391980055/b202e419-0d39-45f9-ac4d-3b13514328d1.png align="center")

After the pipeline starts, we get another error and now checking build logs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693392031443/b405f1b9-160d-4194-afd9-2a5eac12138e.png align="center")

Edit the environment to give privileged permission to perform the docker build image and provide the service role "codebuild-s-service-role".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693392064338/0912cfd0-fdae-4b17-ae1a-192e62fabb18.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693392099344/9ae6636d-52d6-4865-8894-f154e42dc0af.png align="center")

🔥 Here we get a main error, Always remember your GitHub repository <mark>must be in lowercase</mark> (uppercase English alphabets not allowed)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693392203777/0c2e8f37-fa33-4568-9eaa-1dd4d0f425fb.png align="center")

### **✔Step 5: Updating GitHub repository name**

Edit my repository name from uppercase to lowercase.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693392361603/7111b53c-e7ff-4ad3-af22-7745e7332438.png align="center")

### **✔Step 6: Modifying Build Project (CODE BUILD)**

Modify a project configuration, you define every detail regarding the project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693392376445/e4948f24-2e76-4e38-a0d7-ae084a7887fb.png align="center")

Modify your build commands(buildspec file) for your project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693392413954/d7c39b98-f41c-4f0a-bece-a4ef469fbeb3.png align="center")

After the pipeline starts, we get another error and now checking build logs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693392435819/70f637f1-5a75-4e48-8fd8-fe3db15729ff.png align="center")

Again modify your build commands(buildspec file) for your project. Updating for docker login and pushing.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693392476081/6154b022-2c8c-4bea-b632-5bf415ff37f9.png align="center")

Finally, Build Succeeded.🤖

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693392504213/8daa36e8-28c4-4c52-a1db-9d2e25efbd5f.png align="center")

Build Logs

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693392518350/f79e5fe2-aa81-4e86-b08f-f7d7891c64d5.png align="center")

Successfully pushed docker image to Docker Hub.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693392535562/a5ec91ca-c782-4c01-9480-a2f74ff7b33d.png align="center")

## **🔱TASK 3: Integrate Code Build with Code Pipeline**

### **✔Step 1: Search Code Pipeline in the AWS console**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397212132/de6e9403-3f02-4717-8ebd-8754bd2fcc35.png align="center")

### **✔Step 2: Create a Code Pipeline**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397204436/c79de490-15ba-49f6-b66e-9025d9943572.png align="center")

### **✔Step 3: Configure Pipeline Settings**

Give a proper/suitable pipeline name and, a new service role for your code pipeline.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397236495/803b9e6c-3cdd-4314-ab3f-fcbcd7109bad.png align="center")

Add new source name "GitHub (Version 2)" this is a place where you store your input artifact.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397250366/147c24b3-fb7c-487e-9e48-2e6e52a4247f.png align="center")

Now establish a connection with Github.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397265248/f091c2fa-061d-4614-9ffc-8dc70410fb8e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397282269/1df64adc-d57c-4bff-8a9d-c326b69bf2be.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397294640/ea4f41a5-bf0a-4a0c-9834-901530864c80.png align="center")

Add your GitHub repository name with the branch name.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397305009/4dd12f1b-31b3-4e89-9497-90870610f359.png align="center")

Select your build stage "AWS CodeBuild", region and project name.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397319880/c7aa8563-8cc4-403b-8f93-4ed9f80390a5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397330103/e6ae77b4-1f22-49ea-b7ed-8651bfa506d9.png align="center")

Skip the deployment stage, I am including this stage in the code deploy blog (upcoming blog)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397346894/1427e768-ac0e-4add-b175-e31795881911.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397380002/b8a2a4d3-20a3-41e9-859f-4351e294face.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397405176/81d02893-2bff-4d5a-971c-4d4680521a63.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397413419/cc425896-7e45-4765-aac0-34a0dae357f2.png align="center")

The pipeline starts automatically after creating the pipeline.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397457255/347414db-636e-4ba7-adbb-ca214e693edb.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693397467433/59dae664-0ece-4683-8d41-efec25b05687.png align="center")

## **🔱TASK 4: Updating Code in Git Hub & Pipeline Trigger Automatically**

### **✔Step 1: Modify your code**

Before updating the code.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693398007663/02411de2-0a4a-416f-aa27-0a34aaa561c6.png align="center")

After updating the code.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693398029685/21fdabfa-18a4-45d3-a3f4-288ed334b6ab.png align="center")

### **✔Step 2: Your pipeline and build details after successful**

The pipeline starts automatically.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693398046791/f03a1f60-00b5-4263-bff0-d2741edb75df.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693398061555/d5122c7f-f821-4b22-9c5e-132b07c57ceb.png align="center")

Pipeline build logs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693398080845/5ad6a73b-d13a-4bb9-8157-7c3155e353db.png align="center")

Code build phase details.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693398106174/f6995dbb-d622-4066-a225-093f09948472.png align="center")

Code build project run details.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693398114836/f4039e29-670c-4a11-8257-debd362cc961.png align="center")

Updated Docker Image

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693398074427/d4a2625b-0bef-4a04-9d01-d9a178da288c.png align="center")

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.😊

#aws #cloudcomputing #codecommit #github #git #Devops #TrainWithShubham #90daysofdevops #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)

**<mark>Github</mark>**: [https://github.com/dushyantkumark/aws\_cicd\_simple\_python\_app.git](https://github.com/dushyantkumark/aws_cicd_simple_python_app.git)