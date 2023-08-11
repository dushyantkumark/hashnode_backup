---
title: "Setup your Identity And Access Management
 [ IAM -> Group -> User -> Security Credentials  ]"
datePublished: Fri Jul 07 2023 12:43:53 GMT+0000 (Coordinated Universal Time)
cuid: cljskitbp000d09l09sidfvey
slug: setup-your-identity-and-access-management-iam-group-user-security-credentials
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1688733738182/f3994e6c-2696-4504-b150-5986e31a852b.png
tags: aws, iam, iammfaaccess-key-idsecret-access-key, 90daysofdevops, trainwithshubham

---

# **🌟** Steps to setup IAM

If you want to know what is <mark>AWS IAM</mark> , refer to this article [AWS\_IAM\_Detail](https://dushyantkumark.hashnode.dev/introducing-the-power-of-identity-and-access-management-iam) .

To create IAM users and groups on AWS, you can follow some steps:

* Sign in to the AWS Management Console and open the home AWS console.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688292862695/1854b6aa-3ff5-442e-a7cc-37bed25dfcb1.png align="center")

* open the Identity and Management (IAM) console.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688736062260/f453f95b-0b21-4931-9eea-870ddabb6be1.png align="center")

* Go to the dashboard and click user groups and then click on create group.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688293073732/35e8233a-e57c-4234-aef5-6c4fc35b02c2.png align="center")

* Provide a group name and optionally provide a path.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688293106422/1ac9c43b-ec6c-4f3f-b4a8-111430c3d348.png align="center")

* Set the group's permissions by <mark>attaching policies</mark> that define the group's access.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688293126986/00131613-16fb-4630-85d4-c4ea7e759bf8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688293163378/a529071f-c621-4691-bee0-b9bcede717fd.png align="center")

* Review the group's settings and click on "Create group."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688735997854/fc6ea9c8-78e3-4e8c-9850-df3b02314af6.png align="center")

* Check your group is created (aws\_admin).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688293191333/d704f1dd-5a0b-43a8-b850-8b426740284d.png align="center")

* Click on "Add user" in the "Users" section.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688293330590/bc8a8e7a-3ac3-4134-9f30-cab47859ed3b.png align="center")

* Provide a username for the new user
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688293498230/53692bb1-e8fd-4b63-9c77-3ba4a77556a6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688293518915/997ee0d8-51e4-4831-969f-f408596a4eeb.png align="center")

* Set the <mark>user's permissions</mark> by adding them to groups, <mark>attaching policies</mark> directly, or customizing their access.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688293605678/603d411b-8c20-4a59-8c08-69bfb0eda5b2.png align="center")

* You get a <mark>User name</mark> and <mark>Password</mark> for signing into AWS Management Console.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688736322327/5a0cb377-4e14-476c-bf9f-e6651a925fd4.png align="center")

* Go to <mark>security credentials</mark>, generate an <mark>access key</mark> for <mark>programmatic access </mark> or enable the AWS Management Console access.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688736165969/047a5338-a8f5-43ec-bcd8-e4332be23d98.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688293949862/b53d11ff-4c08-4fc3-8634-d25903e11e19.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688293928549/fe1936fa-131f-4095-92c6-3619d5396266.png align="center")

* Give a tag/ description to your keys.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688294154594/aa784acd-1fa1-41b2-83f5-68f319dcbb49.png align="center")

* Download the <mark>CSV file</mark> that contains the <mark>access key</mark> and <mark>secret access key</mark>.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688736229082/6bce070e-b7b5-40ed-99f7-0278fc387b01.png align="center")

# **🌟**Conclusion

IAM is a core component of AWS security and access management. Here we saw how to create IAM users, groups and access keys to access AWS services using AWS CLI.

If you want to know how to set up <mark>AWS CLI</mark> in your window machine and how to access AWS resources, refer to this article [AWS\_CLI](https://dushyantkumark.hashnode.dev/aws-cli-on-your-local-machine) .

Thank you for reading this blog. If you found this blog helpful, please like, share, and follow me for more blog posts like this in the future.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.

#aws #awsiam #awscloud #DevOps #TrainWithShubham

#90daysofdevopsc #happylearning

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)