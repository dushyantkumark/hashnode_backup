---
title: "#KubeWeek Day5 
Kubernetes Storage & Security"
datePublished: Sat Apr 29 2023 09:51:23 GMT+0000 (Coordinated Universal Time)
cuid: clh1sz6zm000b09mnbnohe0em
slug: kubeweek-day5-kubernetes-storage-security
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682711592411/ff34f1bf-9986-4001-bada-3007cd38db85.jpeg

---

## **Kubernetes Storage**

Kubernetes is a popular open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. One critical aspect of running containerized applications is storage. In Kubernetes, storage is managed through a series of abstractions that allow developers to define the type of storage their application needs without worrying about the underlying infrastructure.

Here are some of the main storage abstractions in Kubernetes:

1. Volumes: A volume is an abstraction that allows you to store data in a way that is decoupled from the container's lifecycle. A volume can be backed by various storage systems such as local disk, network storage, or cloud storage.
    
2. Persistent Volumes (PVs): A Persistent Volume is a piece of storage that is provisioned by an administrator and is available for use by the cluster. PVs can be backed by different storage systems like local disk, network storage, or cloud storage.
    
3. Persistent Volume Claims (PVCs): A Persistent Volume Claim is a request for storage by a user. When a user creates a PVC, Kubernetes finds an available PV and binds the PVC to the PV.
    
4. Storage Classes: A Storage Class is a way for administrators to define different types of storage that are available for use in the cluster. Each Storage Class is associated with a particular type of storage, and it specifies the provisioner to use for that type of storage.
    

In summary, Kubernetes provides various storage abstractions that allow developers to define the type of storage their application needs without worrying about the underlying infrastructure. These abstractions make it easy to manage storage in a containerized environment, and they allow applications to scale seamlessly as the storage needs grow.

### **Kubernetes Storage with example**

Sure! Let's walk through an example of how storage can be provisioned and used in a Kubernetes environment.

Let's say we have a web application that requires persistent storage to store user data. We want to use a cloud-based storage solution, so we decide to use Amazon Elastic Block Store (EBS) as our storage backend.

First, we need to create a Persistent Volume (PV) that will represent the EBS volume we want to use. We can create a PV in Kubernetes by defining a YAML file like this:

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: ebs-pv
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  awsElasticBlockStore:
    volumeID: <EBS_VOLUME_ID>
    fsType: ext4
```

In this YAML file, we are defining a PV called `ebs-pv` that has a capacity of 5Gi and can be accessed in ReadWriteOnce mode. We are also specifying that this PV should be backed by an EBS volume with the ID `<EBS_VOLUME_ID>`, and that the filesystem type should be `ext4`.

Next, we need to create a Persistent Volume Claim (PVC) that will represent the storage request from our web application. We can create a PVC in Kubernetes by defining a YAML file like this:

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: ebs-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```

In this YAML file, we are defining a PVC called `ebs-pvc` that requests 5Gi of storage and can be accessed in ReadWriteOnce mode.

Finally, we can use the PVC in our web application's deployment by adding a `volumes` section to the deployment YAML file, like this:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
        - name: web-app-container
          image: web-app-image
          volumeMounts:
            - name: my-storage
              mountPath: /data
      volumes:
        - name: my-storage
          persistentVolumeClaim:
            claimName: ebs-pvc
```

In this YAML file, we are defining a deployment called `web-app` that uses the PVC `ebs-pvc` as a volume mount at the path `/data`. This means that any data written to `/data` in the container will be stored in the EBS volume associated with the PVC.

That's a basic example of how storage can be provisioned and used in a Kubernetes environment using Amazon EBS as the backend storage solution. Of course, there are many other storage solutions and configurations that can be used, but this should give you a good idea of the overall process.

## **Kubernetes Security**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682761203798/b3452fce-371b-4178-87ab-959b8e6220ae.jpeg align="left")

Security is a critical aspect of any production deployment. Kubernetes provides several security mechanisms that can help secure your cluster and the applications running in it. In this section, we will discuss some of the key Kubernetes security features.

### **RBAC (Role-Based Access Control)**

Role-Based Access Control (RBAC) is a Kubernetes feature that enables administrators to define granular access control policies for users, groups, and service accounts. RBAC is used to control who can perform specific actions on Kubernetes resources, such as creating or deleting pods, services, or nodes. RBAC policies can be defined using Roles, ClusterRoles, RoleBindings, and ClusterRoleBindings.

\--&gt; Creating an RBAC Policy

To create an RBAC policy in Kubernetes, we need to define a YAML file with the necessary details, such as the policy name, the type of resource being controlled, and the roles and subjects involved. Here's an example of a YAML file that creates an RBAC policy:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

In this example, we create an RBAC policy named "pod-reader" in the "default" namespace. The policy allows users to perform "get", "watch", and "list" actions on "pods" resources.

### **Pod Security Policies**

Pod Security Policies (PSPs) are a Kubernetes feature that allows administrators to control the security characteristics of pods running on the cluster. PSPs enable administrators to enforce security policies on pods, such as limiting the use of privileged containers or enforcing specific Linux capabilities. PSPs can be defined using YAML files and can be applied to specific namespaces or to the entire cluster.

\--&gt; Creating a Pod Security Policy

To create a Pod Security Policy in Kubernetes, we need to define a YAML file with the necessary details, such as the allowed security contexts, volumes, and privileged access. Here's an example of a YAML file that creates a Pod Security Policy:

```yaml
apiVersion: policy/v1beta1
kind: PodSecurityPolicy
metadata:
  name: restricted
spec:
  privileged: false
  seLinux:
    rule: RunAsAny
  runAsUser:
    rule: MustRunAsNonRoot
  fsGroup:
    rule: MustRunAs
    ranges:
    - min: 1
      max: 65535
  volumes:
  - secret
  - configMap
```

In this example, we create a Pod Security Policy named "restricted". The policy disallows privileged access, requires that the pod run as a non-root user, and allows access to specific volumes, such as secrets and config maps.

### **Secrets**

Secrets are Kubernetes objects used to store sensitive information, such as passwords, API keys, or TLS certificates. Secrets are stored in an encrypted format, and only authorized users and pods can access them. Secrets can be used by applications running in Kubernetes to retrieve sensitive information securely.

\--&gt; Creating a Secret

To create a Secret in Kubernetes, we need to define a YAML file with the necessary details, such as the type of secret and the data to be stored. Here's an example of a YAML file that creates a Secret:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: xxxxxxxxxxx
  password: xxxxxxxxxxx
```

In this example, we create a Secret named "my-secret" with a type of "Opaque," which means that the secret is an arbitrary byte array. We store two pieces of data: a username and a password. The data is encoded in base64 format to ensure that it is stored securely. But this is not the best encryption technique, for the best encryption for your secrets you move to the next level <mark>HASHICORP VAULT</mark>.

### **Network Policies**

Network Policies are a Kubernetes feature that allows administrators to enforce security policies on the network level, such as allowing or denying traffic to specific pods based on their labels or network ports. Network Policies can be defined using YAML files and can be applied to specific namespaces or to the entire cluster.

\--&gt; Creating a Network Policy

To create a Network Policy in Kubernetes, we need to define a YAML file with the necessary details, such as the policy name, the pod selector, and the allowed ingress and egress rules. Here's an example of a YAML file that creates a Network Policy:

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: my-networkpolicy
spec:
  podSelector:
    matchLabels:
      app: myapp
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: mydatabase
    ports:
    - protocol: TCP
      port: 5432
```

In this example, we create a Network Policy named "my-networkpolicy". The policy applies to pods with the label "app: myapp". The policy allows ingress traffic from pods with the label "app: mydatabase" on port 5432 using TCP protocol.

### **TLS (Transport Layer Security)**

Transport Layer Security (TLS) is a cryptographic protocol used to secure communication between applications running on the cluster. Kubernetes supports TLS for secure communication between the API server, kubelet, and etcd. TLS certificates can be issued by a certificate authority (CA) or self-signed. Kubernetes supports certificate rotation to ensure the security of the cluster.

\---&gt; Creating a TLS Certificate

To create a TLS certificate in Kubernetes, we need to define a YAML file with the necessary details, such as the common name and the validity period. Here's an example of a YAML file that creates a TLS certificate.

```yaml
apiVersion: cert-manager.io/v1alpha2
kind: Certificate
metadata:
  name: my-tls
spec:
  commonName: mytls.example.com
  dnsNames:
    - mytls.example.com
  secretName: mytls-secret
  issuerRef:
    name: myissuer
    kind: ClusterIssuer
  duration: 365d
```

In this example, we create a TLS certificate named "my-tls". The certificate has a common name of "[**mytls.example.com**](http://mytls.example.com)" and a validity period of 365 days. The certificate is issued by a ClusterIssuer named "myissuer". The TLS certificate is stored in a Kubernetes Secret named "mytls-secret".

## Conclusion

Kubernetes provides a robust and scalable platform for deploying and managing containerized applications. Its storage system and security features play a crucial role in ensuring the reliability and security of applications running on the cluster. Persistent Volumes, Persistent Volume Claims, Storage Classes, and StatefulSets enable developers to manage and scale storage requirements for stateful applications, while RBAC, Pod Security Policies, Secrets, Network Policies, and TLS provide granular control over access, authentication, and encryption. By leveraging these features, organizations can build and run secure and highly available applications on Kubernetes with confidence.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#Kubernetes #DevOps #90daysofdevops #KubeWeek

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn: </mark> [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog:</mark>[**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)