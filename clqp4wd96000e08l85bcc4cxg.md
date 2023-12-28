---
title: "Kubernetes commands you
should definitely know!"
datePublished: Thu Dec 28 2023 11:41:09 GMT+0000 (Coordinated Universal Time)
cuid: clqp4wd96000e08l85bcc4cxg
slug: kubernetes-commands-you-should-definitely-know
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703763028833/9343b535-0133-4cfb-bcc5-e6797c490ccf.jpeg
tags: kubernetes, eks, 90daysofdevops, trainwithshubham, kubernetes-cheatsheet

---

# 🎡 kubernetes Commands

Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available. Kubernetes provides you with a framework to run distributed systems resiliently. It takes care of scaling and failover for your application, provides deployment patterns, canary deployments, and more. In this blog post, I will mention Kubernetes commands which we need for most of the use-cases.

### 👨‍💻 Check Kubectl Version

This command checks the version of the installed Kubectl client

```yaml
kubectl version --client
```

### 👨‍💻 Set Context for Cluster in different cloud providers

These commands set the context for the specified cloud-managed Kubernetes clusters, allowing subsequent commands to interact with the chosen cluster.

```yaml
# Connect to EKS
aws eks --region <your-region> update-kubeconfig --name <your-cluster-name>
#Connect to AKS
az aks get-credentials --resource-group <your-resource-group> --name <your-aks-cluster-name>
#Connect to GKE
gcloud container clusters get-credentials <your-gke-cluster-name> --region <your-region>
```

### 👨‍💻 kubeconfig file

The kubeconfig file is a crucial part of managing Kubernetes configurations, stored at ***<mark>~/.kube/config</mark>*** by default. It defines clusters, users, and contexts.

This command displays the name of the current Kubernetes context, which represents the cluster that kubectl commands will interact with.

\# Check the current Kubernetes context

```yaml
kubectl config current-context
```

### 👨‍💻 𝗠𝗮𝗻𝗶𝗳𝗲𝘀𝘁 𝗙𝗶𝗹𝗲 - 𝗖𝗿𝗲𝗮𝘁𝗶𝗼𝗻, 𝗗𝗲𝗹𝗲𝘁𝗶𝗼𝗻, 𝗮𝗻𝗱 𝗘𝗱𝗶𝘁𝗶𝗻𝗴 𝗖𝗼𝗺𝗺𝗮𝗻𝗱𝘀

Kubernetes manifest file is a short YAML or JSON document that defines how a specific cluster resource should be configured and managed. It declares the desired state, allowing Kubernetes to maintain that state in the cluster.

Deployment is a ***<mark>blueprint</mark>*** for running and managing application instances, ensuring the specified number of pods are running. It also manages aspects like the container image, configurations, and enables seamless updates, scalability, and self-healing.

\# Create a Deployment using Manifest file

```yaml
kubectl apply -f deployment.yaml
```

\# Delete an object using Manifest file

```yaml
kubectl delete -f deployment.yaml
```

\# Edit a Deployment using Manifest file

```yaml
kubectl apply -f deployment.yaml
```

### 👨‍💻 𝗚𝗘𝗧 𝗖𝗼𝗺𝗺𝗮𝗻𝗱𝘀 (𝗦𝘁𝗮𝘁𝘂𝘀)

These commands retrieve information about different Kubernetes resources, such as pods, services, and deployments.

\# Get commands to check the status

```yaml
kubectl get nodes
kubectl get pods
kubectl get services
kubectl get deployments
```

Get everything in the cluster (statefulset, deployment, pods, nodes, services) in default namespace

```yaml
kubectl get all
kubectl get all -o yaml
kubectl get all -o wide (this command is used to give detailed information)
```

Get everything in the cluster (statefulset, deployment, pods, nodes, services) in particulat namespace (ex: dev)

```yaml
kubectl get namespaces
kubectl get all -n dev
kubectl get all -o wide -n dev (this command is used to give detailed information)
```

These commands show how to retrieve information in different formats for more detailed view with better readability or automation.

```yaml
# Get information in YAML format
kubectl get pods -o yaml
# Get information in JSON format
kubectl get services -o json
```

### 👨‍💻 𝗞𝘂𝗯𝗲𝗰𝘁𝗹 𝗗𝗲𝘀𝗰𝗿𝗶𝗯𝗲

This command provides detailed information about a specific Kubernetes resource, aiding in troubleshooting and understanding its configuration.

\# Describe a resource

```yaml
kubectl describe pod <pod-name>
```

## ❄ 𝗜𝗺𝗽𝗲𝗿𝗮𝘁𝗶𝘃𝗲 𝗖𝗼𝗺𝗺𝗮𝗻𝗱𝘀

Imperative commands allow quick actions without the need for manifest files.

[imperative commands](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/imperative-command/)

### 👨‍💻 𝗞𝘂𝗯𝗲𝗰𝘁𝗹 𝗖𝗿𝗲𝗮𝘁𝗲 𝗖𝗼𝗺𝗺𝗮𝗻𝗱𝘀

These commands demonstrate creating deployments with specific images and replica counts.

\# Create an Nginx Deployment

```yaml
kubectl create deployment nginx-deploy --image=nginx
```

\# Create a Deployment with Redis image and 2 replicas

```yaml
kubectl create deployment redis-deploy --image=redis --replicas=2
```

\# Dry run command will not actually create the Deployment but will generate the YAML configuration file.

```yaml
kubectl create deployment mongod-deploy --image mongo --replicas 3 --dry-run=client -o yaml > mongod.yaml
```

### 👨‍💻 𝗖𝗿𝗲𝗮𝘁𝗲 𝗮 𝗣𝗼𝗱

The kubectl run command creates a pod imperatively, allowing quick pod deployment without the need for a manifest file.

```yaml
# Create a Pod
kubectl run <pod-name> --image=<image-name>
kubectl run nginx-pod --image nginx
```

### 👨‍💻 𝗘𝗱𝗶𝘁 𝗖𝗼𝗺𝗺𝗮𝗻𝗱𝘀

Edit commands are used to modify existing deployments, either imperatively or by scaling the number of replicas.

```yaml
# Edit a Deployment imperatively
kubectl edit "type" "name"
kubectl edit deployment <deployment-name>
```

```yaml
# Scale a Deployment imperatively
kubectl scale deployment <deployment-name> --replicas=3
```

### 👨‍💻 𝗞𝘂𝗯𝗲𝗰𝘁𝗹 𝗥𝗲𝗽𝗹𝗮𝗰𝗲 - 𝗙𝗼𝗿𝗰𝗲

This command forcefully updates an object by replacing it with a new configuration.

```yaml
# Replace and force update an object
kubectl replace --force -f <manifest_file>
```

📌 Certain fields of a resource, like its name or type, cannot be edited using kubectl edit as they are immutable. For such cases, the kubectl replace --force command is used to enforce an update by deleting and recreating the resource with the new configuration.

### 👨‍💻 𝗗𝗲𝗯𝘂𝗴𝗴𝗶𝗻𝗴 𝗖𝗼𝗺𝗺𝗮𝗻𝗱𝘀

These commands demonstrate debugging techniques, including viewing pod logs and executing commands inside a container.

\# Create a Deployment for debugging

```yaml
kubectl create deployment debug-deploy --image=alpine
```

\# View logs of a pod

```yaml
kubectl logs <pod-name>
```

\# Execute a command inside a container

```yaml
kubectl exec -it <pod-name> -- "command"
kubectl exec -it <pod-name> -- /bin/bash
kubectl exec -it <pod-name> -- ls/etc/
```

### 👨‍💻 𝗟𝗼𝗴𝗴𝗶𝗻𝗴 𝗮𝗻𝗱 𝗠𝗼𝗻𝗶𝘁𝗼𝗿𝗶𝗻𝗴 𝗖𝗼𝗺𝗺𝗮𝗻𝗱𝘀

These commands showcase how to view logs of a pod and display resource usage information for pods.

\# View logs of a pod

```yaml
kubectl logs <pod-name>
```

\# Display Resource Usage (CPU and Memory) of Pods

```yaml
kubectl top pods
kubectl top nodes
```

### 📚 𝗸𝘂𝗯𝗲𝗰𝘁𝗹 𝗖𝗵𝗲𝗮𝘁 𝗦𝗵𝗲𝗲𝘁 𝗯𝘆 𝗞𝘂𝗯𝗲𝗿𝗻𝗲𝘁𝗲𝘀

Kubernetes Quick Reference: [https://kubernetes.io/docs/reference/kubectl/quick-reference/](https://kubernetes.io/docs/reference/kubectl/quick-reference/)

Getting Started: [https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-deployment-em-](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-deployment-em-)

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.

#docker #aws #cloudcomputing #Devops #kubernetes #devsecops #TrainWithShubham #90daysofdevopsc #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)