---
title: "🎮 PLAY Super Mario Game on AWS-EKS"
datePublished: Mon Dec 18 2023 15:46:04 GMT+0000 (Coordinated Universal Time)
cuid: clqb38tau000409l23gpk4q3x
slug: play-super-mario-game-on-aws-eks
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702913851601/86f26a0e-0843-4dac-95c5-c74898fc007a.png
tags: aws, eks, 90daysofdevops, super-mario, trainwithshubham

---

# **🎇 Introduction:**

In this tutorial, we'll embark on an exciting journey of setting up the classic Super Mario game on Kubernetes. Leveraging the power of AWS and Kubernetes, we'll create a Kubernetes cluster using Kubeadm. Get ready for a nostalgic adventure in containers and cloud orchestration!

### **✔ Tools Involved:**

* AWS (Amazon Web Services)
    
* Kubernetes
    

### **✔ GitHub:**

[https://github.com/dushyantkumark/k8s-mario-project.git](https://github.com/dushyantkumark/k8s-mario-project.git)

### **✔ AWS-EKS-CLUSTER-SETUP:**

[https://dushyantkumark.hashnode.dev/set-up-your-eks-cluster-like-a-game](https://dushyantkumark.hashnode.dev/set-up-your-eks-cluster-like-a-game)

# **🎇 Create Manifest files -**

Create a deployment.yml file.

```plaintext
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mario-deployment
  namespace: super-mario  
spec:
  replicas: 2  
  selector:
    matchLabels:
      app: mario
  template:
    metadata:
      labels:
        app: mario
    spec:
      containers:
      - name: mario-container
        image: dushyantkumark/mario-game:latest
        ports:
        - containerPort: 80
```

Create services.yml file.

```plaintext
apiVersion: v1
kind: Service
metadata:
  name: mario-service
  namespace: super-mario
spec:
  type: LoadBalancer
  selector:
    app: mario
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

# 🎇 K8s Commands

Check the number of nodes available.

```plaintext
kubectl get no
or
kubectl get nodes
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702911520987/80c56606-b7b2-4fde-95e4-53f938a8849b.png align="center")

Before applying manifest, first, we have to create a particular namespace.

```plaintext
kubectl create namespace super-mario
or
kubectl create ns super-mario
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702911550204/e777b6fd-a821-4bf1-bc06-925ee5a7704a.png align="center")

Apply Manifest configuration files deployment.yaml and service.yaml files.

```plaintext
kubectl apply -f deployment.yaml 
kubectl apply -f services.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702911594179/52245e77-b28d-4289-9d70-10a689b7168e.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702911604782/931a50f9-9ef0-4af4-9497-748153491fa0.png align="center")

If you want to check all the resources available such as deployment, pods, services, and replicaset in a particular namespace (super-mario).

```plaintext
kubectl get all -n super-mario
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702911769979/ae392ea6-7a67-4400-80b9-dcfba180b442.png align="center")

Now you enjoy your game application :-)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702911933984/72e3b6ed-2823-4b3c-b6d6-fe14a3360ffc.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702911938343/f79b09ab-e9c7-4aa5-afe2-b8234a445c55.png align="center")

NOTE:

Perform the cleanup once you are done with the project.

EKS-Cluster creation command

```plaintext
eksctl create cluster --name mario-cluster --region ap-south-1 --node-type t2.medium --nodes-min 2 --nodes-max 4
```

EKS-Cluster deletion command

```plaintext
eksctl delete cluster --name mario-cluster
```

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.😊

#aws #cloudcomputing #docker #Devops #kubernetes #TrainWithShubham #90daysofdevopsc #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://linkedin.com/in/dushyant-kumar-dk)