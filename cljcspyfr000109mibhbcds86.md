---
title: "Setup CircleCI environment - [ Project ]"
datePublished: Mon Jun 26 2023 11:49:04 GMT+0000 (Coordinated Universal Time)
cuid: cljcspyfr000109mibhbcds86
slug: setup-circleci-environment-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687780018349/fc8a8570-0c0c-4a0e-bf85-d80519ed1459.png
tags: continuous-integration, devops, circleci, 90daysofdevops, trainwithshubham

---

# **🌟 Introduction**

CI/CD platform that can be used to implement DevOps practices.  
Its mission is to manage change, so software teams can **innovate faster,** That means to be less complex as can be.  
The main Aim of creating CI/CD pipelines is to **<mark>Deliver changes</mark>,** Build new releases; however, with a **<mark>non-cloud</mark>** CI/CD platform you should manage the CI/CD platform **<mark>infrastructure</mark>** itself.  
Therefore, CircleCI helps you to **<mark>focus</mark>** on **<mark>Delivering changes</mark>** and starting to **<mark>build pipelines</mark>** very **fast** *"will see in the PROJECT given in this post"*  
Also, CircleCi Provides a <mark>Free Plan</mark> on its cloud-based solution.

To list **How powerful is CircleCI**

* Build pipelines **<mark>very fast</mark>**, with less **<mark>complexity</mark>**.
    
* Hold and Handel The **<mark>CI/CD</mark>** solution **<mark>infrastructure</mark>**.
    
* Have a free **<mark>plan</mark>** **<mark>pricing</mark>.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685163839444/b9f46f44-5c09-4da9-93a6-16acdee70b4c.png?auto=compress,format&format=webp align="left")

Learn more about [CircleCI\_Benefits](https://dushyantkumark.hashnode.dev/streamline-your-deployment-workflow-circleci)

## **🔹**Environment Setup

**1\. CircleCI signup**  
CircleCI is **<mark>integrated</mark>** with **<mark>GitHub</mark>**, So in this lab environment will signup with my **<mark>GitHub account</mark>**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687425454881/2eeeeace-0ef1-45cb-8e12-c22d7c2e8521.png align="center")

**2\. Create a Project**  
After Signing up, you'll be redirected to the Setup your code **<mark>Project section</mark>** Which has to select the **<mark>organization</mark>**, and all GitHub **<mark>repos</mark>** listed below, to start creating a project **<mark>Press</mark>** on the **<mark>SetUp Project</mark>** button.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687424849004/c9f8b8cd-0d97-41ed-a4e1-cf9cea0929a6.png align="left")

Then, select **<mark>Fastest</mark>** to discover the **<mark>config.yaml</mark>** template file and *config.yaml template* is The pipeline configuration yaml file.

Now, Let's select the **<mark>CircleCi-Python</mark>** sample, This sample provides config.yaml files with minimum configurations, *Just note that if you have already config.yaml file you can press skip this step.*

**Discover** the config.yaml file, then press on **<mark>commit and run</mark>**.  
This will fire the pipeline and first create a directory which is **<mark>.circleci</mark>**, then in that directory creates a **<mark>config.yaml</mark>** file in the GitHub repository

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687426232093/d4c4adeb-9e1f-4fd9-993a-5ec2a19ad8b2.png align="left")

Here's your **<mark>first pipeline</mark>** that has been running with one job called **<mark>build</mark>.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687424610337/10926a83-3e12-436a-afd0-844d7d7465d4.png align="left")

### 🔸 Setup Triggers

Triggers are used to **<mark>auto-trigger</mark>** the pipeline without human intervention.  
All that you do is commit your changes to your repo and the pipeline will fire automatically.

**How it Works**

* Press on Dashboard
    
* Ensure that you're selecting the right project and branch
    
* Then press the Trigger pipeline button, Press the Trigger pipeline again, *on the other screen that appears.*
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687425844336/80e28f7f-764b-49cc-83c8-afc00716ebbb.png align="left")

### 🔸 **Check Triggers**

let's check our whole process  
\- Open your GitHub repo  
\- In the URL section, replace ***<mark>.com</mark>*** with ***<mark>.dev</mark>****,* this will open a code editor.  
*\-* Make any changes in your code, add then commit it.  
*\-* This should fire the **<mark>CircleCi-Python</mark>** pipeline with the new change automatically.

A code sample of changes is shown below in the given image. For code, the GitHub link is present at the end of this blog.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687424260491/fe6b26b4-fae6-400c-b51c-4ce26ef2f5f5.png align="left")

Now, go to the CircleCI platform, select dashboard, and in the pipeline section click on CircleCi-Python Jobs, you get workflow from **<mark>build</mark>**, **<mark>test</mark>** and **<mark>deploy</mark>**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687424354161/295f7e91-c72e-4fc9-99b2-f05f927512de.png align="left")

That's it, Hope this article inspired you and helps you.

# **🌟** Conclusion

In this post, we have explored how to use CircleCI to build\_test\_deploy Python-based projects. We started by understanding the provided code snippet, which demonstrates a basic CircleCI configuration for a Python project. We examined the YAML code, which defines a job named "build" that utilizes a Docker image, installs dependencies, and runs Python code. CircleCI is a powerful and user-friendly platform for automating the build, test, and deployment processes of Python projects. Its integration capabilities, scalability, and extensive feature set make it an essential tool for modern software development teams. By leveraging CircleCI, you can streamline your development workflow, increase productivity, and deliver high-quality software more efficiently.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome.

#CI/CD #automation #CircleCI #continuous integration #TrainWithShubham

#90daysofdevopsc #happylearning

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)

<mark>Github</mark>: [https://github.com/dushyantkumark/CircleCi-Python.git](https://github.com/dushyantkumark/CircleCi-Python.git)