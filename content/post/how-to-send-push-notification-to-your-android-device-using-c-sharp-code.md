---
author: "Sriman Saswat Suvankar"
date: 2016-11-15
linktitle: Send push notification to your android device using C# code?
title: How to send push notification to your android device using C# code?
tags: ["push notification","c sharp","PushSharp"]
weight: 10
---


## Introduction

Push notification is like a message that hits the users device.Its a modern way of engaging users in the app.Each app can have their own push notification enabled.

This article is going to cover how we can send a push notification to your mobile using a C# code.

The core things we need to send is
<ul>
<li>Token generated from the device which we want to send push notification to</li>
<li>Type of the device (Android,IOS,Windows)</li>
</ul>

### How apps work generally?

Generally you have a database server and then you have the API’s.The mobile app communicates with the API and the API’s communicate with the database and send information to your mobile app and vice versa.
So whenever we install or login to an app the app calls the API and from the API we save the token associated with the device and device type.Whenever we want to send any notification we fetch the token and send it to GCM(Google Cloud Messenger).GCM then takes care of sending it to all the devices that have your app installed.

This was a bit of information regarding the background.Now moving on to the practical implementation.

### What we need?

I was in the same situation looking for some solution and I came across a very good library called [PushSharp] (https://github.com/Redth/PushSharp).

Install [PushSharp] (https://www.nuget.org/packages/PushSharp/) from nuget.

After installing PushSharp add the following line of code.

<script src="https://gist.github.com/srimans/5c6f9ca75779cfcac3cf7e5150bdc933.js"></script>

So that’s it.

### Key notes about the code
<ul>
<li>
<b>senderId</b> and the <b>authorizationToken</b> can be found when you register the app with the GCM.</li>
<li><b>androidDeviceTokens</b> is the list of tokens or we can say the list of devices we have.These are the tokens that we have saved on server side while install or login for an app.The app calls the API to save the token into the database server.</li>
<li>In android maximum of 1000 tokens can be sent.So we have to send it in batches.</li>
<li><b>androidNotificationData</b> is the JSON we create to send the data back to the mobile device like the heading and description for a notification.</li>


Thank you for reading this post.Comments and suggestions is really appreciated 🙂