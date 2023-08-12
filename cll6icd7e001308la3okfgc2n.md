---
title: "Project Title: Jenkins Declarative Pipeline with Email Notification Part-2🚀"
datePublished: Fri Aug 11 2023 11:31:22 GMT+0000 (Coordinated Universal Time)
cuid: cll6icd7e001308la3okfgc2n
slug: project-title-jenkins-declarative-pipeline-with-email-notification-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691830607534/cdd44852-52a7-4e8e-8a5e-82543e1e91d7.png
tags: devops, jenkins, 90daysofdevops, trainwithshubham, cicd-pipelines

---

# 🌟Introduction

Continuous Integration and Continuous Delivery **(CICD)** are crucial aspects of software development that help us **build, test, and deploy software quickly and efficiently.**

# **🌟Project Overview**

Our project is a weather application application. To automate the deployment process of this application, we have set up a CI/CD pipeline using Jenkins. The pipeline consists of several stages, including **code cloning, building Docker images, deploying services to servers using Docker Compose, and updating the Docker registry,** on the server. Get email notifications on your Gmail account.

## **🔱Pre-requisites**

1. A GitHub account to store the source code.
    
2. One server/machine :
    
    a) Jenkins declarative
    
3. Jenkins, Docker and Docker Compose are installed.
    
4. Docker Hub is used to store Docker-versioned images.
    
5. Knowledge of Groovy syntax to create the Jenkins pipelines.
    
6. Set up AWS Simple Email Service (cost-effective email service).
    

## **🔱Let's get started---&gt;**

### ✔Step 1: Get the source code of the web App

Fork this repo:

[https://github.com/dushyantkumark/Weather-App.git](https://github.com/dushyantkumark/Weather-App.git)

### **✔Step 2: Make the server ready for deployment purposes**

Create an ec2 instance, one as the master node for deployment purposes.

<mark>Instances can be t2-medium, 2 CPU, 4 GiB Memory, and ports 8080 , 80, 22, 3000 are open to allow incoming traffic</mark>

**<mark>HOW TO SETUP AN INSTANCE FOLLOW THE PART1 LINK</mark>**

[ec2\_setup\_using\_terraform](https://dushyantkumark.hashnode.dev/project-title-jenkins-setup-using-terraform-part-1)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691647908033/707c0778-2035-4fee-86e9-cb70a9408fb1.png align="left")

* Check versions.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689784485020/6684afdf-ba44-4e62-8c41-358590bed11b.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")
    

Access your Jenkins on [**Localhost**](http://Localhost)[**\[EC2**](http://localhost%5Bec2/)**\](**[**Localhost**](http://Localhost)[**%5BEC2**](http://localhost%5Bec2/)**) \[instance public ip\]:8080**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689785450771/6c643790-2aae-418c-98da-fe0b27ba7509.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **✔Step 4: Create a Jenkins Pipeline project**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691648363006/5890ba45-bd9b-40cd-a95e-83d4d5594530.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691648389763/e7451ce5-7a24-4720-9f45-3577486f3f44.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691648410262/4b67ca7a-c97b-4d90-9082-7f8a550e9a45.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691648434733/3dafcf7b-f96c-4af4-8bd9-bd1a59674904.png align="center")

### **✔Step 5: Docker Hub credentials**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691649228080/c8e46ccc-0f0a-4cc0-b69d-5c63e2d5d739.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691649257649/45411dfe-5401-4ff2-a35d-417bbcf7ccaf.png align="center")

### **✔Step 6: Create a Jenkinsfile for our pipeline to run**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691648504240/6b23ea91-86db-4bb6-a9bd-ba1b79d0a678.png align="left")

```plaintext
pipeline{
    agent any
    
    stages{
        stage('Copy Code'){
            steps{
                echo "Cloning the code"
                git url:"https://github.com/dushyantkumark/Weather-App.git", branch:"main"
            }
        }
        stage('Build'){
            steps{
                echo "Building the image"
                sh "docker build -t weather_app ."
            }
        }
        stage('Logging & Pushing to DockerHub'){
            steps{
                echo "Pushing the image to dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag weather_app ${env.dockerHubUser}/weatherapp:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/weatherapp:latest"
                }
            }
        }
        stage('Deploy'){
            steps{
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
```

The pipeline has several stages that are executed sequentially:

1. **"code" stage:** This stage checks out the code from the GitHub repository using Git.
    
2. **"Build docker images" stage:** This stage builds Docker images for the different components of the multi-container application, such as worker, result, and vote.
    
3. **"Deploy services" stage:** This stage deploys the Docker containers for the application using docker-compose.
    
4. **"Update docker images" stage:** This stage updates the Docker images on DockerHub by pushing the newly built images
    
    The pipeline is executed and sets an environment variable DOCKER\_IMAGE\_TAG using the build number. The pipeline uses several shell scripts to perform Docker-related tasks . The pipeline also uses credentials to log in to DockerHub and push images.
    
    ### **✔Step 7: Run the Pipeline manually to check for any errors**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691648618433/283acb0c-77fb-4d96-a88a-b749a655e32d.png align="left")
    

### **✔Step 8: Check whether the docker image successfully upload to the docker hub or not**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691648667439/e5774a05-4b35-4015-9abd-2601fc5b8f87.png align="left")

The build Succeeded and we can access the Application on the development server, for this Please allow 3000 port in the security group to check the weather app.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691649456590/7f2b8b0e-65b9-4a65-8095-344acff182a4.png align="left")

### **✔Step 9: Setup AWS SES Service**

**Go to the AWS console and search SES (Simple Email Service)**

Once logged in, navigate to the Amazon SES dashboard by searching for "Simple Email Service" in the AWS Management Console's search bar.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691649564470/bf345f26-95cf-4778-b777-abf953b46904.png align="left")

Before you can send emails using Amazon SES, you need to verify the email addresses or domains you'll be sending from. This helps ensure your emails are trusted and less likely to be marked as spam.

* **Verify Email Addresses**: You can verify individual email addresses that you want to send from. Amazon SES will send a verification email to each address, and you need to follow the verification steps in that email.
    
* **Verify Domains**: If you want to send emails from a specific domain (e.g., [example.com](http://example.com)), you can verify the domain instead of individual email addresses. This typically involves adding DNS records to your domain's DNS settings.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691649579731/e34b0503-4fd8-41e4-b96c-7c82c418e000.png align="left")

Verify this URL

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691649613352/a1eb0b68-7fa9-4d42-ac4f-ea3d6b769414.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691649628630/3c0cec7f-7106-4785-9284-412283996a9b.png align="center")

If you want to use Amazon SES to send emails from your applications, you can create SMTP credentials. These credentials can be used with any email client or application that supports SMTP authentication.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691649645750/7050eea9-7633-4517-a9f6-7c7f8d67b0ff.png align="center")

You get your SMTP credentials such as IAM user name, SMTP user name and SMTP password.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691649665049/c8c9b90a-6d1a-4b87-8863-26aa1407e1ba.png align="center")

### **✔Step 10: Setup SMTP in Jenkins**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691650098675/7321accd-da6d-474d-a97a-339cec3afdb0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691650115370/c878461d-cf4d-4a3b-93c1-9fa971b08ceb.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691650144560/3d576a2b-fa31-4d97-b214-303a6dce7c59.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691650161995/546facf6-e5c7-49bf-9fed-2c68a27ccd59.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691650176739/618e660c-7296-433a-8ee9-944ccc09cb0c.png align="center")

Now Jenkins CI/CD pipeline code be

```plaintext
pipeline{
    agent any
    
    stages{
        stage('Copy Code'){
            steps{
                echo "Cloning the code"
                git url:"https://github.com/dushyantkumark/Weather-App.git", branch:"main"
            }
        }
        stage('Build'){
            steps{
                echo "Building the image"
                sh "docker build -t weather_app ."
            }
        }
        stage('Logging & Pushing to DockerHub'){
            steps{
                echo "Pushing the image to dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag weather_app ${env.dockerHubUser}/weatherapp:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/weatherapp:latest"
                }
            }
        }
        stage('Deploy'){
            steps{
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }

    post{
        success{
            emailext attachLog: true, body: 'Email send out from Jenkins', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'kumardushyant545@gmail.com'
        }
        failure{
            emailext attachLog: true, body: 'Email send out from Jenkins', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'kumardushyant545@gmail.com'
        }
    }    
}
```

Run this pipeline code

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691650216498/35c66c0a-b3c0-4c11-8ccd-f5375aec4734.png align="center")

After a successful pipeline run, you get an email from Jenkins with the pipeline name, build number, build status and log file attached.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691650233243/f7f78579-c1e9-44a2-9657-3584da82db5f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691650246114/2be4ed1d-80fc-4d4d-b2c4-3cd23e74a5b3.png align="center")

WOW, your application is running successfully.🔥

&lt;ip\_address&gt;:3000

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691650264650/a4f15435-07d6-4454-9ae9-51547f42269c.png align="center")

### **✔Step 11: Setup** Cloud Watch metrics of CPU Utilization in Percentage(%)📺📈

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691684727207/5d4d4cdc-3713-4b0b-bfba-072006580882.png align="center")

## **🔱Clean Up**

To clean up and delete all of the infrastructure resources we created, run the following command:

🔥Terraform Destroy Command is used when you complete your project, this is only a setup process. The next stage is Jenkins CI/CD pipeline with email message (your build is successful with the project name, build number and build log).

```plaintext
terraform destroy
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691591893467/fa0bbb05-c20b-466e-b0c3-f73454c7b37f.png?auto=compress,format&format=webp align="left")

**<mark>IF YOU WANT TO KNOW HOW TO SET UP SERVER REFER TO PART1 BLOG</mark>**

[BLOG\_LINK](https://dushyantkumark.hashnode.dev/project-title-jenkins-setup-using-terraform-part-1)

suggestions are always welcome🔥

# **🌟Conclusion:**

In this blog, we explored the significance of implementing Continuous Integration/Continuous Delivery (CI/CD) pipelines in software development. Demonstrated how to create a Declarative pipeline in Jenkins that can automatically build Docker images for updated app code and deploy them to the targeted deployment environment, notify management teams about new releases/updates, and perform clean-up for the host server.

Using CICD pipelines teams can streamline their software development processes, improve software quality, and achieve faster release cycles. By automating the repetitive and error-prone tasks of building, testing, and deployment, teams can focus on writing high-quality code and delivering value to their users.

In the end, we know how to use aws ses service and integrate it with Jenkins.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.

#terraform #aws #hcl #Devops #jenkins #CICD #TrainWithShubham #90daysofdevopsc #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)

**<mark>TERRAFORM_SERVER_SETUP</mark>**: [**https://github.com/dushyantkumark/Terraform\_Jenkins.git**](https://github.com/dushyantkumark/Terraform_Jenkins.git)

**<mark>PROJECT_GITHUB</mark>**: [https://github.com/dushyantkumark/Weather-App](https://github.com/dushyantkumark/Weather-App)