---
title: "Kubernetes Project — Deployed a Reddit Clone Apllication"
datePublished: Mon May 08 2023 13:38:01 GMT+0000 (Coordinated Universal Time)
cuid: clhew1b9s000709l3fntp2hwn
slug: kubernetes-project-deployed-a-reddit-clone-apllication
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683545978427/39be4574-3bd6-4226-b116-19ff91e0b69a.png
tags: aws, github, projects, kubernetes, devops

---

This is the simple architecture we are going to follow for our deployment:

## **Points:**

1. Github: version control of your code
    
2. CI Server: one t2.micro
    
3. DockerHub: Create a repository
    
4. Deployment Server: two t2.medium
    

> In this blog post, we will go through the steps of setting up a Kubernetes cluster for a Reddit clone application using Kubernetes, Docker, AWS EC2, and Dockerhub. We set up a Kubeadm cluster & also provide a list of Kubernetes commands used in this application.

## **Basic Terminologies Used:**

\-**<mark>Kubernetes</mark>**: Kubernetes is an open-source container orchestration system for automating software deployment, scaling, and management.

\-**<mark>Docker</mark>**: Docker is a set of platform-as-a-service products that use OS-level virtualization to deliver software in packages called containers.

\-**<mark>Pod</mark>:** A pod is the smallest execution unit in Kubernetes. A pod encapsulates one or more applications. Pods are ephemeral by nature, if a pod (or the node it executes on) fails, Kubernetes can automatically create a new replica of that pod to continue operations.

<mark>-</mark>**<mark>etcd</mark>:** etcd is a distributed key-value store that is used by Kubernetes as its primary data store for storing configuration data, state information, and metadata about the cluster. etcd provides a reliable, highly available, and consistent way to store and manage this data, making it a critical component of Kubernetes

\-**<mark>Replication Controller</mark>**: A ReplicationController is similar to a process supervisor, but instead of supervising individual processes on a single node, the ReplicationController supervises multiple pods across multiple nodes. ReplicationController is often abbreviated to "RC" in discussion and as a shortcut in Kubectl commands.

\-**<mark>API-Server</mark>**: The Kubernetes API server validates and configures data for the API objects which include pods, services, replication controllers, and others.

\-**<mark>Scheduler</mark>**<mark>:</mark> The Kubernetes scheduler is a control plane process that assigns Pods to Node

**\-<mark>Namespaces</mark>:** Namespaces are **a way to organize clusters into virtual sub-clusters** — they can be helpful when different teams or projects share a Kubernetes cluster.

**<mark>Prerequisites</mark>**: To follow this tutorial, you will need the following tools and accounts:

* AWS account
    
* Git account
    

A basic understanding of Docker and Kubernetes

## **\-Step 1:** Launching EC2 instances

Firstly, we need to launch two EC2 instances - one for the Kubernetes master node and another for the worker node. We will be using the t2.medium instance type for both. After launching the instances, we need to configure the security groups for allowing SSH access and Kubernetes communication between the nodes.

## \-**Step 2: Installing Kubeadm**

Following are the steps which are going to apply on both the Master and Worker Servers.

\- **<mark>Step 2.1</mark>**<mark>: Apply below given the command to both the Master and Worker Server</mark>

```yaml
sudo apt update -y
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt update -y
sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
sudo usermod -aG docker $USER
sudo reboot
```

* **Note: Wait for the Server to reboot then proceed with the command given on the next step.**
    

\-**<mark>Step 2.2</mark>**<mark>: Apply the Below Given Command to Master Node Only</mark>

```yaml
sudo su
kubeadm init
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
kubeadm token create --print-join-command
```

\-**<mark>Step 2.3</mark>**<mark>: Apply Below Given Command to Worker Node</mark>

```yaml
sudo su
kubeadm reset pre-flight checks
Paste the Join command on worker node and append --v=5 at end
```

* **Note: Before Running above Paste Command Check your Security group of EC2 Instance(Master Node) is port 6443 open.**
    

\-**<mark>Step 2.4</mark>**<mark>: Check Worker Node is Connected to Master</mark>

```yaml
kubectl get nodes
```

## \-Step 3: Deployment Process

<mark>-Step 3.1: Create a new Namespace for our Reddit-Clone App</mark>

```yaml
kubectl create namespace reddit
```

<mark>-Step 3.2: Creating Deployment File For Reddit-Clone App</mark>

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: reddit-clone-deployment
  namespace: reddit
  labels:
    app: reddit-clone
spec:
  replicas: 3
  selector:
    matchLabels:
      app: reddit-clone
  template:
    metadata:
      labels:
        app: reddit-clone
    spec:
      containers:
      - name: reddit-clone
        image: dushyantkumark/reddit-clone-k8s-ingress
        ports:
        - containerPort: 3000
```

Let's break down the different parts of this file:

> * `apiVersion`: This specifies the API version being used. In this case, we're using the `apps/v1` API version, which is used for creating Deployments.
>     
>     * `kind`: This specifies the kind of Kubernetes object we're creating. In this case, we're creating a Deployment.
>         
>     * `metadata`: This section contains metadata about the Deployment, such as its name.
>         
>     * `spec`: This section contains the desired state of the Deployment.
>         
>         * `replicas`: This specifies the desired number of replicas. In this case, we want 2 replicas.
>             
>         * `selector`: This specifies the label selector used to identify the ReplicaSet managed by the Deployment.
>             
>         * `template`: This specifies the template used to create new pods when scaling up or replacing existing pods.
>             
>             * `metadata`: This section contains metadata about the pod.
>                 
>                 * `labels`: This specifies the labels used to identify the pod.
>                     
>             * `spec`: This section contains the desired state of the pod.
>                 
>                 * `containers`: This specifies the containers to run in the pod.
>                     
>                     * `name`: This specifies the name of the container.
>                         
>                     * `image`: This specifies the container image to use. Here I pulled the image from my docker [**hub.To**](http://hub.To) know more about how to push/pull an image from the docker hub refer to these links:
>                         
>                         [**docker push | Docker Documentation**](https://docs.docker.com/engine/reference/commandline/push/)
>                         
>                         [**docker pull | Docker Documentation**](https://docs.docker.com/engine/reference/commandline/pull/)
>                         
>                     * `ports`: This specifies the ports to expose in the container.
>                         
>                         * `containerPort`: This specifies the port number to expose your application.
>                             

Overall, the deployment.yml file is used to define the desired state of a Deployment, including the desired number of replicas, the label selector used to identify the ReplicaSet, and the pod template used to create new pods.

**<mark>After Creating the deployment.yml file</mark>**

```yaml
kubectl apply -f deployment.yml
```

You can check on your master node as well as on the worker node whether Reddit-clone containers are running.

You can check nodes, pods, namespaces

Commands and images are shown below--&gt;

```yaml
kubectl get nodes  #default
kubectl get nods -n=reddit  #specified namespace
```

```yaml
kubectl get pods -n=reddit
```

```yaml
kubectl get ns  #ns represtents namespace
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683548323628/92711876-31a9-4231-9bc0-08b2b7dd8566.png align="center")

**\-<mark>Step 3.3: Creating Service File For Reddit-Clone App</mark>**

```yaml
apiVersion: v1
# Indicates this as a service
kind: Service
metadata:
  # Service name
  name: reddit-clone-service
  namespace: reddit
spec:
  type: NodePort  
  selector:
    # Selector for Pods
    app: reddit-clone
  ports:
    # Port Map
  - protocol: TCP 
    port: 3000
    targetPort: 3000
    nodePort: 30009
```

Let's break down the different parts of this file:

> * `apiVersion`: This specifies the API version being used. In this case, we're using the `v1` API version, which is used for creating Services.
>     
> * `kind`: This specifies the kind of Kubernetes object we're creating. In this case, we're creating a Service.
>     
> * `metadata`: This section contains metadata about the Service, such as its name.
>     
> * `spec`: This section contains the desired state of the Service.
>     
>     * **type**: `the type` field in the Service YAML file specifies the type of Service to create. The `type` field is required in the `spec` section of the Service YAML file, and it can have one of the following values:
>         
>         1. <mark>ClusterIP</mark>: This is the default type of Service and it exposes the Service on a cluster-internal IP address. The Service is only accessible within the cluster and cannot be accessed from outside the cluster.
>             
>         2. <mark>NodePort</mark>: This type of Service exposes the Service on a specific port on each node in the cluster. This allows external traffic to access the Service using the node's IP address and the specified port.
>             
>         3. <mark>LoadBalancer</mark>: This type of Service creates a load balancer in the cloud infrastructure, which distributes traffic to the Service across multiple nodes in the cluster. This type of Service is useful when you need to expose a Service to the internet or an external network.
>             
>         4. <mark>ExternalName:</mark> This type of Service maps a Service to a DNS name, allowing you to reference the Service by its DNS name rather than an IP address or port number.
>             
> 
> In addition to the `type` field, the Service YAML file can also include other fields such as `selector`, `ports`, and `metadata`. The `selector` field specifies which pods the Service should target, the `ports` field specifies the ports to expose on the Service and the `metadata` field specifies metadata about the Service such as its name, labels, and annotations.
> 
> * `selector`: This specifies the label selector used to identify the set of pods to be exposed by the Service. In this case, we're selecting all pods with the label `app: Reddit-clone`.
>     
>     * `ports`: This specifies the ports to expose on the Service.
>         
>         * `name`: This specifies a name for the port. This is optional but can be useful for readability.
>             
>         * `port`: This specifies the port number on the Service.
>             
>         * `targetPort`: This specifies the port number on the pods to forward traffic to. In this case, we're forwarding traffic to port 3000 on the pods.
>             
>         * nodePort: We've added the `type: NodePort` parameter to the `spec` section of the Service. This tells Kubernetes to create a NodePort Service. The Service will be assigned a random port number in the range of 30000-32767 on each node in the cluster.
>             
>             With this configuration, external traffic can access the Service by connecting to any node's IP address on the assigned NodePort.We've Selected nodePort 30009
>             

You can check the service

Commands and images are shown below--&gt;

```yaml
kubectl get svc -n=reddit
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683550394784/14ad072a-e996-4bc7-aa0c-1358759a95c8.png align="center")

**\-<mark>Step 3.4: Set Inbound traffic rules for communication</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683550138417/824208e2-3f05-49d7-8118-361f494284c2.png align="center")

**\-<mark>Step 3.5: Check your site is running copy your public IP address of the worker node</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683549927415/4e9ff92e-d019-443e-8b0e-ca8ea0be5e75.png align="center")

## <mark>Conclusion:</mark>

Deploying a Reddit clone application through Kubernetes provides a scalable, flexible, and resilient solution that can handle a growing user base and traffic demands. By using Kubernetes to manage containerized workloads, you can easily scale up or down your application based on demand, while ensuring high availability and fault tolerance. Additionally, Kubernetes provides a wide range of features and tools that enable you to automate your deployment and management workflows, streamline your development processes, and increase the efficiency and reliability of your infrastructure. Overall, deploying a Reddit clone through Kubernetes is a great way to leverage the power of containerization and orchestration to build and deploy modern, cloud-native applications.

<mark>From git clone to docker push image process link below:</mark>

[github---&gt;dockerhub](https://dushyantkumark.hashnode.dev/how-to-push-docker-image-to-dockerhub-reddit-clone-apllication)

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#Kubernetes #reddit #DevOps #90daysofdevops #aws #project

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn: </mark> [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog:</mark>[**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)