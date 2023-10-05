---
title: "Episode 4 : 2 Tier Application Deployment using  Kubernetes🔥"
datePublished: Thu Oct 05 2023 12:28:26 GMT+0000 (Coordinated Universal Time)
cuid: clnd5lm0e000409ifg57xaqg4
slug: episode-4-2-tier-application-deployment-using-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696505802034/67977a9f-c74a-4a46-84b0-f9e15ac510fc.png
tags: aws, kubernetes, 90daysofdevops, trainwithshubham, 2tier-architecture

---

# **Introduction 🌞:**

Kubernetes has emerged as the standard for container orchestration, it allows developers to efficiently manage and scale their applications. In this blog, we will walk you through the process of deploying a 2-tier Flask application using Kubernetes. This setup will consist of a frontend/backend and Database tier, each running in separate containers within a Kubernetes cluster and how these containers communicate. At the end of this guide, you will have a scalable and auto-healing feature architecture for your Flask app.

# 🚀Setup Kubernetes cluster:

* I have already set up a Kubernetes Cluster with master and worker nodes.
    
* If you want to know how to create kubeadm cluster, follow the below link.
    

[K8S-Setup-Guide](https://dushyantkumark.hashnode.dev/episode-3-setup-k8s-kubeadm-cluster)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696497056343/a152c0d4-1acd-4039-bb61-6f5768dfa367.png align="left")

# 🚀Docker Images:

* I have already pushed the Docker images into the Docker hub, I will use these images to deploy the application. If you want to know how to create, build and push the image to the docker hub, then follow the link "[K8S-Setup-Guide](https://dushyantkumark.hashnode.dev/episode-3-setup-k8s-kubeadm-cluster)".
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695972185970/403c0dd0-ae7a-47c0-8cf6-10bac7df295f.png?auto=compress,format&format=webp align="left")

# 🚀**Deploying Your Application:**

* Clone your repository code from Git Hub.
    

```plaintext
git clone https://github.com/dushyantkumark/two-tier-flask-app.git
cd two-tier-flask-app
mkdir mysqldata
mkdir k8s
cd k8s
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696499257403/1f2c247a-0f20-4d30-8a2a-552fb70de452.png align="center")

* Create a persistent volume manifest (mysql-pv.yml).
    

```plaintext
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv
spec:
  capacity:
    storage: 256Mi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  hostPath:
    path: /home/ubuntu/two-tier-flask-app/mysqldata        #This is your host path where your data will be stored. Make sure to create mysqldata directory in mentioned path
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696501018455/0e9be476-0a23-474c-871b-a7e1fe59b8de.png align="center")

* Create a persistent volume claim manifest (mysql-pvc.yml).
    

```plaintext
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 256Mi
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696501039374/2d479953-a618-4bcb-99f7-1ef70a89ecaf.png align="center")

* Create a mysql deployment manifest (mysql-deployment.yml).
    

```plaintext
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
  labels:
    app: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
        - name: mysql
          image: mysql:latest
          env:
            - name: MYSQL_ROOT_PASSWORD
              value: "myadmin"
            - name: MYSQL_DATABASE
              value: "myDb"
            - name: MYSQL_USER
              value: "admin"
            - name: MYSQL_PASSWORD
              value: "myadmin"
          ports:
            - containerPort: 3306
          volumeMounts:
            - name: mysqldata
              mountPath: /var/lib/mysql   # this is your container path from where your data will be stored
      volumes:
        - name: mysqldata
          persistentVolumeClaim:
            claimName: mysql-pvc    # PVC claim name
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696501057301/f428e3d9-90bf-4f06-a3e8-a00434f7730d.png align="center")

* Creating a Cluster-IP Service for my Database:
    

```plaintext
apiVersion: v1
kind: Service
metadata:
  name: mysql
spec:
  selector:
    app: mysql
  ports:
    - port: 3306
      targetPort: 3306
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696501071337/eb70feb1-19c2-464e-aeaf-77aba0428edc.png align="center")

* Create Kubernetes resources which are written in the YAML manifest.
    

```plaintext
kubectl apply -f mysql-pv.yml
kubectl apply -f mysql-pvc.yml
kubectl apply -f mysql-deployment.yml
kubectl get po   #check status of pods, youcan use (po or pods)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696501198250/b7c85dc0-c9f0-47cf-bcd0-9d080b316643.png align="center")

* Creating a Deployment File for Web app:
    

```plaintext
apiVersion: apps/v1
kind: Deployment
metadata:
  name: two-tier-app
  labels:
    app: two-tier-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: two-tier-app
  template:
    metadata:
      labels:
        app: two-tier-app
    spec:
      containers:
        - name: two-tier-app
          image: dushyantkumark/2-tier-flask-app:latest
          env:
            - name: MYSQL_HOST
              value: "mysql"
            - name: MYSQL_PASSWORD
              value: "myadmin"
            - name: MYSQL_USER
              value: "root"
            - name: MYSQL_DB
              value: "myDb"
          ports:
            - containerPort: 5000
          imagePullPolicy: Always
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696501730288/0e15e627-0545-4d83-b1a9-2cf23bcb94f5.png align="center")

* Create a Nodeport Service to expose it to the external world:
    

```plaintext
apiVersion: v1
kind: Service
metadata:
  name: two-tier-app-service
spec:
  selector:
    app: two-tier-app
  ports:
    - protocol: TCP
      port: 80  # Internal Node port, container port traffic will be directed to this port 
      targetPort: 5000 # Matches the containerPort of the Flask app
      nodePort: 30005 # Node external port, we access our web app on this port
  type: NodePort
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696501823245/44e98c42-7b6a-4326-a77d-91e702fb97b6.png align="center")

* Create or Update Kubernetes resources which are written in the YAML manifest.
    

```plaintext
kubectl apply -f two-tier-deployment-app.yml
kubectl apply -f two-tier-service-app.yml
kubectl get po
```

* Add a 30005 port to the worker node security group, to access our web app.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696502448045/54dfe19c-a60e-4ff1-bb98-12af02e64f79.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696502643185/330fb585-8cba-4be9-8d7d-ac4ea7fc81d4.png align="center")

```plaintext
kubectl get po
kubectl get svc
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696502734838/80ae3053-ea6c-4ed8-a690-3d57aef3f615.png align="center")

> ***<mark>Note: FOR connection between Application and Database I am copying mysql CLUSTER-IP and pasting it into MYSQL_HOST (two-tier-deployment-app.yml)</mark>***

* open your web application deployment file.
    

```plaintext
vim two-tier-deployment-app.yml
NOTE (add cluster ip of mysql service)
- name: MYSQL_HOST
  value: "10.102.243.87" 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696503143702/01530b37-b368-43c5-b698-774e763c2d05.png align="center")

* Update Kubernetes resources which is deployment.
    

```plaintext
kubectl apply -f two-tier-deployment-app.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696503392014/8610583a-efbc-4a32-aab3-69a21c39e904.png align="center")

* Data base connected successfully but the table "myDb.messages" is not present
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696503412833/2c5e3450-160f-4678-b1b7-e56f542361a1.png align="center")

* Create the Message table in your MySQL Database but before creating a table access the MySql Database and then enter in the mysql with the following commands.
    

```plaintext
sudo docker exec -it <container-id> bash
sudo mysql -u root -p
enter password:
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696503734772/a0ba5d75-be39-48ea-b1d8-c605aaae859c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696503706695/b5f94d3c-602c-49bb-9d8d-ce37233585cb.png align="center")

* Check the Databases, use myDb and then create a table with the help of the following commands. use the syntax directly copy and paste it to your terminal.
    

```plaintext
show databases;
use myDb;

CREATE TABLE messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    message TEXT
);
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696503822307/a669e361-9f83-47f9-9198-2f952dc5e125.png align="center")

* After Creating the table access your 2-Tier Flask Deployment App on your browser: with the help of the following syntax:
    

```plaintext
http://<ec2-instance-public-ip>:30005
http://13.235.16.156:30005
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696503994545/4e13626d-1f97-438e-b843-ad113cc8ebe9.png align="center")

* Add some messages and submit them for testing purposes.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696504047247/d3f6f860-0dfe-4198-b9d0-6359503093ab.png align="center")

* Verify that data in the databases.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696504093846/483437a4-83dc-44cd-8bcb-e87707c56b39.png align="center")

* Let's consider if traffic increases, then you auto-scale your pods.
    

```plaintext
kubectl get deployment
kubectl scale deployment two-tier-app --replicas=4 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696504274401/789871c2-8b12-4244-9ed1-b4afd50a883d.png align="center")

* Let's consider if your pod is deleted, then your pod auto-heals itself.
    

For example, I move into the worker node and delete one pode for testing the feature of auto-healing.

```plaintext
# Worker Node [ Data Plane ]
sudo docker ps 
sudo docker kill <container-id>
# master node [ Control Plane ]
kubectl get po
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696504788545/81de9469-5a23-43fb-90b8-a9a1fff60f8d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696504809856/021180a9-1c69-4bc6-9277-02c144271952.png align="center")

* Kubernetes will attempt to list resources of multiple types that are common and supported in your cluster. The specific resource types included may vary depending on your cluster's configuration and installed resources, but it typically includes common types like **<mark>pods, services, deployments, and replicasets</mark>**.
    

```plaintext
kubectl get all
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696504949591/19def069-ebec-40db-88e5-567a26cdd5e1.png align="left")

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)

**<mark>GitHub</mark>**: [**https://github.com/dushyantkumark/two-tier-flask-app.git**](https://github.com/dushyantkumark/two-tier-flask-app.git)