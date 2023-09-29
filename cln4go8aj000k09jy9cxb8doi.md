---
title: "Episode 2 : 2 Tier Application Deployment🔥"
datePublished: Fri Sep 29 2023 10:28:28 GMT+0000 (Coordinated Universal Time)
cuid: cln4go8aj000k09jy9cxb8doi
slug: episode-2-2-tier-application-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695973602595/81e6e478-7b3c-4027-93db-773b4ba224be.png
tags: docker, aws, 90daysofdevops, trainwithshubham, 2tier-architecture

---

**Hello, learners in today's topic we will deploy a 2-Tier Application Deployment with the Help of Various DevOps Tools.**

## **📌 Prerequisites**

Here are some prerequisites for this project are given below:

* AWS EC2
    
* Git & GitHub
    
* Docker
    
* DockerHub
    

## 📌 Create an Ec2 instance

* **Log in to your AWS account with username and Password.**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695967521298/77f3eb48-f9b9-4a9e-8619-b5065051aa9e.png align="center")
    
* **Click on the Launch instance option on the right side.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695967544349/4a188131-fe0b-456d-bb76-9013c63ffda4.png align="left")

* **Now give the instance name and choose operating system image.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695967603979/24cfa8cb-b339-47f2-9a80-e3ea7da848e7.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695967728803/63695f7d-d25d-4a57-a2c6-6e393b3d724c.png align="center")

* **Select the instance type (t2.micro) and create a new key pair.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695967832393/5c353c5d-bcc7-4951-b1fe-2b1d727412ac.png align="left")

* **Now configure the network setting, storage and then launch your instance.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695967971772/1a1a270a-e7db-4e3f-97ca-d21731e5bcc2.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695967983829/e322d4bd-2024-4c82-be48-511ce5a1099b.png align="center")

* **Now click on the Connect Button when your instance is in the Running Condition.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695968037371/d7b30ee5-c530-4019-a850-9459c8a74c27.png align="left")

## 📌 Installing, configuring and troubleshooting the application

* **First, ssh your instance then run the following command for the Package update and Docker Installation.**
    
    ```plaintext
    ssh -i "docker.pem" ubuntu@<public_dns>
    or
    ssh -i <"key_name"> <user_name>@<public-ip>
    ```
    
    ```plaintext
    sudo apt-get update -y ; sudo apt install docker.io -y
    ```
    

Run the following command for the Package update and Docker Installation.

* Troubleshoot the docker permission denied problem.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695968430060/c59348a8-f07b-4c5a-be95-f0c347352051.png align="center")
    
* **Clone the Repository from the git hub, copy the SSH and paste it into the terminal here is the command.**
    

```plaintext
https://github.com/dushyantkumark/two-tier-flask-app.git
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695968605816/a5a8111d-a792-455b-b3a1-f0996186b361.png align="left")

* **Write a Docker for the Python installation and Mysql Client.**
    

```plaintext
# Use an official Python runtime as the base image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# install required packages for system
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y gcc default-libmysqlclient-dev pkg-config \
    && rm -rf /var/lib/apt/lists/*

# Copy the requirements file into the container
COPY requirements.txt .

# Install app dependencies
RUN pip install mysqlclient
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code
COPY . .

# Specify the command to run your application
CMD ["python", "app.py"]
```

* **After Writing the Docker file Now build it with the following commands it includes 1/8 Steps which I have Mentioned in the Screenshot.**
    

```plaintext
docker build -t flaskapp-2tier .
docker images
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695968721747/d2bb8445-f23f-492f-8830-0a3dda542077.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695968751102/91313fd3-2574-498b-a46d-0d0ef6593c10.png align="center")

* **Now Run the docker Container with the help of Docker images with Port Number with the help of the Below command.**
    

```plaintext
docker run -d -p 5000:5000 flaskapp-2tier:latest
docker ps 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695969121603/d36bbb75-7fe7-48e2-bdd1-ec82bfe433c3.png align="left")

* **Now open the Port in our Security Groups for Incoming Traffic and allow port no 5000.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695969230509/c2673a0d-7e1a-4c19-b14a-b5ed3e552397.png align="left")

* **Now Access the app with the help of the Public IP of Ec2 Instance with port no here is the Syntax:-**
    

```plaintext
http://13.232.124.66:5000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695969399679/4cdcece7-19ae-42e1-8963-d32d0c4dbacc.png align="left")

**We need to create a MySQL Container.**

```plaintext
docker run -d -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD="myadmin" mysql:5.7
docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695969623855/29d773b9-06d6-464c-b1d4-b5d5e6207294.png align="center")

* **Now Access the app with the help of the Public IP of Ec2 Instance with port no here is the Syntax:-**
    
    ```plaintext
    http://13.232.124.66:5000
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695969807844/2b16dc6c-6b60-4fb3-b461-16308bffacdd.png align="center")

Both containers are **<mark>not communicating</mark>** with each other because both containers are <mark>not in the same network</mark>. To solve this problem we have to create a **<mark>custom bridge network</mark>**.

* **We need to create a docker network 2tier to connect MySQL Container and MySQL Database.**
    

```plaintext
docker network create twotier
docker network ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695970016812/02b7736c-3510-4eaa-857f-4f39c1eb655b.png align="left")

* **Stop previous running containers, before creating new containers.**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695970200010/25c53a99-4614-49e0-a056-f40446c7223d.png align="center")
    
* **As per the Diagram need a MySQL Container with username and Password to use these commands to run I have to use the Environment Variable in these with -e.**
    

```plaintext
sudo docker run -d -p 5000:5000 --network=twotier -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=myadmin -e MYSQL_DB=myDb flaskapp-2tier:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695970310622/cb309858-5808-4853-9ff0-3acd11dc3c6d.png align="left")

* **As per the Diagram need a MySQL Database username and Password use these commands to run I have used the Environment Variable in these with -e and run the mysql image latest.**
    

```plaintext
sudo docker run -d -p 3306:3306 --network=twotier -e MYSQL_DATABASE=myDb -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin -e MYSQL_ROOT_PASSWORD=admin mysql:5.7
docker ps 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695970669963/910cb0b0-da2c-4b39-9f29-508cba162e3e.png align="left")

As per the Diagram need a MySQL Database username and Password to use these commands to run I have used the Environment Variable in these with -e and run the MySQL image latest Diagram.

* **Check the Network of Both Containers and Inspect both containers on the Network with the help of the below command.**
    

```plaintext
docker network ls 
docker network inspect twotier
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695970850530/16179a53-08c7-4f57-afb7-54ac29ffcd46.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695970921691/fc9e457e-b231-4ae4-8c0e-a45d25308d93.png align="center")

* **Now your MySql Container and MySql Database are connected.**
    
    ```plaintext
    http://13.232.124.66:5000
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695971223343/79a8b8e8-006f-41e8-8cad-51c679e678c2.png align="center")
    
* **Create the Message table in your MySQL Database but before creating a table access the MySql Database and then enter in the mysql with the following commands.**
    

```plaintext
sudo docker exec -it <container-id> bash
sudo mysql -u root -p
enter password
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695971244727/53334171-4f82-4189-813c-468ccb6985af.png align="left")

* **Check the Databases, use myDb and then create a table with the help of the following commands. use the syntax directly copy and paste to your terminal.**
    

```plaintext
show databases;
use myDb;

CREATE TABLE messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    message TEXT
);

```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695971559838/6b78b7bd-0a16-4810-9f7c-6c38abe2f6e2.png align="left")

* **After Creating the table access your 2-Tier Flask Deployment App on your browser: with the help of the following syntax:**
    

```plaintext
http://<ec2-instance-public-ip>:5000
http://13.232.124.66:5000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695971642639/4a545adc-bf8e-458f-8f88-1a71393a1952.png align="left")

* **Add some messages and submit them for testing purposes.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695971733332/f5287f21-c651-43cb-921a-eb3fff59e910.png align="center")

* **Verify that data in the database.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695971808498/dee47ec0-28c0-41c8-830e-ee7938a11b8b.png align="center")

## 📌 Push Your Docker Image To DockerHub

* **Login to your docker hub account.**
    
    ```plaintext
    docker login
    Username: <dockerhub_username>
    Password: <dockerhub_password>
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695971964372/d7c1211a-22c6-4483-b211-a79be8769e9c.png align="center")

* **Again tag your docker image with your dockerhub username.**
    
    ```plaintext
    docker images
    docker tag flaskapp-2tier:latest dushyantkumark/2-tier-flask-app:latest
    docker images
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695972435060/4de0508f-584e-444b-bff5-4ea4d4595c49.png align="center")

* **Push your tagged docker image to your docker hub account.**
    
    ```plaintext
    docker push dushyantkumark/2-tier-flask-app:latest
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695972137756/02091f9a-41de-44b1-b4f2-03a5906b63c5.png align="center")

* **Check your docker image in the docker hub account.**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695972185970/403c0dd0-ae7a-47c0-8cf6-10bac7df295f.png align="center")
    

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.😊

#aws #cloudcomputing #docker #Devops #TrainWithShubham #90daysofdevopsc #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)

**<mark>GitHub</mark>**: [https://github.com/dushyantkumark/two-tier-flask-app.git](https://github.com/dushyantkumark/two-tier-flask-app.git)