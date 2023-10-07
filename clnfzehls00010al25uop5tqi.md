---
title: "Running Node app using Helm Chart 👨‍💻"
datePublished: Sat Oct 07 2023 11:58:14 GMT+0000 (Coordinated Universal Time)
cuid: clnfzehls00010al25uop5tqi
slug: running-node-app-using-helm-chart
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696674339924/1c2c55a4-6fb8-47ee-b5a7-172723f88de5.png
tags: aws, kubernetes, helm, 90daysofdevops, trainwithshubham

---

# **🌟 Introduction:**

In this blog post, we will walk you through the process of deploying a Docker image from Docker Hub using Helm. Helm is a powerful package manager for Kubernetes that allows you to define, install, and upgrade even the most complex Kubernetes applications.

Helm is a valuable tool in the DevOps toolbox, streamlining Kubernetes deployments and making it easier to manage your complex applications in a containerized environment. 🚢📦

# 🌟 Why Helm?

Helm solves several challenges in the Kubernetes deployment process:

1. **Package Management**: Helm allows you to package your application, including all its dependencies and configurations, into a single unit called a "chart." This simplifies the distribution and installation of complex applications.
    
2. **Version Control**: Helm charts can be versioned and stored in a chart repository, making it easy to manage different versions of your application and rollback to previous versions if needed.
    
3. **Templating**: Helm uses Go templates to generate Kubernetes manifest files dynamically, enabling you to customize deployments for different environments (e.g., development, production) without duplicating code.
    
4. **Upgrade and Rollback**: Helm simplifies the process of upgrading and rolling back applications, ensuring smooth updates and minimizing downtime.
    
5. **Collaboration**: Teams can collaborate more effectively by sharing and reusing Helm charts, reducing the risk of configuration errors.
    

**Real-World Example:** Imagine you are managing a microservices-based application with multiple services that need to be deployed and scaled independently. Helm allows you to create charts for each service, define their dependencies, and manage their deployments as a cohesive application. When you need to update a service or roll back to a previous version due to issues, Helm simplifies the process, making your DevOps tasks more efficient and error-free.

# 🌟 **Prerequisites:**

## 📍 Make sure you have the following prerequisites:

* Kubernetes cluster: You should have a Kubernetes cluster up and running. I am using Kubeadm with one control plane and one data plane.
    
* Helm: Helm should be installed on your local machine/ virtual machine/ ec2-instances.
    
    Use these commands to install helm in k8s cluster.
    
    ```plaintext
        curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
        sudo apt-get install apt-transport-https --yes
        echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
        sudo apt-get update
        sudo apt-get install helm
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696671214230/6d8949f0-f2f3-4666-b9f9-752084543c35.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696671219397/eb574bc2-b54a-4455-8f74-262a08056c31.png align="center")
    
* Docker: You need Docker installed on your local machine/ virtual machine/ ec2 instance for building and pushing Docker images.
    
    ```plaintext
    kubectl get no # no is for nodes
    kubectl get all
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696671250471/d1c49556-f0ad-4791-8549-15140f833853.png align="center")
    

### 📌 **Step 1: Create a Helm Chart**

First, we need to create a Helm chart to define the deployment of our application. Open your terminal and run the following command to create a Helm chart named "app-node":

```plaintext
helm create app-node
sudo apt-get install tree -y
tree app-node
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696671316484/8ee9b36d-a79d-4379-a003-f69545d0b52f.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696671410817/b492b3a5-9c24-4915-976e-cc1437625d10.png align="center")

This command generates a directory structure for your Helm chart with default templates and values.

**<mark>Chart.yaml</mark>**

Contains the metadata of the helm

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696671496280/c0d9c5c3-059c-49d6-ad94-86b6ac2de7ae.png align="center")

### 📌 **Step 2: Edit values.yaml**

Navigate to the **<mark>"app-node"</mark>** directory and open the **<mark>"values.yaml"</mark>** file in your preferred text editor. Update the file to match the specifications you provided in your question: such as replicaCount, repository, service, autoscaling,etc.

```plaintext
replicaCount: 2

image:
  repository: trainwithshubham/node-app-test-new
  pullPolicy: Always 
  # Overrides the image tag whose default is the chart appVersion.
  tag: "latest"

imagePullSecrets: []
nameOverride: ""
fullnameOverride: ""

serviceAccount:
  # Specifies whether a service account should be created
  create: true
  # Annotations to add to the service account
  annotations: {}
  # The name of the service account to use.
  # If not set and create is true, a name is generated using the fullname template
  name: ""

podAnnotations: {}

podSecurityContext: {}
  # fsGroup: 2000

securityContext: {}
  # capabilities:
  #   drop:
  #   - ALL
  # readOnlyRootFilesystem: true
  # runAsNonRoot: true
  # runAsUser: 1000

service:
  type: NodePort
  port: 8000
  targetPort: 8000
  nodePort: 30010

ingress:
  enabled: false
  className: ""
  annotations: {}
    # kubernetes.io/ingress.class: nginx
    # kubernetes.io/tls-acme: "true"
  hosts:
    - host: chart-example.local
      paths:
        - path: /
          pathType: ImplementationSpecific
  tls: []
  #  - secretName: chart-example-tls
  #    hosts:
  #      - chart-example.local

resources: {}
  # We usually recommend not to specify default resources and to leave this as a conscious
  # choice for the user. This also increases chances charts run on environments with little
  # resources, such as Minikube. If you do want to specify resources, uncomment the following
  # lines, adjust them as necessary, and remove the curly braces after 'resources:'.
  # limits:
  #   cpu: 100m
  #   memory: 128Mi
  # requests:
  #   cpu: 100m
  #   memory: 128Mi

autoscaling:
  enabled: false
  minReplicas: 1
  maxReplicas: 4
  targetCPUUtilizationPercentage: 50
  # targetMemoryUtilizationPercentage: 80

nodeSelector: {}

tolerations: []

affinity: {}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693224370334/dafbc4dd-ddb0-4416-8529-8aa7e1a0d76f.png?auto=compress,format&format=webp align="left")

This configuration specifies the number of replicas, Docker image details, and service specifications for your application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696671639301/3c2046ba-5401-45f9-a040-21d5418c4235.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696671655108/eb432f5c-f363-4fa5-91fe-fd892578cd02.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696671666945/bad8186c-3c08-4e43-96e6-10f5a7371af9.png align="center")

### 📌 **Step 3: Deploy the Helm Chart**

Now that our Helm chart is configured, we can deploy our application to the Kubernetes cluster.

This command deploys the **<mark>"app-node"</mark>** Helm chart to your Kubernetes cluster. Helm will create all the necessary Kubernetes resources based on the configuration in your chart.

```plaintext
Install a helm chart using install command
$ helm install <FIRST_ARGUMENT_RELEASE_NAME> <SECOND_ARGUMENT_CHART_NAME>
helm install note-app ./app-node
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696671762843/2d4147b6-3343-4d93-a0e0-eb4df044bf99.png align="left")

### 📌 **Step 4: Verify the Deployment**

To verify that your application has been deployed successfully, you can run the following command to list all the deployments in your cluster:

```plaintext
helm list -a
kubectl get deployments
or
kubectl get all
```

You should see the "app-node" deployment listed with the desired number of replicas.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696671899944/8501e6a6-2740-426a-9e10-1a2efbb37bcb.png align="left")

### 📌 **Step 5: Access Your Application**

To access your application, you can use the NodePort service you defined in the **<mark>"values.yaml"</mark>** file. Find the NodePort assigned to your service:

```plaintext
kubectl get svc 
kubectl get po
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696671983223/62c785e9-a682-4402-98c1-5443a7b6edc5.png align="left")

Locate the "node-app" service and note the port under "PORT(S)". You can now access your application using your Kubernetes cluster's IP address and the NodePort.

### 📌 **Application Output**

You have successfully deployed a Docker image from Docker Hub using Helm. Helm makes it easy to define and manage complex Kubernetes deployments, making it an essential tool for DevOps engineers working with Kubernetes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696672027884/252b2f52-7cde-4d19-8e48-5ccd942c8dcc.png align="left")

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.😊

#aws #cloudcomputing #docker #Devops #TrainWithShubham #90daysofdevopsc #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)