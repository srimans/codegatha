---
author: "Sriman Saswat Suvankar"
date: 2018-01-27
linktitle: Upload file to amazon S3 bucket using c# code
title: How to Upload File to Amazon S3 Bucket?
tags: ["Amazon S3","Cloud Storage","c sharp"]
weight: 10
---


## Introduction
S3 stands for <b>Simple Storage Service</b>. It is one of the many services provided by Amazon.
This post is all from my experience and what I have learnt during my short professional career.
If you are talking of Amazon storage services then it is a very big and unending topic to write on but here I will take example of a simple file to upload into the bucket.
Not only uploading but is very important to write the code in an effective way such that it is easy to understand and make subsequent changes easily. 
I  will give you few tips which will certainly help you in writing code in a better way.

So here it goes……..

Although the implementation is simple but I will make sure a good architecture is maintained so that our   <b>DRY</b>(<b>D</b>on't <b>R</b>epeat <b>Y</b>ourself) is still kept intact.

When we are doing real life projects there are many instances where uploading a content to any service be it a cloud service,or file system we tend to violate DRY principle. Somehow we end up using hard coded strings in our views(.cshtml) files. One simple change in the requirement means we have to change everywhere and then we test. Developer might have forgotten to change one file due to which it again comes back to him and then change again,test again and a lot of time goes in this. All the time wasted can be saved if you do not repeat yourself. One change one shot and boom… Your feature change is published in seconds…. Keep in mind,always try not to repeat yourself while writing code.

S3 stands for Simple Storage Service. As the post heading goes it is provided by Amazon.You can take help of buckets to store your photos,files and documents. Buckets are like containers. Those who are familiar with Microsoft Azure, it's like azure container service.You can read more about Amazon s3 bucket from [here] (https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingBucket.html).

### Step 1
Very first step in each and every project is creating a good architecture. A good architecture always saves you a lot of time in development. It also increases speed of delivery of your features for testing. First we will create an interface.

<script src="https://gist.github.com/srimans/e3741e546f5165ef665408c7c3a585f7.js"></script>

### Step 2
Add keys to web.config file. Keys should be declared there in Web.Config files as they might change depending upon the test environment and production environment.

<script src="https://gist.github.com/srimans/d044ecbd1e4a1267aec62a4f474ae3b4.js"></script>

### Step 3
Add the dll/reference using the nuget package from [here] (https://www.nuget.org/packages/AWSSDK/2.3.55.2) . Or run the following command in package manager console.

### Install-Package AWSSDK -Version 2.3.55.2

### Step 4
Create a class that will inherit this interface.Lets name it ContentService.

<script src="https://gist.github.com/srimans/01c095e9ccb48d48a170ab8e391e8609.js"></script>

<b>CASE:</b> Suppose we want to save history of resumes uploaded by a user then the structure of our file uploaded on s3 can be
`````
amazon-base-url/bucket-name/content-type/content-folder-name/file-name
`````
<b>FileName</b> can be timestamp or a GUID.

<b>Stream</b> is input stream found in System.IO namespace.

<b>Content Folder</b> Name can be unique-ids of your entities(business objects)

<b>ContentType</b> is an enum/static string class file that will contain the folder name. Depending on business requirement you might have different type of contents. For ex: user documents might be one content type, images of products can be another one.

If you are using Dependency Injection
`````
DO NOT FORGET TO REGISTER DEPENDENCIES FOR THE ICONTENT SERVICE
`````

IMPORTANT
* In real life scenarios when we are creating an application we tend to hardcode string files in .cshtml files while getting content full url. We need not have to hardcode strings in .cshtml files.
* Only thing we need is an urlHelper and htmlHelper classes that will take care of repetitions in code.To learn about Html helpers and Url Helpers click here.
* Business logics/repository will do the validations for checking which kind of file we upload(.jpg/.png/.pdf) and what should be the size of the file. Then it can call the contentService to use it for uploading and getting content.

You can add more methods to contentService like deleting content according to your requirements.

Hope you learnt something. Keep following for more posts :)

