---
title: "Kubernetes Project — Deploy a Flask and MongoDB Microservices"
datePublished: Thu May 04 2023 19:25:59 GMT+0000 (Coordinated Universal Time)
cuid: clh9ipeq9000309kx72uw8cn8
slug: kubernetes-project-deploy-a-flask-and-mongodb-microservices
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683227644626/81fa6c54-f27a-4311-9259-088b0da05a38.png

---

## **Introduction:-**

Kubernetes is a powerful container orchestration tool that enables developers to deploy, manage, and scale containerized applications. While Kubernetes is designed to be easy to use, it's not without its challenges, and troubleshooting is a critical skill that all Kubernetes users must possess. In this blog, we'll explore some common Kubernetes troubleshooting techniques that you can use to diagnose and fix issues with your Kubernetes clusters.

### **Prerequisites for deployment-**

1. **Update the system and install docker:**
    

```yaml
sudo apt update -y
sudo apt install docker.io -y

sudo systemctl start docker
sudo systemctl enable docker
```

1. **Kubeadm installation:**
    

```yaml
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg

echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update -y
sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
```

1. **To connect with the cluster(for the master node):**
    

```yaml
sudo su
kubeadm init

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml

kubeadm token create --print-join-command
```

1. **To connect with the cluster(for the Worker node):**
    

```yaml
sudo su
kubeadm reset pre-flight checks
(*Paste the Join command on worker node and append `--v=5` at end*)
(*kubeadm token create --print-join-command*)
```

1. **To verify cluster connection:-**
    

```yaml
kubectl get nodes
```

### **<mark>Let's dive into our deployment------&gt;</mark>**

**Clone the repo:-**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683213823331/c53e74e8-9dbd-4d75-8473-57021d30faf7.png align="center")

1. **1\. Create the docker file**
    
    ```yaml
     vim Dockerfile
    ```
    
    1. 1. **Configuration of the docker file**
            

```yaml
    FROM python:alpine3.7
    COPY . /app
    WORKDIR /app
    RUN pip install -r requirements.txt
    ENV PORT 5000
    EXPOSE 5000
    ENTRYPOINT [ "python" ]
    CMD [ "app.py" ]
```

1. **3\. Now we will make a new deployment file of taskmaster.yml**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682744529063/e689a002-02b9-4796-b228-cc3d143e8ed0.png?auto=compress,format&format=webp align="left")
    
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: taskmaster
      labels:
        app: taskmaster
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: taskmaster
      template:
        metadata:
          labels:
            app: taskmaster
        spec:
          containers:
            - name: taskmaster
              image: gauriyadav1504/gauri-micro:latest
              ports:
                - containerPort: 5000
              imagePullPolicy: Always
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682744705019/1a8d9630-cde3-4361-bbc6-d38f9e3ee20d.png?auto=compress,format&format=webp align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682744821381/2a7a4780-0115-4d13-994f-ab843627e93c.png?auto=compress,format&format=webp align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682744876763/bb3e4fa7-6ece-415e-9299-e4957da41d9f.png?auto=compress,format&format=webp align="left")
    
    1. 1. Make new taskmaster service file known as taskmaster-svc.yml
            
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682744955353/7a8c7d32-d8aa-4b25-8b7f-4a44d70cbd7d.png?auto=compress,format&format=webp align="left")
    
    ```yaml
    kind: Service
    metadata:
      name: taskmaster-svc
    spec:
      selector:
        app: taskmaster
      ports:
        - port: 80
          targetPort: 5000
          nodePort: 30007
      type: NodePort
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682745172245/6b59c2ab-80be-47c0-be6d-fe98ce3e128d.png?auto=compress,format&format=webp align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682745849644/5829fb21-3667-4440-894c-3cda4d645682.png?auto=compress,format&format=webp align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682745883971/f033dab1-75d4-4f6e-b4c9-246adef6c08e.png?auto=compress,format&format=webp align="left")
    
    1. 1. Make Mongo persistent volume file, that is mongo-pv.yml
            
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682745987222/0830b8fc-43c8-4dea-a057-f94494bb658e.png?auto=compress,format&format=webp align="left")
    
    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: mongo-pv
    spec:
      capacity:
        storage: 256Mi
      accessModes:
        - ReadWriteOnce
      hostPath:
        path: /tmp/db
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682746034865/c4bd6a22-de72-46e7-9bb5-4c1d3d21939d.png?auto=compress,format&format=webp align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682746082336/1818092d-cdb1-43c3-9342-72ef10f38433.png?auto=compress,format&format=webp align="left")
    
    1. 1. Make a file to claim persistent volume, that is mongo-pv.yml
            
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682746144196/87f85519-fb46-4c72-a744-3089ae10a402.png?auto=compress,format&format=webp align="left")
    
    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: mongo-pv
    spec:
      capacity:
        storage: 256Mi
      accessModes:
        - ReadWriteOnce
      hostPath:
        path: /tmp/db
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682746186253/c9b39cea-ac8b-4136-974f-4f89215d2da8.png?auto=compress,format&format=webp align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682746211781/868e8db4-3b18-47a3-b517-8d167eb9038f.png?auto=compress,format&format=webp align="left")
    
    1. 1. Make a mongo file vim mongo.yml
            
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682746273254/46fc67c2-3727-49f6-8702-a2c36d4e6c51.png?auto=compress,format&format=webp align="left")
    
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: mongo
      labels:
          app: mongo
    spec:
      selector:
        matchLabels:
          app: mongo
      template:
        metadata:
          labels:
            app: mongo
        spec:
          containers:
            - name: mongo
              image: mongo
              ports:
                - containerPort: 27017
              volumeMounts:
                - name: storage
                  mountPath: /data/db
          volumes:
            - name: storage
              persistentVolumeClaim:
                claimName: mongo-pvc
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682746318713/91b9ba59-c1bf-4b4e-b206-b0b25e828424.png?auto=compress,format&format=webp align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682746349076/c5323c9d-244d-4f32-914f-fd7c08b492ea.png?auto=compress,format&format=webp align="left")
    
    1. 1. make service for mongo file vim mongo-svc.yml
            
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682746469563/100867f0-d759-458b-b21a-f21461bf4d8f.png?auto=compress,format&format=webp align="left")
    
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        app: mongo
      name: mongo
    spec:
      ports:
        - port: 27017
          targetPort: 27017
      selector:
        app: mongo
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682746493010/05de98af-39ff-466c-8087-bd9b5938f60b.png?auto=compress,format&format=webp align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682746522750/16b0fed2-b0d8-43f2-9f78-549fd86829bb.png?auto=compress,format&format=webp align="left")
    

***Thank you for reading!!***  
\\...................................................................................................................................................

**~Dushyant Kumar**

The above information is up to my understanding. Suggestions are always welcome.

#Kubernetes #DevOps #90daysofdevops #KubeWeek

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn: </mark> [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog:</mark>[**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)