---
title: "Docker Networking"
datePublished: Fri Jun 16 2023 04:20:25 GMT+0000 (Coordinated Universal Time)
cuid: cliy2aged000d09mlgayhf0gg
slug: docker-networking
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686814190964/52ff4218-eb47-455a-a113-965e1e39a4dd.png
tags: docker, networking, docker-network, 90daysofdevops, trainwithshubham

---

## 🌟 **Docker Overview**

Docker is an open platform for developing, shipping and running applications. To read more about Docker [CLICK](https://hashnode.com/edit/clisar1x40bjwemnv1hjt5iua).

## 🌟 What is Docker Networking?

Docker Networking is a way in which Docker containers connect to other containers on the same host or different hosts and also to the outside world, i.e., through the internet.

Docker’s networking subsystem is pluggable using drivers. Several drivers exist by default and provide core networking functionality.

There are various kinds of Docker networks such as:

* Bridge Network
    
* Host Network
    
* None Network
    
* MACVLAN and IPVLAN Networks
    
* Overlay Network
    

### **🔹** About Docker Networking

In this article, we discuss the various available docker networks and try to implement those to have hands-on experience in getting started with various network types.

So, let's get started.

To view all the available networks on a system, use the given command:

```plaintext
docker network ls
```

## 🌟 Bridge Network

### **🔹** Default Bridge Network

Whenever we install docker, it creates a <mark>default bridge network</mark> to which all the containers with no defined network can be connected.

It is a solution to provide isolation of containers from the underlying host network.

If we inspect this network, we will find the following:

```plaintext
docker inspect bridge
```

![Screenshot 2022-04-03 at 8.54.14 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648999457746/zJSueVVHn.png?auto=compress,format&format=webp align="left")

This is one of the most important parts of the output.

We see that a separate interface(**docker0**) is created with a specific **<mark>Subnet</mark>** and **<mark>Gateway</mark>**. Any docker container launched in this network will take up IP addresses from the specified network only.

We spin up an nginx container with no network specified:

```plaintext
docker run -d -p 8080:80 --name mynginx1 nginx
```

***<mark>--name</mark>*** =&gt; It defines the name of the container.

***<mark>-p</mark>*** =&gt; This option maps the <mark>container's port 80</mark> to the <mark>host's port 8080</mark>. It allows you to access the NGINX web server running inside the container by visiting [`localhost:8080`](http://localhost:8080) on your host machine.

***<mark>-d</mark>*** =&gt; This runs the container in detached or daemon mode, i.e., the background.

***<mark>nginx</mark>*** =&gt; It is the name of the image we are using.

Now, let us spin up another container similarly:

```plaintext
docker run -d -p 8081:80 --name mynginx2 nginx
```

```plaintext
docker inspect mynginx1 mynginx2 | grep IPAddress
```

View their IP Addresses.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686815398712/4e0241d6-a731-431c-91cc-e6cd3f843271.png align="left")

*<mark>mynginx1</mark>* has IP <mark>172.17.0.2</mark> and *<mark>mynginx2</mark>* has IP <mark>172.17.0.3</mark>. This proves that are connected to the <mark>default host bridge</mark>.

But this has disadvantages. However, the bridge is an isolation solution from the host network. If no network is specified, we can't get isolation as all containers will connect to this default bridge only. Docker solves this issue with the help of <mark>custom bridge networks</mark>.

### **🔹** Custom Bridge Network

Creating a custom bridge network will create its <mark>own separate Network ID</mark>, interface, Subnet and Gateway.

This will help to create isolated infrastructures.

```plaintext
docker network create custom
```

Let us inspect this to view the above details:

```plaintext
docker inspect custom
```

![Screenshot 2022-04-03 at 9.25.03 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649001328645/fI4X3gmEz.png?auto=compress,format&format=webp align="left")

Launch a container in this network and view that its IP is in the subnet of the custom bridge.

To launch use the *<mark>--network</mark>* <mark>tag</mark>:

```plaintext
docker run -d -p 8082:80 --name mynginx3 --network custombridge nginx
```

*One can log into a container and ping other containers in the same network to test the implementation*.

## 🌟 Host Network

Sometimes we do not require isolation from the host, we can simply spin up the container on the host network and use the host network directly.

```plaintext
docker run -d --name hostnginx --network host nginx
```

We do not use the *\-p* tag here because there is <mark>no connection</mark> to any other network. This will launch the container in the host network.

## 🌟 None Network

This network is useful when there exists a container that requires complete isolation from any kind of network.

Use *<mark>--network none</mark>* in this case.

## 🌟 MACVLAN and IPVLAN Networks

They are generally used for applications that are running on the host but a separate IP address, different than the physical network, is required for them.

One can use the MACVLAN network driver to assign a MAC address to each container’s virtual network interface, making it appear to be a physical network interface directly connected to the physical network.

If we have some services (with well-defined ports) running on the system, and we want to launch these services but can not ask the container to expose it to a not well-defined port. For example, if we are already running nginx on port 80 (a well-defined port for nginx), and we want a new nginx service, we will have to expose it to a different port on the host. But as it is cumbersome to do so, we can use MACVLAN here.

To create one we can use:

```plaintext
docker network create -d macvlan --subnet x.x.x.x/20 --gateway x.x.x.x -o parent=eth0 macnetwork
```

The subnet I get from running the ***<mark>ifconfig</mark>*** on my Linux container.

Now, we can launch a different service onto this created MAC network.

```plaintext
docker run -d --name macnginx --network macnetwork nginx
```

On inspecting the network and container we find that:

macnetwork-

![Screenshot 2022-04-07 at 7.01.13 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649295083003/gHXOhzPs4.png?auto=compress,format&format=webp align="left")

macnginx -

![Screenshot 2022-04-07 at 7.04.15 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649295261603/5hq500FZT.png?auto=compress,format&format=webp align="left")

The basic difference between MACVLAN and IPVLAN is that <mark>MACVLAN</mark> assigns a <mark>different MAC address</mark> to each attached docker container and <mark>IPVLAN</mark> assigns the <mark>same MAC address</mark> to all containers attached to it.

## 🌟 Overlay Network

An overlay network is used in the case of a <mark>Docker Swarm</mark> Cluster.

It is several nodes connected together to create a cluster to manage the number of containers running onto them. So, there needs to be some kind of network connection between all nodes.

An overlay network is utilized for creating an <mark>internal private</mark> network to the Docker nodes in the Docker Swarm cluster.

This will be a common network that will be present on all nodes in the Swarm cluster.

## 🌟 Conclusion

I believe that this article will help to understand the basics of Docker Networking and it might become easy for the readers to improve their Docker infrastructures with this understanding. Docker is a very deep topic and having an understanding of Docker Networking right in the beginning will make the learning curve relatively less steep when one moves to advanced topics.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#docker #docker container #docker network #DevOps #TrainWithShubham

#90daysofdevopsc #happylearning

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)