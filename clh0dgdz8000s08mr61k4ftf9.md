---
title: "#KubeWeek Day 4 
Kubernetes Services and Service Discovery"
datePublished: Fri Apr 28 2023 09:49:05 GMT+0000 (Coordinated Universal Time)
cuid: clh0dgdz8000s08mr61k4ftf9
slug: kubeweek-day-4-kubernetes-services-and-service-discovery
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682670849664/1d8bb87c-c923-4d28-acc6-09c96b23d42d.png

---

## **Kubernetes Service**

Kubernetes services are a fundamental building block of distributed applications deployed on Kubernetes clusters. They provide a stable IP address and DNS name for a set of pods in the cluster, allowing other applications within the cluster to communicate with them.

There are several types of Kubernetes services, including:

There are several types of Kubernetes services, including:

* ClusterIP: Exposes the service on a cluster-internal IP address. This is the default service type.
    
* NodePort: Exposes the service on a node-specific port, which can be accessed externally.
    
* LoadBalancer: Exposes the service externally using a cloud provider’s load balancer.
    
* ExternalName: Maps service to a DNS name external to the cluster.
    

[**Refer**](https://hashnode.com/edit/clgxezcfu000g09mh24xf2lpj) to this for a brief about services.

## Kubernetes Service Discovery

Kubernetes provides built-in service discovery, which is the process by which applications in a distributed system can locate and communicate with each other. This is achieved through the use of Kubernetes services.

Kubernetes services provide a stable IP address and DNS name for a set of pods in the cluster. Services can discover other services by their DNS name, allowing for seamless communication between services within a Kubernetes cluster, even as the number of instances of those services changes dynamically.

Kubernetes uses labels and selectors to define sets of pods that a service targets. When a new pod is created or an existing pod is terminated, Kubernetes automatically updates the service’s endpoints to ensure that traffic is always directed to a healthy pod.

There are several ways to access a Kubernetes service from within the cluster, including:

* DNS name: Services are automatically assigned a DNS name, which can be used to access the service from within the cluster.
    
* Environment variables: Kubernetes automatically sets environment variables for each service, which can be used by applications to access the service.
    
* Service discovery libraries: Libraries such as Kubernetes client libraries and service mesh tools like Istio can be used to access and manage services within a Kubernetes cluster.
    

## **Exposing Kubernetes Workloads to the Outside World Using Services**

Services provide a way to expose Kubernetes workloads to the outside world. Let's take a look at how this works.

To expose a workload using a Service, you first need to create a deployment that defines the Pods that will run the workload. Once the deployment is created, you can create a Service that points to the Pods. The Service will provide a stable IP address and DNS name that can be used to access the Pods.

Here is an example of how to create a deployment and a Service for a web application:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: my/myapp:latest
        ports:
        - containerPort: 80

---

apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

In this example, we are creating a deployment that will run three replicas of a web application. We are then creating a Service that points to the Pods created by the deployment. The Service is exposed externally using a LoadBalancer.

Once the Service is created, you can access the web application using the Service's external IP address and port.

## **Service Discovery in Kubernetes**

Service Discovery is the process of discovering Services and Pods within a Kubernetes cluster. Kubernetes provides several mechanisms for Service Discovery, including DNS and environment variables.

### DNS-Based Service Discovery

Kubernetes provides a built-in DNS service that allows you to discover Services and Pods using their DNS names. The DNS service is automatically created when you create a cluster.

The DNS service uses the following naming convention:

```yaml
<service-name>.<namespace>.svc.cluster.local

#Example
myapp.default.svc.cluster.local
```

For example, if you have a Service named `myapp` in the `default` namespace, you can access it using the DNS name `myapp.default.svc.cluster.local`.

If you have multiple replicas of a Pod running a Service, Kubernetes will load balancer the requests between the replicas. DNS-based Service Discovery is a powerful way to discover Services and Pods within a Kubernetes cluster. It allows you to easily access Services and Pods using their DNS names, without having to worry about IP addresses or port numbers.

### Environment Variable-Based Service Discovery

Kubernetes also provides environment variables that allow you to discover Services and Pods from within a container. When a container is created, Kubernetes sets several environment variables that provide information about the container's namespace, hostname, and IP address.

For example, Here is an example YAML file that defines a Service and a Pod in Kubernetes and shows how you can access them using environment variables:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  type: ClusterIP
  selector:
    app: myapp
  ports:
  - name: http
    port: 80
    targetPort: 8080

---
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: nginx
    env:
    - name: MYAPP_SERVICE_HOST
      value: "myapp.default.svc.cluster.local"
    - name: MYAPP_POD_IP
      valueFrom:
        fieldRef:
          fieldPath: status.podIP
```

In this example, we define a Service named myapp with a label selector of `app: myapp`. The Service listens on port 80 and forwards traffic to port 8080 on the Pods that match the label selector.

We also define a Pod named myapp-pod with the same label selector of `app: myapp`. This Pod runs a container based on the nginx image and sets two environment variables: `MYAPP_SERVICE_HOST` and `MYAPP_POD_IP`.

The `MYAPP_SERVICE_HOST` environment variable contains the DNS name of the Service, which Kubernetes automatically sets based on the Service name and namespace. The `MYAPP_POD_IP` environment variable is set using a fieldRef that retrieves the IP address of the Pod from the status field.

By using these environment variables in your application, you can easily access the Service and Pod from within your containers, without having to hardcode IP addresses or DNS names. This provides a flexible and scalable way to build containerized applications in Kubernetes.

Environment variable-based Service Discovery is useful when you need to access Services and Pods from within a container. However, it can be more complex than DNS-based Service Discovery, as you need to handle environment variables and their values within your application code.

### Conclusion

In summary, Kubernetes Services and Service Discovery are powerful tools that can help DevOps teams manage containerized applications at scale. Whether you're exposing your application to the outside world or building complex distributed systems, Kubernetes Services and Service Discovery provide the necessary building blocks to manage your applications effectively in a cloud-native environment.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#Kubernetes #DevOps #90daysofdevops #KubeWeek

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn: </mark> [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog:</mark>[**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)