---
title: "DevSecOps  Project : Swiggy Clone"
datePublished: Sun Dec 31 2023 11:26:59 GMT+0000 (Coordinated Universal Time)
cuid: clqtepp3m000008k0c1j3gmq0
slug: devsecops-project-swiggy-clone
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703965038652/599ffe67-6832-4f68-ac3e-6f4c501b9e84.jpeg
tags: cloud-computing, devops, devsecops, 90daysofdevops, trainwithshubham

---

# Introduction:

In today's fast-paced digital landscape, building and deploying applications not only requires speed but also airtight security. That's where DevSecOps comes into play, blending development, security, and operations into a single, unified process.

In this guide, we will start a journey where we'll leverage Terraform, Jenkins CI/CD, SonarQube, Trivy, Argocd, and Amazon Elastic Kubernetes Service (EKS) to create a robust and secure pipeline for deploying applications on Amazon Web Services (AWS).

Whether you're an experienced developer looking to enhance your DevSecOps skills or a newcomer eager to explore this exciting intersection of software development and security, this guide has something valuable to offer.

Let's start and explore the steps to safeguard your Amazon app while ensuring smooth and efficient deployment process.

## Overview:

* **Infrastructure as Code:** Use Terraform to define and manage AWS infrastructure for the application.
    
* **Container Orchestration:** Utilize Amazon EKS for managing and scaling containerized applications.
    
* **CI/CD with Jenkins:** Set up Jenkins to automate building, testing, and deploying the application.
    
* **Static Code Analysis:** Incorporate SonarQube to analyze code quality and identify vulnerabilities.
    
* **Container Image Scanning:** Integrate Trivy to scan container images for security issues.
    
* **Application Deployment with Argocd:** Use Argocd for declarative, GitOps-based application deployment on EKS.
    

### Project Resources:

**GitHub Link:**

[SWIGGY-CLONE-REPOSITORY](https://github.com/dushyantkumark/Swiggy_DevSecOps_Project.git) - Application code & Manifest files.

## Step1: Create IAM Users

Navigate to the **AWS console**

* Create two **IAM** user with **administration access.**
    
* Create two IAM user credentials for ap-south-1, us-east-1.
    
* Create one t2.xlarge EC2 instance with Ubuntu ami using terraform.
    
* Login to the EC2 instance and follow the below steps.
    

## **Step2: Aws Configuration**

Install the AWS Cli in your local machine (windows laptop)

**Check AWS CLI is install on your lapto:**

```plaintext
aws --version
aws configure
```

Provide your Aws **Access key** and **Secret Access key**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704010000122/087d3493-be09-4a11-a265-66fa6f10dc36.png align="center")

## **Step3: Terraform files and Provision Jenkins, sonarqube**

**Check terraform Installation in yor laptop :**

```yaml
terraform --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704010272211/96bc4f53-e527-4cb0-8812-181d33004c16.png align="center")

[Terraform\_Repository\_Link](https://github.com/dushyantkumark/Swiggy_DevSecOps_Project.git)

This will install Jenkins, Docker, Sonarqube, and Trivy, kubectl, eksctl, aws cli by Terraform with an EC2 instance(t2.xlarge).

### **Terraform commands to provision:**

```plaintext
terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704010545680/5d82921f-1086-48a7-847d-6715ea8839e6.png align="left")

```plaintext
terraform fmt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704010636410/87c6721a-4496-4089-83bb-c053c056fb20.png align="center")

```plaintext
terraform validate
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704010682730/868e431e-7ee4-45bc-a117-66f652671b57.png align="left")

```plaintext
terraform plan
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704010808772/6185b3ba-a5bd-411b-914f-7f5beac3558a.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704010822123/e12327e6-94ec-4be5-aea5-45f97ffb270e.png align="center")

```plaintext
terraform apply
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704010870214/96716266-c6b4-430f-b3d7-34469e201374.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704010896607/5ea1f5a2-121e-4273-979e-bcc5030c2ebe.png align="left")

Now uncomments the backend block in terraform.tf file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704011471210/da1fe600-50ca-419d-8c1c-2df79b995c4f.png align="center")

```plaintext
terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704011498085/b0210ff4-1db0-4b5a-9298-11daf6200fc8.png align="center")

**Output:**

The EC2 instance Jenkins-sonarqube-trivy-vm is created by Terraform with Jenkins, Sonarqube, Trivy, kubectl, eksctl, aws cli as userdata for the EC2 instance, which is installed during the creation of the EC2 instance.

S3 bucket is created with terraform.tf statefile present in it and dynamodb table is created for state locking the terraform state.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704011638197/a0de65b9-b4f8-49c9-9927-1dfdba5d280a.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704011727859/8e90d2df-0ce3-47c8-b27b-5c8cf8f065b0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704011750641/440a2e85-e23a-490b-bc59-1882423a0f8c.png align="center")

SSH my ec2 instance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704012109703/8d0ccf86-b5f8-4fad-9b38-9893f5795855.png align="center")

```plaintext
<Public IPV4 address>:8080. #For accessing Jenkins
13.233.17.158:8080
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704011940344/e55dc367-9a06-4c2c-8e7c-6ee6f1151a68.png align="center")

```plaintext
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704011999679/38c4abe3-f11f-40fc-be5a-a191ddd3e73d.png align="left")

Unlock Jenkins using an administrative password and install the suggested plugins.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702184009718/220fd0e7-8677-45b0-bcd4-864ca6140f0f.png?auto=compress,format&format=webp align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702184057274/24c6d381-fd6a-480f-9765-6c193b18f9b3.png?auto=compress,format&format=webp align="left")

Jenkins will now get installed and install all the libraries.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702184089284/2b9472b9-dd89-43e5-8722-d340d4fc2263.png?auto=compress,format&format=webp align="left")

Create a user, click save, and continue.

Jenkins Getting Started Screen.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702184154349/77e112a9-9681-4a30-9bb4-4da534f71347.png?auto=compress,format&format=webp align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704012135514/72b190f5-5a46-40b2-8f45-c7c2de813b03.png align="left")

Copy your public key again and paste it into a new tab.

```plaintext
<instance-public-ip>:9000
13.233.17.158:9000
```

Now our Sonarqube is up and running as a Docker container.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704012251453/f4aa75a2-2489-4c9e-a1eb-02ad6c003d99.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704012344798/6d3d4b18-9cde-4551-8903-ba36dba274d0.png align="left")

Enter your username and password, click on login, and change your password.

```plaintext
# bydefault username and password is admin
username admin
password admin
```

Set new password for login.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702184287966/3fa0b289-9c08-4e2c-a07e-61db25ccd699.png?auto=compress,format&format=webp align="center")

Update the new password. This is the Sonar Dashboard, as shown below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702184334262/85d152eb-a13c-421c-a469-52ea229f9648.png?auto=compress,format&format=webp align="left")

**Check Trivy version**

Check the Trivy version in an Ec2 instance.

```plaintext
trivy --version
```

## **Step 4: Install Plugins like JDK, Sonarqube Scanner, NodeJs, and OWASP Dependency Check**

### **4A — Install Plugin**

Goto Manage **Jenkins** →**Plugins** → **Available Plugins**

**Install below plugins**

1: Eclipse Temurin Installer (Install without restart)

2: SonarQube Scanner (Install without restart)

3: Sonar Quality Gates (Install Without restart)

4: NodeJs (Install Without restart)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704012699327/9a6772c8-df4f-43c5-b1d2-eaf5ffa6a6d4.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704012718475/2a5d8e9b-0e32-4cb8-a71b-ceea28a303b1.png align="center")

### **4B: Configure Java and Nodejs in Global Tool Configuration**

Goto Manage **Jenkins** → **Tools** → Install **JDK (17)** and **NodeJs (16)**. Click on **Apply** and **Save**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704012765434/b125a23a-5a0d-466d-9e0c-0a549d7d4af4.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704012813957/8e8d0fc4-efd2-4cf3-b666-e903b9ad8387.png align="left")

## **Step 5: Configure Sonar Server in Manage Jenkins**

Grab the public IP address of your EC2 instance where sonar is running.

Sonarqube works on Port 9000, so &lt;Public IP&gt;:9000.

Go to your Sonarqube server.

### **5A: Create new token in SonarQube**

Click on **Administration** → **Security** → **Users** → Click on **Tokens** and **Update Token**, → Give it a name, and click on **Generate Token**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702185366020/fe4e754a-e0ad-4317-99e8-50884fa07296.png?auto=compress,format&format=webp align="left")

click on update Token

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694160866134/49f34dd2-de41-455c-aee0-f1ffe13d8488.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

Create a token with a name and generate

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704012898117/6ef8c182-faa6-4b23-85a6-76aef0eaeab5.png align="left")

copy this Token

### 5B: Configure SonarQube Credentials

Goto **Jenkins Dashboard** → **Manage Jenkins** → **Credentials** → Add **secret text**. It should look like this

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702186101219/307a7eac-9b0f-47f1-a7c1-3379c21ae0b0.png?auto=compress,format&format=webp align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704012957178/0ae35f1c-4e11-462a-851f-3abdeecf7dbd.png align="left")

You will see this page once you click on create

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704012980748/3dd1c227-66eb-4589-a371-a9037c44b776.png align="left")

### 5C: Configure Sonar Server in Manage Jenkins

Now, go to Dashboard → **Manage Jenkins** → **System** and add like the below image.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704013050680/d8212c86-52cf-4450-bad0-f0f671e8d584.png align="left")

Click on Apply and Save.

**The Configure System option** is used in Jenkins to configure different server

**Global Tool Configuration** is used to configure different tools that we install using Plugins

### 5D: Configure Sonar Scanner in Manage Jenkins --&gt; Tools

We will install a sonar scanner in the tools.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704013124441/630875e9-8f1f-4c21-90f4-79a11b188023.png align="left")

### 5E: Configure Quality gate in SonarQube Server

In the Sonarqube Dashboard, add a quality gate as well.

In the sonar interface, create the quality gate as shown below:

Click on the **quality gate, then create.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702186397756/2fb60e8b-4ceb-433b-bcf7-7187a2b26f90.png?auto=compress,format&format=webp align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704013161763/2f71ec73-0e60-4761-8b50-dd5407dde933.png align="left")

Click on the **save** option.

In the Sonarqube Dashboard, Create **Webhook** option as shown in below:

**Administration--&gt; Configuration--&gt;Webhooks**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704013247203/1c11142a-b9dd-4e28-ae96-7c386449db03.png align="left")

Click on **Create**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704013253860/89bd2d24-332b-4930-b17a-b607a1da6c5c.png align="left")

Add details:

```plaintext
<http://jenkins-private-ip:8080>/sonarqube-webhook/
```

### 5F:Setup new pipeline with name "devsecops-swiggy"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704013450563/139784cd-0d1f-4481-be1f-09bd51276140.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704013478267/7159bdb2-fc4a-4eef-9e43-f794df3c720f.png align="center")

If you want help how to write scripted pipeline, use Pipeline Syntax.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704013570038/d25204cf-0cbb-45de-968f-93da8c961061.png align="center")

Let's go to our pipeline and add the script to our pipeline script.

```plaintext
pipeline{
    agent any
    tools{
        jdk 'jdk17'
        nodejs 'node16'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/dushyantkumark/Swiggy_DevSecOps_Project.git'
            }
        }
}
```

Click on Build now, and you will see the stage view like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704013663211/aa01a69d-50bd-4cf1-8e2b-1cb1b3c71101.png align="left")

Add more stages such as Sonar analysis, quality gate, install dependencies.

```plaintext
        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Swiggy-CICD \
                    -Dsonar.projectKey=Swiggy-CICD '''
                }
            }
        }
        stage("quality gate"){
           steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'Sonar-token' 
                }
            } 
        }
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
```

Click on Build now, and you will see the stage view like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704013774925/0b55e868-5b9a-4474-b858-0a6c4f17d46a.png align="center")

To see the report, you can go to Sonarqube Server and go to Projects.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702186853794/cc3ee1e6-fd9f-4d35-8208-d18abcb7290c.png?auto=compress,format&format=webp align="left")

You can see the report has been generated, and the status shows as passed. You can see that there are 801 lines it has scanned. To see a detailed report, you can go to issues.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704013977579/418eda9e-c80d-4cfa-9392-e686dd43b7cc.png align="left")

## **Step 6: Install OWASP Dependency Check Plugins**

Go to **Dashboard** → **Manage Jenkins** → **Plugins** → **OWASP Dependency-Check**. Click on it and install it without restarting.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694162570631/a0da6454-e85a-4e27-908a-255b024bf834.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

First, we configured the plugin, and next, we had to configure the Tool

Goto **Dashboard** → **Manage Jenkins** → **Tools** →

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704014012424/f8d83c57-74a5-4289-abb7-d753dab353ad.png align="left")

Click on **Apply** and **save** here.

Now go to **Configure** → Pipeline and add this stage to your pipeline and build.

```plaintext
stage('OWASP FS SCAN') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ --disableYarnAudit --disableNodeAudit', odcInstallation: 'DP-Check'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('TRIVY FS SCAN') {
            steps {
                sh "trivy fs . > trivyfs.txt"
            }
        }
```

Click on Build now, and you will see the stage view like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704014485555/fe9ad62f-f9a2-45a7-8e72-0f3c7ac3046e.png align="center")

You will see that in status, a graph will also be generated for vulnerabilities.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698225711345/5765f1cb-fd23-416b-a25b-2157083bd213.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

## **Step 7: Docker Image Build and Push**

We need to install the Docker tool on our system.

Go to **Dashboard** → **Manage Plugins** → **Available plugins** → Search for **Docker** and install these plugins.

Install these plugins:

* Docker
    
* Docker Commons
    
* Docker Pipeline
    
* Docker API Docker-build-step
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702187503440/4e287534-ef71-40c5-b9d0-0a40bcd3978e.png?auto=compress,format&format=webp align="left")

Now, goto **Dashboard** → **Manage Jenkins** → **Tools** →

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704014192072/a20d7b52-6d62-4013-8bc6-940ccd3c3871.png align="left")

Now go to the Dockerhub repository to generate a token and integrate with Jenkins to push the image to the specific repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704015001943/9bf3ac22-69cf-4d4f-ba59-c7207ebf3249.png align="center")

Click on that **My Account,** --&gt; **Security --&gt; New access token** and copy the token.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704014286114/2a1a8257-1123-40b7-b2e7-2d6adad55038.png align="left")

Goto **Jenkins Dashboard** → **Manage Jenkins** → **Credentials** → Add **secret text**. It should look like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704014306916/163fac91-5482-49e0-b78a-a952027a2095.png align="left")

Add this stage to Pipeline Script.

```plaintext
stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker'){ 
                    app.push("${env.BUILD_NUMBER}")  
                       sh "docker build -t swiggy-app ."
                       sh "docker tag swiggy-app dushyantkumark/swiggy-app:latest "
                       sh "docker push dushyantkumark/swiggy-app:latest "
                    }
                }
            }
        }
        stage("TRIVY IMAGE SCAN"){
            steps{
                sh "trivy image dushyantkumark/swiggy-app:latest > trivyimage.txt" 
            }
        }
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704014644074/298dda0a-7552-45b8-b15c-054be6eebe45.png align="left")

When you log in to Dockerhub, you will see a new image is created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704014578219/c98565a1-c31d-4928-99c7-0cdb26195877.png align="left")

Now test the swiggy application is running or not.

Add this stage to Pipeline Script.

```plaintext
stage("Depoy to container"){
            steps{
                sh "docker run -d -p 3000:80 --name swiggy dushyantkumark/swiggy:latest" 
            }
        }
```

Now access your application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704015354727/80885ee8-1216-4db3-85be-d2f8bb5b2376.png align="center")

## **Step 8: Creation of EKS Cluster with ArgoCD**

**Installation of KUBECTL, EKSCTL, AWS CLI are done at the time of ec2 instance creation using terraform.**

### 8A: Creation of EKS Cluster

**Now let's configure aws cli credentials for eks creation in us-east-1 region.**

```plaintext
aws configure
# add accessKey, secretAccessKey, region, output format.
```

**Command to Create EKS Cluster using eksctl command:**

```plaintext
eksctl create cluster --name <name-of-cluster> --region <regionName> --node-type <instance-type> --nodes-min <min-no-of-nodes> --nodes-max <max-no-of-nodes>

eksctl create cluster --name swiggy-cluster --region us-east-1 --node-type t2.medium --nodes-min 2 --nodes-max 4
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704015966713/9557467d-2132-4e25-b4a3-894db1ceb4c8.png align="left")

**It will take 10–15 minutes to create a cluster.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704015994132/55de78a9-54ad-430a-ae6b-31d991e43a75.png align="left")

Check your cloudformation stack and ekscluster.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704016339685/bf02d855-60ef-43de-86ce-9dc864a23373.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704016346539/9d6ab9c4-f2b5-4c8a-a49e-29962bade565.png align="center")

As you will see in the EC2 instances nodes running in the name of EKS Cluster (swiggy-cluster) as shown below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704016082621/4060b404-2c21-4be5-8dc4-83d9dbf108a1.png align="left")

**EKS Cluster is up and ready and check with the below command.**

```plaintext
kubectl get no
kubectl get po
```

### 8B: Installing ArgoCD

**Now let's install ArgoCD in the EKS Cluster.**

```plaintext
kubectl create ns argocd
# This will create a new namespace, argocd, where Argo CD services and application resources will live.
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.4.7/manifests/install.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702189008925/f8ba1a3f-e38d-446b-9d07-211cf135ec8a.png?auto=compress,format&format=webp align="left")

**Download Argo CD CLI:**

```plaintext
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
```

**Access The Argo CD API Server:**

```plaintext
# By default, the Argo CD API server is not exposed with an external IP. To access the API server, 
choose one of the following techniques to expose the Argo CD API server:
* Service Type Load Balancer
* Port Forwarding
```

**Let's go with Service Type Load Balancer.**

```plaintext
# Change the argocd-server service type to LoadBalancer.
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

Wait about 2 minutes for the LoadBalancer creation

```plaintext
export ARGOCD_SERVER=kubectl get svc argocd-server -n argocd -o json | jq --raw-output '.status.loadBalancer.ingress[0].hostname'
```

The initial password is autogenerated with the pod name of the ArgoCD API server.

```plaintext
export ARGO_PWD=`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`
```

NOW get the loadbalancer url and argocd password.

```plaintext
echo $ARGOCD_SERVER
echo $ARGO_PWD
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704016803089/a6f2bb6a-3252-4145-9f08-65f8d9655e10.png align="center")

**List the resources in the namespace:**

```plaintext
kubectl get all -n argocd
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704016850769/860a43e5-1855-4b97-adb9-1a9f57115176.png align="left")

**Get the load balancer URL:**

```plaintext
kubectl get svc -n argocd
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704016886620/9be46127-7970-4189-93ab-ece98c772704.png align="left")

Lets create new namespace for application.

```plaintext
kubectl create ns swiggy
```

Pickup the URL and paste it into the web to get the UI as shown below image:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704016910300/98c59dd5-984d-49f8-bc12-b8906e8ce1c1.png align="left")

**Login Using** ARGO\_PWD**:**

```plaintext
echo ARGO_PWD
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704017063517/334def6c-870d-4a1f-baf0-763773272348.png align="left")

Login with the admin and Password in the above you will get an interface as shown below:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702189214666/11a907bb-59b7-43b3-9458-c411fe842c2b.png?auto=compress,format&format=webp align="left")

**Lets connect with github repository:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704017304636/af40ae63-04c7-4d71-840d-2ba90211b1f5.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704017328574/97038a3a-2a7e-46a9-84b3-ea01724d4b7c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704017360030/b2b925ba-a724-4e0f-b710-6c3cb6946231.png align="center")

Now deploy an application, first we have to configure the details in Application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704017560584/d4d54483-c54c-47bf-b652-ebb18823f21b.png align="center")

**Enter the Repository URL, set path to ./, Cluster URL to** **kubernetes.default.svc, the namespace to swiggy and click save.**

The GitHub URL is the Kubernetes Manifest files which I have stored and the pushed image is used in the Kubernetes deployment files.

**Repo Link:** [https://github.com/dushyantkumark/Swiggy\_DevSecOps\_Project.git](https://github.com/dushyantkumark/Swiggy_DevSecOps_Project.git)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704017743945/23eb587e-57e5-4c29-b3bb-fcfada8df0a9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704017710314/8b1da791-954e-4445-84e4-2bcec33fceca.png align="left")

**You should see the below, once you're done with the details.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704017762713/69727f2e-4897-414a-9d73-62784ee048eb.png align="left")

**Click on it.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704017807297/2c1e3c64-e8d3-4239-a2d5-7aa6b063447a.png align="left")

**You can see the pods running in the EKS Cluster.**

```plaintext
kubectl get po -n swiggy
kubectl get all -n swiggy
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704017847377/db478684-26ec-4f7f-8e1e-630389772bb6.png align="left")

With the above load balancer, you will be able to see the output as shown in the below image:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704017950245/ab595de3-7a11-446f-8026-013859ec3df6.png align="left")

## **Step 9: Clean up your resources**:

* Delete your Cluster
    

```plaintext
eksctl delete cluster --name swiggy-cluster
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704018262728/11f6470f-6e02-4a45-9af5-1898c2bf86a0.png align="center")

* Destroy your Infrastructure using terraform from your laptop (windows)
    

```plaintext
terraform destroy
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704018461060/48906b6a-383a-4795-9a32-57ec3cf14479.png align="center")

* Delete IAM credentials you create, remove policies from users.
    

## Conclusion:

In this project, we have covered the essential steps to deploy a Swiggy app with a strong focus on security through a DevSecOps approach. By leveraging tools like Terraform, Jenkins CI/CD, SonarQube, Trivy, Argocd, and EKS, we can create a robust and secure pipeline for deploying applications on AWS.

Remember that security is an ongoing process, and it is crucial to stay updated with the latest security practices and continuously monitor and improve the security of your applications. With the knowledge gained from this guide, you can enhance your DevSecOps skills and ensure the smooth and efficient deployment of secure applications on Amazon Web Services.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.

#docker #aws #cloudcomputing #Devops #kubernetes #devsecops #sonarqube #trivy #owasp #TrainWithShubham #90daysofdevopsc #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Github</mark>**: [https://github.com/dushyantkumark/Swiggy\_DevSecOps\_Project.git](https://github.com/dushyantkumark/Swiggy_DevSecOps_Project.git)