---
title: "Dockerfile! (Dockerize Python Application)"
datePublished: Tue Jun 13 2023 07:52:29 GMT+0000 (Coordinated Universal Time)
cuid: cliu7c6nr03q3rhnv29ht8t92
slug: dockerfile-dockerize-python-application
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686640103024/b2d246e5-6cfb-4217-b1cd-1cfb6ca97389.png
tags: docker, devops, docker-images, 90daysofdevops, trainwithshubham

---

# image

# 🌟**How to build the docker file to a running Container?**

To convert a Dockerfile into a Docker container, you need to follow these steps:

* Create Docker file
    
* Build the Docker Image
    
* Verify the image
    
* Run the container from that image
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686635495274/b5f23272-8441-485e-b360-96b9f76dbd8e.png align="center")
    

# 🌟What is a Docker file?

* A Dockerfile is a text file that contains a series of commands or instructions.
    
* These instructions are executed in the order in which they are written.
    
* Execution of these instructions takes place on a base image.
    
* You will use a Dockerfile to create your own custom Docker image
    

# 🌟How to write Dockerfile?

Let's go through the step-by-step process of writing a Dockerfile with an example:

**Step 1**: Choose a **<mark>Base Image</mark>** Let's say we want to build a Docker image for a simple Python application. We'll choose the official <mark>Python base image</mark> as our starting point.

```plaintext
# Use a base image with Python pre-installed
FROM python:3.9-slim
```

**Step 2**: Set the **<mark>Working Directory</mark>** Specify the working directory inside the container where our application code will be copied and executed.

```plaintext
# Set the working directory inside the container
WORKDIR /app
```

**Step 3**: **<mark>Copy</mark>** Files Copy the application files from the host machine to the container's working directory.

```plaintext
# Copy the application files to container app directory 
COPY . /app
```

**Step 4**: **<mark>Install Dependencies</mark>** Since our Django application has dependencies defined in the requirements.txt file, we need to install them inside the container.

```plaintext
# Install all the dependencies written in requirement.txt
RUN install -r requirements.txt
```

In the **<mark>requirement.txt</mark>** file, what dependencies do you want to install according to your project?

```plaintext
asgiref==3.2.3
Django==3.0.3
django-cors-headers==3.2.1
djangorestframework==3.11.0
pytz==2019.3
sqlparse==0.3.0
```

**Step 5**: **<mark>Expose Ports</mark>** Specify which ports should be published when running a container from the image. In this case, we'll expose port <mark>8001</mark>, which is the port our Django application will be listening on.

```plaintext
# Expose port 8001 for the application
EXPOSE 8001
```

**Step 6**: Define **<mark>CMD</mark>** the Startup Command Specify the command that should be executed when a container is launched from the image. In this case, we'll run our Django application using the command given below.

```plaintext
# Set the command to run when the container starts
CMD ["python", "manage.py", "runserver", "0.0.0.0:8001"]
```

# 🌟**How to build Docker image?**

Build the Docker Image Open a terminal or command prompt, navigate to the directory containing the Dockerfile, and run the following command to build the <mark>Docker image</mark>:

```plaintext
docker build -t my-djando-app .
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686642589808/479c9838-9d8b-4f12-ad30-3d3ffd85e00c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686642022299/96c30c7a-214d-46ba-aafe-2e71d95b867e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686642060723/97653752-c7ed-4c91-aeff-c308098fa9e1.png align="center")

# 🌟How to verify the Docker image?

Every Docker image has a unique identifier called the **<mark>Image ID</mark>**. You can check the ID of a locally available image using the command. Look for the image name and corresponding ID in the output.

```plaintext
docker images
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686642096409/2a9f8c67-2a82-48ee-80de-739542c44c8f.png align="center")

# 🌟How to run Docker Container?

Run the Docker Container Once the Docker image is built and verify the image. You can create and run a container from it using the following command:

```plaintext
docker run -d -p 8001:8001 --name django-app-cont my-django-app
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686642115236/694c25f8-42a3-4ad5-a85b-7e698bb0567c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686642145940/3f23f228-ec77-4d90-93fc-f203a147f916.png align="center")

In the above command <mark>'-d'</mark> daemon process or background process, **<mark>'-p' or '--publish'</mark>** it maps port 8001 of the container to port 8001 of the host machine, <mark>'--</mark>**<mark>name'</mark>** gives the name to the container you create.

You have to specify <mark>inbound</mark> and <mark>outbound</mark> rules before accessing your application on the web.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686642302345/a9ec4bae-2879-4c5d-82c5-7fdb15623ade.png align="center")

Now you have a Dockerfile that builds a Docker image for a <mark>Python Django</mark> application. Running the container in <mark>daemon mode</mark> will start your application on port 8001, and you can access it from your ec2 instance machine by visiting **<mark>http://ip-address-ec2-instance:8001</mark> .**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686642363132/467b5d1a-3b4a-4e34-924d-e6376129f14d.png align="center")

Docker Commands <mark>Comming soon</mark> on **<mark>Linkedin</mark>**, the link is given below.

THANKS!!

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#docker #docker container #docker hub #DevOps #TrainWithShubham

#90daysofdevopsc #happylearning

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)