---
title: "How to push docker image to DOCKERHUB — Reddit Clone Apllication"
datePublished: Wed May 17 2023 12:33:03 GMT+0000 (Coordinated Universal Time)
cuid: clhroofyh000a09mcaq3v371e
slug: how-to-push-docker-image-to-dockerhub-reddit-clone-apllication
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684323400584/0f79ab40-5f15-4843-9df3-46ca84656cf2.png
tags: docker, github, docker-images, 90daysofdevops, trainwithshubham

---

## \&gt;Setup CI server:

After launching the EC2 instance of type **t2.micro** which will be primarily used for coder management and packaging we have to install **Docker** and clone the code from the git repository to the CI server.

### **(Docker Installation)**

Before moving forward we'll be installing docker by the command:

```plaintext
sudo apt-get update -y; sudo apt install docker.io -y
```

### **(Giving permission to Docker)**

After the docker installation, to access docker commands we have to give user permission to the Docker using the below command.

```plaintext
sudo usermod -aG docker $USER 
```

### (Cloning the code from Git)

After Docker installation, we need the project code in our local machine to proceed further with image creation. To do so we have to clone the code from the GitHub repository, command given below:

```plaintext
git clone https://github.com/dushyantkumark/reddit-clone-k8s-ingress.git
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684324290001/bcdb219e-78d4-43cd-8cea-5a811b699238.png align="center")

Now above you can see we have got our project directory named **reddit-clone-k8s-ingress**.

do ls that shows the list and subdirectories of reddit-clone-k8s-ingress.

## **\&gt;Containerizing the application with Docker**

After getting the code in our Local machine we have to create the docker image of the code which will further be deployed.

### Writing the Docker file for containerization

```plaintext
FROM node:19-alpine3.15

WORKDIR /reddit-clone

COPY . /reddit-clone

RUN npm install

EXPOSE 3000

CMD ["npm","run","dev"]
```

This Dockerfile creates a Docker image for a Reddit clone application using Node.js version 19 on Alpine Linux version 3.15.

The `FROM` instruction specifies the base image for the Docker image, which in this case is the `node:19-alpine3.15` image.

The `WORKDIR` instruction sets the working directory for any subsequent instructions in the Dockerfile to `/reddit-clone`.

The `COPY` instruction copies the contents of the current directory (.) to the `/reddit-clone` directory in the Docker image.

The `RUN` instruction runs the `npm install` command to install the required dependencies for the Reddit clone application.

The `EXPOSE` instruction exposes port 3000 in the Docker image, which is the port used by the Reddit clone application.

The `CMD` instruction specifies the command to run when the Docker container is started, which in this case is the `npm run dev` command to start the application in development mode.

Overall, this Dockerfile sets up an environment to run a Node.js-based Reddit clone application, installs its dependencies, and starts the application in development mode on port 3000.

### Building the Docker image from the above Dockerfile

After writing the Dockerfile we can build a **Docker image** out of it by using the command docker `build . -t reddit-clone-k8s-ingress` . This command builds a Docker image for the reddit clone application based on the Dockerfile.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684325334608/c39509cf-de0a-4ade-9a6b-d45a6bb8856d.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684325358852/200f79a9-0b7f-4eb0-a041-99b74e9814b1.png align="left")

Now above you can see an image `redit-clone-k8s-ingress` has been created and tagged. Using `docker images` you can see the image that has been created above:

### Logging in to Docker Hub

Docker Hub is nothing but a hub of repositories containing docker Images. Once the image is built from the docker file, we have to push the image to the Docker hub so that during the deployment the image can be fetched from DockerHub itself. It works like GitHub.

So, to push the image we have to log in to our docker hub account from the CLI using the command:

```plaintext
docker login
```

### Tag and Push the image to Docker Hub

Once the login is successful we can tag the image and then push the image to the docker hub by using the commands given below

`docker push username/tagname:latest` is the syntax:

```plaintext
docker tag reddit-clone-k8s-ingress dushyantkumark/reddit-clone-k8s-ingress
docker images
docker push dushyantkumark/reddit-clone-k8s-ingress:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684326149400/38b78140-6570-428e-8f3b-6d9283e1f30b.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684326114138/503510e9-7a6f-4d53-bd21-9ef4a4d6da56.png align="center")

Now from the above images from Docker Hub, you can see the image has been pushed.

## Project Remaining part

<mark>For Kubernetes deployment, you can follow the link below</mark>

[<mark>reddit-app</mark>](https://hashnode.com/edit/clhew1b9s000709l3fntp2hwn)

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#github #dockerhub #reddit #DevOps #90daysofdevops #aws #project #happylearning #trainwithshubham

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn: </mark> [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog:</mark>[**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)