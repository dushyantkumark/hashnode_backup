---
title: "Monitoring using Prometheus, Grafana & Cadvisor."
datePublished: Thu Jan 04 2024 13:25:26 GMT+0000 (Coordinated Universal Time)
cuid: clqz8pfph00010al76l8t8ryi
slug: monitoring-using-prometheus-grafana-cadvisor
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704258613686/39feefd1-b4c2-49f7-9662-be28a3a2aa3d.jpeg
tags: redis, prometheus, grafana, trainwithshubham, cadvisor

---

In this article, we will run a docker container and we will monitor and see the cpu utilization and other metrics in cadvisor, prometheus and grafana dashboard.

## What is cadvisor

(Container Advisor) is an open-source tool developed by Google that provides container-level performance metrics. It is specifically designed to work with containerized environments, such as Docker. `cAdvisor` is used to collect, aggregate, and export information about running containers. This information includes resource usage metrics, performance statistics, and other relevant data.

In the context of Prometheus, `cAdvisor` serves as an exporter. An exporter in the Prometheus ecosystem is a component that collects metrics from a third-party system and makes them available for Prometheus to scrape. In this case, `cAdvisor` collects container metrics and exposes them in a format that Prometheus can understand. Prometheus then scrapes these metrics from the `cAdvisor` service at regular intervals.

## What is Redis

`Redis` is an open-source, in-memory data structure store used as a database, cache, and message broker. It supports various data structures like strings, hashes, lists, sets, and more. `Redis` is known for its speed and flexibility, making it a popular choice for applications that require fast data access and caching. Additionally, it can be used as a message broker in distributed systems.

## What is Prometheus

`Prometheus` is an open-source monitoring and alerting toolkit designed for reliability and scalability of systems. It is primarily used to collect and store time-series data, making it valuable for monitoring and analyzing the performance of various components in a system.

## What is Grafana

`Grafana` is an open-source platform for monitoring and observability. It provides a customizable and interactive dashboard for visualizing data from different sources, including Prometheus. Grafana is widely used to create visually appealing graphs, charts, and alerts, making it easier for users to understand and analyze their system's performance.

### Steps-

1. make a ec2 instance of t2.medium, create and allocate elastic ip to ec2.
    
2. Install docker and docker compose on ec2 instance.
    
3. make a directory prometheus.
    
4. install prometheus via document -wget command (check readme file [https://github.com/dushyantkumark/prometheus-grafana-cadvisor-tutorial/blob/main/README.md](https://github.com/dushyantkumark/prometheus-grafana-cadvisor-tutorial/blob/main/README.md))
    
5. make a compose file -- see the compose file in this repo- [https://github.com/dushyantkumark/prometheus-grafana-cadvisor-tutorial/blob/main/README.md](https://github.com/dushyantkumark/prometheus-grafana-cadvisor-tutorial/blob/main/README.md)
    
6. create new container tetris-game, monitor this container.
    

<mark>this Docker Compose file helps you set up a monitoring environment using Prometheus and cAdvisor to collect and visualize container metrics. Redis is an in-memory data structure store often used as a database, cache, and message broker.</mark>

## Launch Instance & EIasticIP

**Click on the Launch instance option on the right side**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704259921496/7e688363-592a-449e-8f4c-6cc07a4b0327.png align="center")

**Now click on the Connect Button when your instance is up and running Condition.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704260151567/73e87483-f7b1-4d57-a7b8-e5ae6bde59ba.png align="center")

Create new eip that is static in nature.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704260212295/135f7b26-8112-4136-a0c8-d4eb2c511c13.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704260351976/21259e45-1127-4467-9cc4-c202a47d9730.png align="center")

New eip attached to ec2 instance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704260328293/0e0d502e-2603-4391-8cfc-f859447b62a8.png align="center")

## Install & Configure Tools

First ssh your ec2-instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704267173157/00615b9d-b991-4872-8d4a-9e71f80dac14.png align="center")

Second make new directory `prometheus`, move into that directory and then install `prometheus`, `docker compose`. Create <mark>docker-compose.yaml</mark> file which contain container creation services.

```plaintext
pwd
mkdir prometheus
cd prometheus
pwd
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704267591769/9daeb272-33fe-4d08-ae42-f1cb46c05494.png align="center")

Updating your ec2 instance.

```plaintext
sudo apt update
```

Install prometheus

Install docker.

```plaintext
sudo apt-get install docker.io -y
sudo chown $USER /var/run/docker.socket
docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704267821382/0aec36e3-2201-4df2-a9b3-fdcb8fd24c95.png align="center")

Install docker-compose.

```plaintext
sudo apt install docker-compose -y
```

download prometheus.yaml configuration file, using below command in prometheus directory.

```plaintext
wget https://raw.githubusercontent.com/prometheus/prometheus/main/documentation/examples/prometheus.yml
```

Create new yaml file called docker-compose.yaml in prometheus directory, docker compose file is used to define and run multi-container Docker applications.

This file is used to define and run multi-container Docker applications. In your case, it specifies three services: `prometheus`, `cadvisor`, and `redis`. Let me break down the configuration:

```yaml
version: '3.2'
services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    ports:
    - 9090:9090
    command:
    - --config.file=/etc/prometheus/prometheus.yml
    volumes:
    - ./prometheus.yml:/etc/prometheus/prometheus.yml:ro
    depends_on:
    - cadvisor
  cadvisor:
    image: gcr.io/cadvisor/cadvisor:latest
    container_name: cadvisor
    ports:
    - 8080:8080
    volumes:
    - /:/rootfs:ro
    - /var/run:/var/run:rw
    - /sys:/sys:ro
    - /var/lib/docker/:/var/lib/docker:ro
    depends_on:
    - redis
  redis:
    image: redis:latest
    container_name: redis
    ports:
    - 6379:6379
```

Here's a breakdown of the key components:

1. **Services:**
    
    * `prometheus`: Runs the Prometheus monitoring tool. It exposes its web interface on port 9090 and depends on the `cadvisor` service. It uses a volume to mount the `prometheus.yml` configuration file.
        
    * `cadvisor`: Runs Google's cAdvisor, collecting container resource usage. It exposes its web interface on port 8080 and depends on the `redis` service.
        
    * `redis`: Runs the Redis database server, exposing its default port 6379.
        
2. **Images:**
    
    * `prom/prometheus:latest`: The latest version of the Prometheus image.
        
    * [`gcr.io/cadvisor/cadvisor:latest`](https://github.com/krishkprawat/grafana-prometheus-cadvisor-Tutorial/blob/main/README.md): The latest version of the cAdvisor image.
        
    * `redis:latest`: The latest version of the Redis image.
        
3. **Container Names:**
    
    * Each service has a specified container name (`prometheus`, `cadvisor`, `redis`).
        
4. **Ports:**
    
    * Port mappings are defined for each service (`9090:9090` for Prometheus, `8080:8080` for cAdvisor, `6379:6379` for Redis).
        
5. **Volume Mounts:**
    
    * Prometheus uses a volume to mount the `prometheus.yml` configuration file.
        
6. **Dependencies:**
    
    * `prometheus` depends on `cadvisor`.
        
    * `cadvisor` depends on `redis`.
        

now its time to run multiple containers using single command, this will create 3 containers - cadvisor, prometheus and redis.

```plaintext
docker-compose up -d
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704268147647/2499fb80-4920-4afd-86a9-57934f4e08a8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704268455235/3f5dfc9e-f9d7-4715-b5ab-3a81adc8f89e.png align="center")

check active running containers using command.

```plaintext
docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704268507187/6a99628d-5107-46b8-9e46-886f8c5a5151.png align="center")

### cAdvisor, Prometheus Dashboard

This is the output of cAdvisor, before getting this dashboard open some ports in security group.

cAdvisor - 8080

prometheus - 9090

cAdvisor gui dashboard.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704269605271/40f20108-78e9-46ad-a1be-685be292dc65.png align="center")

Prometheus gui dashboard.

go to prometheus &gt; status&gt; target-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704269667821/c127f7b9-f17e-4b2c-886e-1bdbad269aa4.png align="center")

There is only one target "prometheus" at all right now , to add new target &lt;&gt; here, add the new job in prometheus.yml for docker containers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704269625665/38900cef-d8f3-49a9-95dc-f74f599077f1.png align="center")

### Adding new target for docker in prometheus

Now open prometheus.yaml file in prometheus directory and add new job\_name with static\_configs.

```plaintext
vim prometheus.yaml
- job_name: "docker"
  static_configs:
     - targets:
         - cadvisior:8080
```

restart the docker container and see the prometheus gui now, automatically a target &lt;&gt;(docker) will be added there.

```plaintext
docker restart <container_name/container_id>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704270359590/5f96e6dc-1bc4-4806-849d-02a043bf69d2.png align="center")

cAdvisor gui dashboard.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704270571151/cfa34c3f-038c-4ff8-a6da-50c58e4ef249.png align="center")

prometheus gui dashboard with new target "docker".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704270605350/ef282869-da7f-4130-9410-cb8fe25ffb01.png align="center")

Now check docker metrics in prometheus.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704270679251/a105253b-f7eb-4719-b085-35290e06d106.png align="center")

Now test tje promQL

goto graph and hit the promQL -

```plaintext
rate(container_cpu_usage_seconds_total{name="redis"}[1m])
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704270832245/7cd2bbbf-ccf2-41a4-a9ec-1ca1a008b2d6.png align="left")

## See the metrics of new docker container - tetris-game

### run the docker container directly in terminal

```plaintext
docker run -d -p 80:80 --name tetris-game dushyantkumark/tetris-v2:latest
docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704271099028/29b1ece5-4512-4647-bfee-d653c4e7ab40.png align="center")

go to cadvisor gui and this new tetris-game container should show there also.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704271205302/f798b506-f43e-4c67-9c65-e2bc6b738deb.png align="center")

goto prometheus, and hit the promQL -

```plaintext
rate(container_cpu_usage_seconds_total{name="todo-app"}[1m]) 6
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704271317739/e4280f39-cb6b-461d-b8ff-619b3f6dcee6.png align="center")

goto browser and access your gaming application.

```plaintext
<instance_public_IP:80>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704271442163/75901b69-6317-4a86-995d-51780fa0b5fb.png align="left")

## Setup Grafana Dashboard

Follow below commands to install and configure grafana-server.

change directory cd /home/ubuntu

```plaintext
sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key
#Stable release
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

```plaintext
# Update the list of available packages
sudo apt-get update

# Install the latest OSS release:
sudo apt-get install grafana -y

# Start grafana server
sudo systemctl start grafana-server

# Enable grafana server
sudo systemctl enable grafana-server

# Check status of grafana-serber
sudo systemctl status grafana-server
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704272307906/6a2d86b2-00fe-401e-8776-d2d87cc7eaeb.png align="center")

Add port number 3000 in security group.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704272369923/52da788a-7155-40b5-bc78-d531ab830ee1.png align="center")

go to home -&gt; connection -&gt; data source -&gt; prometheus : check prometheus connectivity.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704272460508/23f4097c-fdc7-498d-b1f9-2eae146b7be2.png align="center")

to see the docker dashboard - goto prometheus dashboard - search docker - copy the ID. (10619)

got to prometheus -&gt; dashbaord -&gt; add new -&gt; paste the ID (10619) and select the prometheus server and hit enter. thts all now you will see the docker metrics in dashboard.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704272827279/147f58ef-12ee-4550-bc14-cc4633f45acc.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704272785089/bfd88663-1968-437f-b957-78c128eb2d31.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704272790200/d11440c9-28d7-4a9d-905a-efd95209acfa.png align="left")

## Setup Node Exporter

It serves as an agent that runs on the machine to be monitored, capturing information about the host's hardware and operating system metrics. These metrics can include details about CPU usage, memory usage, disk utilization, network statistics, and other essential system-level information.

Update docker-compose.yaml in prometheus directory, docker compose file is used to define and run multi-container Docker applications, this time is for "`node-exporter`".

```plaintext
version: '3.2'
services:
  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    restart: unless-stopped
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.rootfs=/rootfs'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)'
    expose:
      - 9100
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    ports:
    - 9090:9090
    command:
    - --config.file=/etc/prometheus/prometheus.yml
    volumes:
    - ./prometheus.yml:/etc/prometheus/prometheus.yml:ro
    depends_on:
    - cadvisor
  cadvisor:
    image: gcr.io/cadvisor/cadvisor:latest
    container_name: cadvisor
    ports:
    - 8080:8080
    volumes:
    - /:/rootfs:ro
    - /var/run:/var/run:rw
    - /sys:/sys:ro
    - /var/lib/docker/:/var/lib/docker:ro
    depends_on:
    - redis
  redis:
    image: redis:latest
    container_name: redis
    ports:
    - 6379:6379
```

There is only two target "prometheus" and "docker" at all right now , to add new target &lt;&gt; here, add the new job in prometheus.yml for docker containers.

Now open prometheus.yaml file in prometheus directory and add new job\_name with static\_configs.

```plaintext
vim prometheus.yaml
- job_name: "node-exporter"
  static_configs:
     - targets:
         - node-exporter:9100
```

Run following command:

```plaintext
docker-compose up -d
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704273729871/6b49b2c4-7afe-4041-b098-2f3ba389d086.png align="center")

go to cadvisor gui and this new node-exporter container should show there also.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704273936854/b82e55e6-7790-4e5b-991a-64f5bf93e2d6.png align="center")

prometheus gui dashboard with new target "node-exporter".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704273991392/f960fcd3-0980-473b-aed3-e87a0a3cf57b.png align="center")

* got to prometheus -&gt; dashbaord -&gt; add new -&gt; paste the `ID (10619)` and select the prometheus server and hit enter. thats all now you will see the docker metrics in dashboard.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704274120159/fb3c0c5f-ad85-41e7-9b56-c469243759be.png align="center")

* got to prometheus -&gt; dashbaord -&gt; add new -&gt; paste the `ID (1860)` for node-exporter.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704274267181/7c95d3fc-3ad3-4c70-afec-a452a51d760e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704274247762/1d5221c1-40e0-4468-8fd5-6a4f17d95e6d.png align="center")

Import dashboard to check how Prometheus query used for collecting metrics and then try in your environment with making some changes accordingly.

Thank you so much for taking the time to read till the end! Hope you found this blog informative.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.

#docker #aws #cloudcomputing #Devops #grafana #cadvisor #prometheus #redis #TrainWithShubham #90daysofdevopsc #happylearning

**<mark>Follow for many such contents:</mark>**

**<mark>LinkedIn</mark>**: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Blog</mark>**: [**dushyantkumark.hashnode.dev**](http://linkedin.com/in/dushyant-kumar-dk)

**<mark>Github</mark>**: [https://github.com/dushyantkumark/prometheus-grafana-cadvisor-tutorial.git](https://github.com/dushyantkumark/prometheus-grafana-cadvisor-tutorial.git)