---
title: "Docker Intro"
datePublished: Mon Jun 12 2023 03:30:39 GMT+0000 (Coordinated Universal Time)
cuid: clisar1x40bjwemnv1hjt5iua
slug: docker-intro
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686490338576/6fbc3da9-61d1-4e76-87f7-b550e8dfd3e4.png
tags: docker, docker-images, 90daysofdevops, trainwithshubham

---

# 🌟**Introduction**

In our day-to-day life, we interact with many applications on our smartphones, tablets, or computers – games, educational apps, and a lot more. But have you ever wondered how these applications are available at any time? They're deployed by using different tools, one of the tools as docker.

# 🌟**BEFORE CONTAINERS**

Let us dial back the clock. Back when computers were a novelty, and companies wanted to run their applications, they would have had to buy a server for doing so. However, this came with a caveat: you could only run one application per server. If you wanted to run multiple applications, you would have to buy as many servers. As costs would skyrocket, this was a problem, for both the company and the environment on a larger scale

IBM fixed this issue by introducing the concept of *virtual machines* into the game. With them, we could run multiple applications on the same server. You may have heard of / done dual booting on your PC; like installing Windows on your Mac device or Ubuntu on Windows. These are virtual machines. However, they had a problem as well. They needed their own operating system, which tended to take up a lot of memory and storage on your hard disk. This made them slow and not so efficient.

# 🌟What is Container

Let’s say you built a website that works well on your system but your friend runs into some problems with it when they try using it on their computer. To avoid such hassles, you can use a container, which would ship the entire website along with its dependencies, such as the web database, front end, back end, source code, etc. This would ensure that the website runs smoothly.

In computing terms, containerization is an efficient method for running, deploying and scaling applications.

# 🌟**CONTAINER VS VIRTUAL MACHINES**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686495239422/7d3716f7-311e-4d24-938d-5b19b25a6bb7.png align="left")

Any application which runs on a virtual machine will require a guest OS to run, which would require a hypervisor. A hypervisor manages the virtual machines and is used to create multiple machines on the host operating system. As you can see from the picture, every OS would require a dedicated amount of space in the hardware, which is *virtually* divided.

In the case of containers, you need to have only one operating system, and on top of that, you have a container engine, on which you run applications. They use the idea of isolating your application from the main operating system.

To sum it up succinctly, virtual machines use multiple operating systems to run multiple applications whereas containers use only the host operating system to run applications via the container engine.

In reality, however, containers run on top of virtual machines. You can say they are a lightweight alternative.

# 🌟**WHAT IS DOCKER**

Docker is one among many container platforms that allows you to build such containers to test, build and scale applications rapidly and easily by running them in isolated environments.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686492244886/935dd4bc-cc82-49f7-8755-006a86004d19.png align="center")

# 🌟**WHY USE DOCKER**

• Helps transport code faster

• Makes scaling, deploying and identifying issues in the application easier

• Saves up space as you don’t need to install the whole application locally

# 🌟**DOCKER TERMINOLOGIES**

## **🔹Docker Runtime**

It allows us to start and stop containers. There are two types:

(i) Low-level runtime (runc)

(ii) High-level runtime (containerd)

## **🔹Docker Client**

It is what we use to interact with Docker. You can think of it as the user interface for Docker. Whenever you type in a command, the client sends these to the daemon.

## **🔹Docker CLI**

It allows users to issue commands to the Docker Daemon. Docker uses a client–server architecture.

![ARCH.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646204553850/Bfhoxb-UH.png?auto=compress,format&format=webp align="left")

## **🔹Docker Engine**

It is responsible for the overall functioning of the Docker platform. It is a client-server-based application with three components:

(i) Server – which runs the daemon

(ii) Rest API – deals with the interaction of applications with their server

(iii) Client – which is nothing but the command line interface (CLI)

## **🔹Docker Daemon**

It is the heart of the Docker architecture, which does the crucial work of building, running, and distributing the containers. It also manages the Docker images and the containers.

## **🔹Docker Image**

The file that contains the source code, and operating system files to run the application along with its other dependencies inside the container is called Docker image. A containerized application is the running instance of an image. Docker images are immutable.

## **🔹Dockerfile**

It contains the list of instructions to create Docker images.

## **🔹Docker Registries**

This is where Docker images are stored. Docker Hub is the official online public repository of Docker where you can find all the images of popular applications. Docker Hub also allows us to create our own images for our application.

# 🌟Convert the docker file to Container

To convert a Dockerfile into a Docker container, you need to follow these steps:

* Create Docker file
    
* Build the Docker Image
    
* Verify the image
    
* Run the container from that image
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686494225029/82ae457f-64db-46ba-87a0-5819c6cbb471.png align="center")
    

# 🌟Conclusion

So there it is, folks! Docker, in simple terms, is a fantastic tool that helps create and deliver software applications conveniently and reliably.

Although Docker sounds a bit technical, just remember that even the most complex things can be understood when related to something fun and familiar.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#docker #docker container #docker hub #DevOps #TrainWithShubham

#90daysofdevopsc #happylearning

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)