---
author: "Sriman Saswat Suvankar"
date: 2018-01-11
linktitle: Not knowing our infrastructure cost us big time
title: We destroyed it!!!Not knowing our infrastructure cost us BIG TIME!!!
weight: 10
tags: ["SQL Server","Story"]
topics: ["Dev Stories"]
---


## Introduction

Of late I have not been writing posts that are related to coding. Of late things are mostly related to experiences. But keep calm. More posts related to coding are coming soon. Keep following for more updates as they say 😉

`````
We destroyed it……Not knowing our infrastructure cost us BIG TIME!!
`````

This line goes way back to the late 2016’s and the early 2017’s when I was working with a startup as a software developer. I was the first developer hired by them and I was enjoying what I have been doing. Of course learning new things is always fun.Isn’t it?

We knew one big feature was coming. To get this big feature out we had to do a lot of restructuring to the code.It was months of hard work. A special tool was built in order to do the restructuring of data in the database. For things to work, we needed a restructuring and we did it. We built it ,we tested it and YEAHHHHH!!! 🙂 Finally we are going to go live on the next day.

### THE BIG DAY
There comes the big day when we had to deploy the changes.We had to run the special tool to do the changes in the database and then we had to deploy the latest changes of the website to the main server.

Note : It feels very lame to say this but we were a very small company with no staging or test servers. Whatever was done was directly deployed to live after testing in development. It is very lame but it was like that only.

### MISTAKE 1
Before doing the changes as we knew they were all related to the database,we took a backup of our database.We had an automatic backup of database happening twice daily.The backup I took manually was kept in the same place where automatic backup was happening.

### MISTAKE 2
Hell yeah we were confident of our application.Kudos to our courage(I say it in a sarcastic way) that we connected to the live database(remote database) from our local machine.It took a lot of time.There were many steps which the tool had to do.To complete a single small step it took ages. Frustrated by that and thinking that it’s never going to complete ,we stopped the application.

Oo….Now its 12 o’clock in the afternoon and guess what!!! Automatic backups have happened. The backup taken by me was indeed overwritten and we have corrupted the database. It was the live database.

### MISTAKE 3
Executing and making these kind of changes should be done when you have less people coming into your site or less traffic on your site. Of course there were less people visiting the website on those days and did not hamper our business a lot.

Our minds ran helter skelter calling people to know how we can get out of this. Looking for possible solutions to restore database in stack overflow. We tried restoring our database to some point of time where it was all right for us. We tried looking for our backup on cloud.

But all in vain!!!!!
`````
We destroyed it and we just destroyed our database
`````

Not knowing where backups are stored on cloud,not knowing/realizing the time for automatic backups,putting the backup on the same folder where automatic backup happened and connecting to remote database from our local machine and doing extensive database operations is what we did and it KILLED us!!

### RELIEF
I was filled with some sort of happiness when I saw a backup which was four days older. Without having any way out we restored it against our live database. We moved the tool to the remote machine(it was just an .exe).Executed the program locally(where database server was hosted). Finally we were back but we lost four days of data. We apologized to our small marketing team for doing this and we lost their four days of hard work.

Having extra servers would have definitely helped us. But nevertheless there is always some learning happening 🙂

P.S : In the whole post We means me and my colleague in the company.We were both trying to solve the task. Small company and whole onus was on us and like in a startup you have the liberty to touch each parts of the whole system.

Hope you enjoyed the post and you won’t make the mistake that we did!! Keep following for more posts 🙂