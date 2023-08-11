---
title: "AWS S3: Simple Storage Service with Handson Lab"
datePublished: Thu Jul 13 2023 04:42:54 GMT+0000 (Coordinated Universal Time)
cuid: clk0nzdce000k0ammdv6y21pr
slug: aws-s3-simple-storage-service-with-handson-lab
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689151448045/cc51571b-df3d-47ae-830e-f06e12fda4ec.png
tags: aws, devops, s3, 90daysofdevops, trainwithshubham

---

# **🌟** Introduction

S3 offers virtually unlimited storage capacity, high durability, and availability, ensuring data protection and accessibility. It integrates well with other AWS services and provides robust security features to control access and encrypt data. S3 is widely used by individuals and businesses to store various types of files, making it a popular choice for data storage and backup in the cloud.

![AWS S3](https://www.edureka.co/blog/wp-content/uploads/2016/10/1_B9CIOrxdROHvtdmouQA1_A-removebg-preview-300x225.png align="center")

# **🌟** What is AWS S3?

Amazon Simple Storage Service (Amazon S3) is a highly scalable and reliable cloud storage service provided by Amazon Web Services (AWS). It offers a simple web services interface that allows individuals and businesses to store and retrieve any amount of data from anywhere on the web.

With AWS S3, you can store and retrieve data objects such as images, videos, documents, and any other type of file. It provides virtually unlimited storage capacity, allowing you to store as much data as you need without worrying about capacity constraints.

S3 offers durability, ensuring that your data is stored redundantly across multiple devices and facilities within an AWS Region. This redundancy minimizes the risk of data loss due to hardware failures or disasters. It also provides high availability, enabling you to access your data whenever you need it.

One of the key advantages of S3 is its scalability. You can start with a small amount of storage and easily expand it as your needs grow. S3 seamlessly handles the increased storage requirements without any disruption to your applications or workflows.

S3 also offers robust security features to protect your data. You can manage access to your data using AWS Identity and Access Management (IAM) policies, bucket policies, and Access Control Lists (ACLs). Additionally, you can enable server-side encryption to ensure the confidentiality of your data.

AWS S3 integrates well with other AWS services, allowing you to build scalable and cost-effective solutions. For example, you can use S3 with AWS Lambda for serverless computing, Amazon CloudFront for content delivery, or Amazon Athena for data analytics.

# **🌟** Why do we need AWS S3?

There are several reasons why businesses and individuals may need AWS S3 (Amazon Simple Storage Service):

1. **Scalable Storage**: AWS S3 provides virtually <mark>unlimited storage capacity</mark>, allowing businesses to store and retrieve <mark>large amounts of data</mark> as their needs grow. It eliminates the need for investing in and managing on-premises storage infrastructure.
    
2. **Data Backup and Recovery**: S3 is an <mark>excellent solution</mark> for <mark>data backup</mark> and <mark>recovery</mark>. It offers high durability, storing data redundantly across multiple devices and facilities. This <mark>reduces the risk of data loss</mark> and provides <mark>reliable backup</mark> options for critical business data.
    
3. **Cost-Effective**: AWS S3 follows a <mark>pay-as-you-go model</mark>, where you only <mark>pay for the storage and bandwidth</mark> you use. There are <mark>no upfront costs</mark> or <mark>long-term commitments</mark>. This makes it cost-effective, especially for small businesses or startups that want to minimize infrastructure costs.
    
4. **Data Accessibility**: S3 allows <mark>easy and secure access</mark> to data from anywhere on the web. It provides a simple web services interface and supports various access control mechanisms to manage user permissions effectively.
    
5. **Integration with Other AWS Services**: S3 seamlessly <mark>integrates</mark> with <mark>other AWS services</mark>, enabling businesses to build scalable and powerful applications. It can be used with services like <mark>AWS Lambda, Amazon Athena, Amazon CloudFront, and more, to process, analyze, and deliver data efficiently.</mark>
    
6. **Security and Compliance**: S3 offers <mark>robust security</mark> features, including <mark>access control mechanisms</mark>, <mark>encryption options</mark>, and <mark>logging capabilities</mark>. It helps businesses meet compliance requirements and ensures the confidentiality and integrity of their data.
    
7. **Content Distribution**: AWS <mark>S3 integrates</mark> with <mark>Amazon CloudFront</mark>, a content delivery network <mark>(CDN)</mark>, allowing businesses to distribute their content globally with <mark>low latency and high data transfer speeds</mark>.
    

## **🌟 Different types of data storage in AWS S3?**

You can store virtually any kind of data, in any format, in S3 and when we talk about capacity, the volume and the number of objects that we can store in S3 are unlimited.

\**An object* is the fundamental entity in S3. It consists of data, key and metadata.

When we talk about data, it can be of two types-

* Data which is to be accessed frequently.
    
* Data which is accessed not that frequently.
    

Therefore, Amazon came up with 3 storage classes to provide its customers the best experience and at an affordable cost.

In AWS S3 (Amazon Simple Storage Service), different storage classes are available to meet various data storage needs. Here are the different storage classes in S3 with real-time examples:

1. **S3 Standard**: This storage class is suitable for <mark>frequently accessed data</mark> and <mark>real-time applications</mark>. For example, a popular e-commerce website stores its product images and website assets in S3 Standard to ensure fast and reliable access to the images for customers browsing the website.
    
2. **S3 Intelligent-Tiering**: This storage class automatically moves data between <mark>two tiers based</mark> on access patterns: <mark>frequent access</mark> and <mark>infrequent access</mark>. An example could be a media streaming platform that hosts a vast library of video content. Frequently watched videos are kept in the frequent access tier, while less popular videos are moved to the infrequent access tier, optimizing costs without sacrificing performance.
    
3. **S3 Standard-IA (Infrequent Access)**: This storage class is ideal for data that is <mark>accessed less frequently</mark> but requires <mark>rapid access when needed</mark>. For instance, a data analytics platform that stores large datasets for periodic analysis may use S3 Standard-IA to efficiently store and retrieve data during analysis runs, while keeping storage costs lower compared to S3 Standard.
    
4. **S3 One Zone-IA**: This storage class is <mark>similar to S3 Standard-IA</mark> but <mark>stores data in a single Availability Zone</mark>. It is suitable for scenarios where data redundancy is not a critical requirement, and cost optimization is a priority. A backup system that stores infrequently accessed data in a single region could use S3 One Zone-IA to save on costs.
    
5. **S3 Glacier**: Glacier is designed for <mark>long-term data archival</mark> with <mark>lower storage costs</mark>. A financial institution might use S3 Glacier to <mark>store historical transaction records</mark> that need to be retained for <mark>regulatory compliance purposes</mark>. Although the data is <mark>rarely accessed</mark>, it can be retrieved when required for auditing or legal requirements.
    
6. **S3 Glacier Deep Archive**: This storage class offers the <mark>lowest storage costs </mark> and is suitable for <mark>rarely accessed and highly cost-sensitive data</mark>. An example could be a research institution that archives large volumes of scientific data, such as genomic sequences or climate data, for future reference. These datasets may have minimal retrieval requirements but need to be stored for extended periods at the lowest cost.
    

# **🌟** Steps to create an S3 bucket

* First <mark>create an account</mark> on AWS. You can create **<mark>AWS Free Tier</mark>** on AWS Cloud, you can create a Free Tier account by going to Google, searching for AWS free tier account and follow the link.
    

![](https://miro.medium.com/v2/resize:fit:700/1*DchWVmuC_oXpK-Xa3h5lfw.png align="left")

You can create new account by following the link and after that it will ask you for your information; just follow the steps and you are ready to go. It will ask for your card information but its free, so you won’t be charged for anything if you use only AWS free Tier limit. Or if you already have one you can simple login to your account.

I already have one, so I am going to use my account.

After you logged in go to your <mark>AWS console</mark> and look for service S3. You can search for <mark>S3 </mark> in the search bar or can find it simply by clicking on Services on the left top.

* AWS console screen with recently visited services.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689144929465/af26c30d-eeea-45a7-ad82-8196e1a18e37.png align="left")

* On the AWS console screen click on **<mark>S3</mark>**.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689144906333/01259d26-0224-4378-9e62-bfb1281ed94e.png align="left")

On the Console Screen create a bucket.

This screen will show up. Click on **<mark>Create Bucket</mark>** button.

* After clicking on **<mark>Create Bucket</mark>** Button you will see the screen like this. Just fill in the **<mark>bucket name</mark>** and don’t change any permissions and click **<mark>Create Bucket</mark>** button at the bottom of the screen.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689144963395/9093f7c2-a43f-4310-b141-cc0cac19ca5b.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689145026258/f9b8bfcd-e7ad-42e8-bb73-8b7563819fc4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689145039995/873f4a9d-6b26-4f4d-84be-e9bffe67fac4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689145051732/5f525ab7-cf3a-43a7-8884-1c04dc9970d7.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689145078180/3c4d820f-aa1f-488c-9343-4f4a5633d8d6.png align="center")

* After that, you will see all the created buckets here. Now click on the recently created bucket to upload your website or image.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689145104536/9e4287fc-3e49-4b08-b067-c0d0f2d75a54.png align="left")

* Click on the recently created bucket, you see it empty now it's time to **<mark>upload files/folder</mark>** AWS S3 Buckets list.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689145180975/990ac7e0-02fa-4675-ab4e-20157bf4729d.png align="left")

* Here in the selected bucket, you can upload your folder or simply drag your folder here to upload files It will take some time to upload all your files, so wait.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689145201284/ba0b900b-20e9-4b8e-9cc1-7fb724ab37f8.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689145247143/c9b842b3-2171-4d95-ba4f-14047fa08a3b.png align="center")

* Now your file <mark>uploaded successfully</mark>.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689145281878/75de3cf0-5f97-4763-b863-59bdd46dcda1.png align="center")

* Refresh your web browser and now you see your object in the bucket.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689145301973/03a5efb5-48ec-4d47-9b6c-6047b1d9432a.png align="left")

* You will see your output as an image as an output.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689145314871/ee1884f0-fdf0-4a6e-9853-02e51ea39df9.png align="center")

# **🌟** Conclusion

S3 is a core service of AWS Cloud Computing. Here we saw what is AWS S3, why we need AWS S3 and different types of data storage in S3. We also do a hands-on lab on how to create an s3 bucket, and how to upload files such as images. If you want how to access the AWS S3 bucket using AWS CLI refer to the blog link below.

[AWS\_S3\_CLI](https://dushyantkumark.hashnode.dev/aws-cli-on-your-local-machine)

Thank you for reading this blog. If you found this blog helpful, please like, share, and follow me for more blog posts like this in the future.

\\...................................................................................................................................................

The above information is up to my understanding. Suggestions are always welcome. Thanks for reading this article.

#aws #S3 #awscloud #DevOps #TrainWithShubham

#90daysofdevopsc #happylearning

@[Shubham Londhe](@TrainWithShubham) **Sir**

<mark>Follow for many such contents:</mark>

<mark>LinkedIn</mark>: [**linkedin.com/in/dushyant-kumar-dk**](http://linkedin.com/in/dushyant-kumar-dk)

<mark>Blog</mark>: [**dushyantkumark.hashnode.dev**](http://dushyantkumark.hashnode.dev)