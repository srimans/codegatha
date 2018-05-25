---
author: "Sriman Saswat Suvankar"
date: 2017-02-02
linktitle: Create Logging And Connect Locally Hosted Website to Database
title: How to create logging and connect locally hosted website to database?
tags: ["IIS","Hosting"]
weight: 10
---

This post is a continuation of my previous <a href="/post/how-to-host-a-website-locally-on-iis/" target="_blank">post</a>.Here we will see how we can create a login and connect your web application to the database.

In real life scenarios when we are hosting the website on the IIS and we also have the application pointing to a database then we need to have proper logging and proper permissions set up.If not then we will get a yellow screen saying...

`````
Cannot open database database-name requested by the login. 
The login failed.Login failed for user IIS APPPOOL\App-pool-name.
`````
<b>App-pool-name</b> is generally the name under which you have hosted the website on IIS.

## Prerequisites

* Already hosted website on IIS.
* Already created database lets say Test.

## Steps

* Expand the security tab and then right click on Logins.

![Login](/img/12.jpg)

* Select the new Login option.

![NewLogin](/img/22.jpg)

* In general tab put the login name as IIS APPPOOL\app-pool-name.In my case its test.in.So login name is <b> IIS APPPOOL\test.in </b>.

![LoginName](/img/32.jpg)

* Click on User Mapping tab on the left and select master and test.Below on the database role membership for <b>master</b> select the <b>db_owner</b>.Click <b>Ok</b>.

![User Mapping](/img/41.jpg)

* Point your web application to the Test database.

![Point Application To Test Database](/img/5.jpg)

Yeah!! Now you have hosted website locally and connected to database as well.

Thanks for reading this post. Keep following me for more updates.