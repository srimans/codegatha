---
author: "Sriman Saswat Suvankar"
date: 2017-01-28
linktitle: Host a website locally on IIS
title: How to host a website on local IIS?
tags: ["IIS","Hosting"]
weight: 10
---

## Prerequisites

You already have installed IIS on your system.If IIS is not installed then go to 
#### Control Panel -> Programs and features -> Turn on windows features on or off

## Steps

* Add a new MVC Web application.Here I have added it to the path <b>E:\ </b>

![CreateProject](/img/11.jpg)
![CreateProject](/img/21.jpg)

* Open the IIS by pressing <b>Windows+R</b> and then type <b>inetmgr</b>. Right click on folder <b>Sites</b> and click <b>Add Website</b>

![AddWebsite](/img/31.jpg)

* Enter the site name as you want and the host name as per your requirement.Put the <b>IPAddress</b> as <b>127.0.0.1</b>.Host name is the name by which our local website runs and 127.0.0.1 is the IP address for <b>localhost</b>.

![AddWebsite](/img/4.jpg)

* Update the host file by going to <b> C:\Windows\System32\drivers\etc </b>. Open the hosts file in <b>notepad</b>.Run notepad as <b>administrator</b>.

![AddWebsite](/img/51.jpg)

* Update the hosts file by adding an entry with the <b>IPAddress</b> and <b>host name</b>.

![AddWebsite](/img/72.jpg)

* Open the browser and then run the website.

![AddWebsite](/img/91.jpg)

Yeahhh!!!Finally you have hosted your website locally  🙂 In the next blog [post](/post/how-to-create-logging-and-connect-locally-hosted-website-to-to-database) I will try to connect the locally hosted website with database on sql server and create a logging.