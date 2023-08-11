---
title: "Introducing the Power of Identity and Access Management (IAM) 🔑"
datePublished: Tue Jul 04 2023 04:57:29 GMT+0000 (Coordinated Universal Time)
cuid: cljntjh4o000g09l3gdz07l56
slug: introducing-the-power-of-identity-and-access-management-iam
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1688447428394/77cf38c8-3006-41e6-85d9-658b30f4864f.png
tags: aws, iam, aws-certified-solutions-architect-associate, 90daysofdevops, trainwithshubham

---

# **🌟**Introduction

In the world of cloud computing, Identity and Access Management (IAM) plays a vital role in ensuring <mark>data security</mark> and <mark>managing user access</mark>. IAM enables you to define and control <mark>user identities</mark>, <mark>roles</mark>, and <mark>permissions</mark> within your AWS environment. With IAM, you can grant fine-grained access to AWS services, resources, and APIs while maintaining a robust security posture. Mastering IAM empowers you to protect your <mark>sensitive data</mark>, <mark> prevent unauthorized access</mark>, and adhere to <mark>compliance requirements</mark>.

# **🌟Why is the IAM needed?**

Let’s consider an example to understand the IAM role. Consider an organization called <mark>“</mark>[**<mark>CloudTechAI.com</mark>**](http://example.com)<mark>”</mark>, where every employee needs to verify their identity as an employee of the organization by biometrics before entering the premises. This implies that each employee must be authenticated before gaining access to the office.

After entering the office, what will the employees do in the office? In which department they will work? Which computer they will access? This is where <mark>authorization</mark> comes into the picture.

Subsequently, the organization assigns specific permission to each employee, determining what they can access and accomplish, as well as which department they are authorized to work in. This process is known as authorization.

Similarly to the example mentioned above, AWS Cloud utilizes the IAM role to manage <mark>authentication</mark> and <mark>authorization</mark>.

Suppose there is no authentication and authorization process in AWS. In such a scenario, any user could create an account and use any services, they would have root access, granting them the ability to perform virtually any action within the organization’s cloud infrastructure. This could lead to the <mark>unintentional</mark> or <mark>deliberate deletion</mark> of critical services related to the application, resulting in significant losses. To mitigate this risk, AWS offers IAM roles.

IAM effectively addresses the challenge of authentication and authorization, providing a solution to ensure the secure management of user access and privileges within the AWS cloud environment.

# **🌟**What is the IAM?

IAM stands for Identity and Access Management. It is a core service of AWS that enables users to manage <mark>user identities</mark> and <mark>control access</mark> to AWS resources.

It manages the <mark>entire authorization</mark> and <mark>authentication</mark> of the AWS cloud.

## **🔹**What is Authentication?

Authentication is a method of <mark>validating </mark> the identity of a user. Using authentication you will be <mark>only able to view</mark> and get into the AWS but you will <mark>not be able to access and not be able to create any resources</mark> because you don't have the permission.

## **🔹**What is Authorization?

Authorization is the <mark>allowed set of permissions</mark> given to the user. Using <mark>policies</mark>, you can authorize the user.

## **🔹**Identities of IAM

![](https://lh4.googleusercontent.com/V3pStcFiVdshNh69vQmkGhq0UvdD38E5vHAQxo3kwnDknF8IFAvjUAEvAlMVjTUbl_9-qxPprosBRhU1woZpKc4RKjjkfHr3fAKQprgzN_r2MmhGqbzHur1wg3BeJcJ1ykHbI119O4NaZdiDXopNPPQ align="left")

### 🔸 **User**

Users within AWS represent <mark>individual entities</mark> including humans, applications, or services that interact with AWS resources. Each user possesses a <mark>unique identity</mark> and <mark>security credentials</mark>, such as a username and password, for **<mark>authentication</mark>**.

With IAM, <mark>administrators can create</mark> <mark>users</mark>, and assign them <mark>unique credentials</mark>, such as a <mark>username </mark> and <mark>password </mark> or <mark>access keys</mark>, for **<mark>authentication</mark>** and also be used to access AWS resources and services. <mark>Before assigning any policies or permissions, users initially have </mark> **<mark>root access</mark>**.

### 🔸 **Policies**

Policies are <mark>JSON documents</mark> that define the <mark>permissions </mark> and <mark>access rules</mark> for users, and groups. They allow you (<mark>administrators</mark>) to specify the actions that are <mark>allowed or denied</mark> on AWS resources. The JSON file of a policy consists of <mark>statements</mark> that define <mark>one or more permissions</mark> and the resources to which those permissions apply. These policies can be <mark>pre-defined</mark> by AWS and it's known as <mark>AWS-managed policies</mark>, or you can also create <mark>custom policies</mark> that you <mark>create according to your specific requirements</mark>.

IAM policies can be <mark>attached</mark> to <mark>individual users</mark>, <mark>groups</mark>, or <mark>roles</mark>, and they determine the level of access and permissions granted to those entities. Policies can be created and customized to fulfill specific requirements and address security needs.

Once a user is created, it is necessary to assign them a set of policies that outline the actions they can perform. These <mark>policies </mark> define the <mark>permissions </mark> and <mark>authorizations </mark> for users, groups, or roles, ensuring appropriate access controls and restrictions are in place.

### 🔸 **Groups**

Groups are a <mark>way to organize users</mark> into <mark>logical collections</mark>. Instead of assigning permission individually to each user, <mark>permissions</mark> can be <mark>granted to a group</mark>, and <mark>users added</mark> to that <mark>group inherit those permissions</mark>. This simplifies the way of <mark>assigning permissions</mark> across <mark>multiple users</mark> with <mark>similar access</mark>.

In organizations, <mark>managing access for individual users</mark> can become a <mark>hectic task </mark> due to the <mark>presence of multiple departments</mark> and varying access requirements. This is where groups come into play.

Groups provide a solution for organizing users based on their common access needs.

### 🔸 **Roles**

Roles are used to <mark>grant temporary permissions</mark> to AWS services or external identities, <mark>without the need for long-term access keys</mark>. Roles define a <mark>set of permissions</mark> that determine <mark>what actions can be performed</mark> on AWS resources.

Roles in AWS are <mark>similar to users</mark>, but <mark>they are temporary</mark>. The credentials, such as <mark>usernames </mark> and <mark>passwords</mark>, associated with roles are also <mark>temporary</mark>.

Let's say you have a **<mark>web application</mark>** that needs to <mark>interact with an AWS SNS </mark> (Simple Notification Service) topic to <mark>send out notifications</mark>. Rather than <mark>embedding access keys in your application's code or configuration files</mark>, which can be <mark>risky</mark>, you can <mark>create an IAM role</mark> and <mark>assign it to your EC2 instances </mark> running the web application.

The IAM role would be <mark>configured </mark> with the <mark>necessary permissions</mark> to <mark>publish messages</mark> to the <mark>SNS topic</mark>. When your EC2 instances <mark>assume the role</mark>, they obtain <mark>temporary security credentials</mark> that <mark>grant them the permissions</mark> specified in the <mark>role's policy</mark>.

By assigning the IAM role to your EC2 instances, you ensure that <mark>only authorized instances</mark> can <mark>send notifications to the SNS topic</mark>. Additionally, <mark>you don't need to manage access keys or credentials</mark> within your application's code, as the instances automatically <mark>receive the necessary permissions through the role</mark>.

Similarly, if your application is <mark>hosted on a private cloud</mark> and needs to <mark>access storage</mark> in AWS, the application developer can <mark>use roles to grant access</mark> to AWS storage.

This approach provides a <mark>more secure</mark> and <mark>centralized way</mark> to <mark>grant permissions </mark> to your application components <mark>without exposing long-term access keys</mark>.

# **🌟**Conclusion

IAM roles are a core component of AWS security and access management. IAM roles provide a secure and flexible approach for organizations to grant access to AWS resources.

Thank you for reading this blog. If you found this blog helpful, please like, share, and follow me for more blog posts like this in the future.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.

#aws #awsiam #awscloud #DevOps #TrainWithShubham

#90daysofdevopsc #happylearning

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)