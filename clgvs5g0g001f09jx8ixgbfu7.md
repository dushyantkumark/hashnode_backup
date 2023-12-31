---
title: "#KubeWeek Day 1
 Kubernetes : Understanding Architecture, 
Components, Installation and Configuration"
datePublished: Tue Apr 25 2023 04:41:38 GMT+0000 (Coordinated Universal Time)
cuid: clgvs5g0g001f09jx8ixgbfu7
slug: kubeweek-day-1-kubernetes-understanding-architecture-components-installation-and-configuration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682946467787/4757f964-0339-4ef6-9cd5-b92624a7f9d4.webp

---

Kubernetes is an open-source platform that automates the deployment, scaling, and management of containerized applications. It helps manage and orchestrate containerized applications across multiple hosts, making it easier to deploy and manage applications at scale. In this blog post, we will take a deep dive into the architecture, components of Kubernetes and walk through the installation process of Kubeadm on both the master and worker nodes, and set up a Kubernetes cluster.

# **Kubernetes Architecture**

Kubernetes architecture is a distributed system that consists of a master node and multiple worker nodes. The master node manages the overall state of the cluster and the worker nodes run the containerized applications. The system uses a set of APIs to communicate between nodes and manage resources, such as storage and networking. The architecture is designed to be scalable, fault-tolerant, and extensible to support a wide range of applications and workloads.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682351448301/fd0441a2-ebb2-42b0-acdb-fd27f23ff5e2.png?auto=compress,format&format=webp align="left")

The Kubernetes architecture consists of the following components:

1. **Master Components:** The master components are responsible for managing the overall Kubernetes cluster.
    
    a. **Kubernetes API Server**: The API server is the central control plane of the Kubernetes cluster. It provides a RESTful interface for communication with other components of the cluster.
    
    b. **etcd**: etcd is a distributed key-value store that is used to store the configuration data and the state of the Kubernetes cluster.
    
    c. **Kube-Controller Manager**: The controller manager is responsible for managing the various controllers that are responsible for maintaining the desired state of the cluster.
    
    d. **Kube-Scheduler**: The scheduler is responsible for scheduling the containerized workloads to the worker nodes.
    
2. **Node Components**: The node components are responsible for running the containerized workloads.
    
    a. **Kubelet**: The kubelet is responsible for managing the containerized workloads on a node. It communicates with the API server to receive instructions on how to manage the containers.
    
    b. **Container Runtime**: The container runtime is responsible for running the containers on a node. It could be Docker, rkt, or any other container runtime that supports the Kubernetes Container Runtime Interface (CRI).
    
    c. **kube-proxy**: The kube-proxy is responsible for managing the network connectivity of the containers running on a node.
    
    # **Kubernetes Components**
    
    When you deploy Kubernetes, you get a cluster.
    
    A Kubernetes cluster consists of a set of worker machines, called [**nodes**](https://kubernetes.io/docs/concepts/architecture/nodes/), that run containerized applications. Every cluster has at least one worker node.
    
    The worker node(s) host the [**Pods**](https://kubernetes.io/docs/concepts/workloads/pods/) that are the components of the application workload. The [**control plane**](https://kubernetes.io/docs/reference/glossary/?all=true#term-control-plane) manages the worker nodes and the Pods in the cluster. In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault tolerance and high availability.
    
    **The components can be divided into two categories: Control Plane and Worker Nodes**
    
    ### Control Plane :
    
    **1\. kube-apiserver**
    
    Provides an API that serves as the front end of a Kubernetes control plane. It is responsible for handling external and internal requests—determining whether a request is valid and then processing it. The API can be accessed via the kubectl command-line interface or other tools like kubeadm, and via REST calls.
    
    **2\. kube-scheduler**
    
    This component is responsible for scheduling pods on specific nodes according to automated workflows and user-defined conditions, which can include resource requests, concerns like affinity and taints or tolerations, priority, persistent volumes (PV), and more.
    
    **3\. kube-controller-manager**
    
    The Kubernetes controller manager is a control loop that monitors and regulates the state of a Kubernetes cluster. It receives information about the current state of the cluster and objects within it and sends instructions to move the cluster toward the cluster operator’s desired state.
    
    The controller manager is responsible for several controllers that handle various automated activities at the cluster or pod level, including replication controller, namespace controller, service accounts controller, deployment, statefulset, and daemonset.
    
    **4\. etc**
    
    A key-value database that contains data about your cluster state and configuration. Etcd is fault-tolerant and distributed.
    
    **5\. cloud-controller-manager**
    
    This component can embed cloud-specific control logic - for example, it can access the cloud provider’s load balancer service. It enables you to connect a Kubernetes cluster with the API of a cloud provider. Additionally, it helps decouple the Kubernetes cluster from components that interact with a cloud platform, so that elements inside the cluster do not need to be aware of the implementation specifics of each cloud provider.
    
    ### Worker Node :
    
    **6\. Nodes**
    
    Nodes are physical or virtual machines that can run pods as part of a Kubernetes cluster. A cluster can scale up to 5000 nodes. To scale a cluster’s capacity, you can add more nodes.
    
    **7\. Pods**
    
    A pod serves as a single application instance and is considered the smallest unit in the object model of Kubernetes. Each pod consists of one or more tightly coupled containers, and configurations that govern how containers should run. To run stateful applications, you can connect pods to persistent storage, using Kubernetes Persistent Volumes—[**learn more in the following section.**](https://spot.io/resources/kubernetes-architecture/11-core-components-explained/#kubernetes-persistent-volumes)
    
    **8\. Container Runtime Engine**
    
    Each node comes with a container runtime engine, which is responsible for running containers. Docker is a popular container runtime engine, but Kubernetes supports other runtimes that are compliant with Open Container Initiative, including CRI-O and rkt.
    
    **9\. kubelet**
    
    Each node contains a kubelet, which is a small application that can communicate with the Kubernetes control plane. The kubelet is responsible for ensuring that containers specified in pod configuration are running on a specific node, and manages their lifecycle. It executes the actions commanded by your control plane.
    
    **10\. kube-proxy**
    
    All compute nodes contain kube-proxy, a network proxy that facilitates Kubernetes networking services. It handles all network communications outside and inside the cluster, forwarding traffic or replying on the packet filtering layer of the operating system.
    
    **11\. Container Networking**
    
    Container networking enables containers to communicate with hosts or other containers. It is often achieved by using the container networking interface (CNI), which is a joint initiative by Kubernetes, Apache Mesos, Cloud Foundry, Red Hat OpenShift, and others.
    
    ## **Kubernetes Installation & Configuration: Kubeadm**
    
    There are some prerequisites before moving further:
    
    * 2 or more Linux servers running **Ubuntu**
        
    * root privileges
        
    * 4 GB or more of Ram - for better performance, use 6 GB
        
    * 2 CPUs or more
        
    * Full network connectivity between all machines in the cluster (public or private network is fine)
        
    * Unique hostname, MAC address, and product\_uuid for every node.
        
    * Certain ports are open on your machines.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682353259123/0bf7b885-99d6-4ac4-84d2-8281c1f35fd2.png?auto=compress,format&format=webp align="left")
    
    Please find the below steps under which we will see how to install and configure Kubeadm:
    
    \*step 1 to 4 performed in both Kubernetes-Master and Kubernetes-Node/Worker
    
    Step 1: Update Ubuntu
    
    ```plaintext
    sudo apt update
    ```
    
    Step 2: Install Docker
    
    ```plaintext
    sudo apt install docker.io
    ```
    
    Step 3: Start and Enable Docker
    
    ```plaintext
    sudo systemctl enable docker
    ```
    
    ```plaintext
    sudo systemctl start docker
    ```
    
    ```plaintext
    sudo systemctl status docker
    ```
    
    Step 4: Install Kubeadm
    
    ```plaintext
    sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
    
    echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
    
    sudo apt update -y
    sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
    ```
    
    Step 5: Configure the Master Node
    
    ```plaintext
    sudo su
    kubeadm init
    
    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config
    
    kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
    
    kubeadm token create --print-join-command
    ```
    
    The kubeadm init command initializes the master node.
    
    The mkdir command creates a directory for the Kubernetes configuration file. The cp and chown commands copy the configuration file and set the correct permissions. The Kubectl apply command installs Weave Net, which is a popular networking plugin for Kubernetes.
    
    The kubeadm token create command creates a token for joining worker nodes to the cluster.
    
    Step 6: Configure the Worker Node (Run on the worker node)
    
    ```plaintext
    sudo su
    kubeadm reset pre-flight checks
    
    # Paste the Join command on worker node with `--v=5`
    ```
    
    Step 7: Verify the Cluster (Run on the master node)
    
    ```plaintext
    kubectl get nodes
    ```
    
    This command lists all the nodes in the cluster.
    
    If everything is set up correctly, the output should show both the master and worker nodes.
    
    \\...................................................................................................................................................
    
    The above information is up to my understanding. Suggestions are always welcome.
    
    #Kubernetes #Devops #90daysofdevops #Kubeweek #kubeweekchallenge @[Shubham Londhe](@TrainWithShubham) **Sir**
    
    <mark>Follow for many such contents:</mark>
    
    <mark>LinkedIn: </mark> [https://www.linkedin.com/in/dushyant-kumar-dk/](https://www.linkedin.com/in/dushyant-kumar-dk/)
    
    <mark>Blog:</mark>[**https://dushyantkumark.hashnode.dev/**](https://shivanikumari.hashnode.dev/)