---
title: "Docker Volume"
datePublished: Wed Jun 14 2023 11:11:06 GMT+0000 (Coordinated Universal Time)
cuid: clivm2wk7001h09l0faip4yze
slug: docker-volume
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686730387546/dbd5fdc0-ea71-4399-95e9-76ec5ddb4e06.webp
tags: docker, devops, docker-volume, 90daysofdevops, trainwithshubham

---

## 🌟**Introduction:**

Docker volumes play a crucial role in managing data persistence and sharing between containers in Docker. They provide a convenient way to store and access data, ensuring that valuable information remains intact even if containers are stopped, started, or replaced. In this post, we will explore Docker volumes in depth and walk through a simple hands-on example to help you grasp the concept and get started with using volumes effectively.

## 🌟What are Docker Volumes?

Docker volumes are special **<mark>directories</mark>** or **<mark>named entities</mark>** that exist outside the container's file system. They serve as a dedicated space for storing and sharing data between <mark>containers(one container to another container)</mark> or between a <mark>container and the host system</mark>. With volumes, you can separate data from containers, allowing for easier management, data persistence, and seamless collaboration between containers.

When you run applications inside Docker containers, you might have to store and access data. Docker volumes provide a way to do it.

Think of a Docker volume as a special directory/folder that exists outside the container. It's like a <mark>shared storage</mark> space that <mark>multiple containers</mark> can use to store and retrieve data.

### **🔹**Using Docker volumes has a few advantages:

**<mark>Data Persistence:</mark>** Volumes allow data to persist even if containers are stopped or deleted. So you don't lose important information when containers are recreated or updated.

**<mark>Sharing Data:</mark>** Volumes enable <mark>multiple containers</mark> to share the same data. This is useful when you have different containers that need access to the same files or information.

**<mark>Separation from Containers</mark>:** Volumes are separate from the containers themselves. This means you can update or replace containers without affecting the data stored in volumes.

Creating and using a volume is like creating a special folder on your computer. You can give it a name and then associate it with one or more containers. Containers can read from and write to this volume, just like accessing files on their filesystem.

For example, imagine you have a web application running in a Docker container. You can create a volume to store the application's data, such as user uploads or configuration files. This volume can be linked to the container, allowing the application to read and write data in that volume. If you update or replace the container, the data in the volume remains intact.

## 🌟Hands-on Example:

Storing Application Data with Docker Volumes Let's dive into a practical hands-on example that demonstrates the usage of Docker volumes for storing application data.

**<mark>Step 1:</mark>** Create a Docker Volume Open your terminal or command prompt and create a Docker volume using the following command:

```plaintext
docker volume create my_volume
```

This command creates a volume with a specific name called "**<mark>my_volume</mark>**". You can choose any name you prefer.

**<mark>Step 2: </mark>** Run a Container with the Volume Next, let's run a Docker container and attach the volume we created. Execute the following command:

```plaintext
docker run -d -v my_volume:/data --name my_container nginx
```

Here, we run an Nginx container and mount it to the "**<mark>my_volume</mark>**" volume. The volume is mounted to the "/data" directory inside the container and we name the container called "**<mark>my_container</mark>**".

**<mark>Step 3:</mark>** Verify the Volume To ensure the volume is successfully created and attached to the container, inspect it using the following command:

```plaintext
docker volume inspect my_volume
```

This command provides <mark>detailed information</mark> about the volume you created '**<mark>my_volume</mark>**', which also includes its 'mountpoint'.

**<mark>Step 4:</mark>** Access the Volume To access the volume from <mark>within the container</mark>, we'll use a command inside the container's shell. Use the following command:

```plaintext
docker exec -it my_container /bin/bash
```

This command enters the container's shell. Once you enter into a running container then go to '<mark>/data</mark>' directory.

```plaintext
cd /data
```

Now, you have access to your volume and can perform operations like creating files or directories etc.

**<mark>Step 5:</mark>** Test Data Persistence Let's test the data persistence of the volume. Create a file inside the container "/data" directory using the following command:

```plaintext
echo "Hello, Docker Volume!" > test.txt
```

Exit the container's shell by typing **<mark>exit</mark>**.

**<mark>Step 6: </mark>** Inspect the Volume on the Host To verify data persistence, inspect the volume on the host machine. Run the command:

```plaintext
docker inspect my_volume
```

Look for the "Mountpoint" field in the output, which indicates the location on the host where the volume is stored. You should find the "<mark>test.txt</mark>" file inside that directory.

## 🌟Conclusion:

Docker volumes provide a powerful mechanism for managing data persistence and sharing in Docker containers. By separating data from containers and leveraging volumes, you can ensure the integrity and availability of your application's data. In this blog post, we explored the concept of Docker volumes and walked through a simple hands-on example, enabling you to create and use volumes effectively in your Dockerized applications.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#docker #dockercontainer #dockervolume #DevOps #TrainWithShubham

#90daysofdevopsc #happylearning

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)