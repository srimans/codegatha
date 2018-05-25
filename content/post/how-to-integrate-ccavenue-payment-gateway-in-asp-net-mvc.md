---
author: "Sriman Saswat Suvankar"
date: 2016-11-26
linktitle: Integrate CcAvenue payment gateway in ASP.NET MVC?
title: How to integrate CcAvenue payment gateway in ASP.NET MVC ?
tags: ["c sharp","ASP.NET","MVC","Payment Gateway"]
weight: 10
---

## Prerequisites

You should have a ccavenue account.

## Problem

* The second step is the problem I faced while integrating the ccavenue page.I found out that most of the people were finding the same.As we are developing something we need to first test it in development environment.

Inside your ccavenue account they have already given you the access code,merchant Id and access key for a url.But those credentials will only work if you are redirecting to the ccavenue page from that url only.

For ex:If url set up in your account is https://xyz.com then only if you redirect from https://xyz.com then  you will be redirected to the correct page else you will get <b>1002</b> i.e <b>Merchant Authentication failed</b>.

## Solution

* Drop a mail to service@ccavenue.com along with your merchant id and test url.They will set it up for you !! Cheers 🙂

But what if they do not respond? So there is another solution.

* You can login to your account and they have a tab called <b>support</b>.In that support when you enter an email id an email comes to that mail id with some credentials.Login to that url with your credentials and <b>raise a ticket</b> there on urgent basis.Your issue will be resolved 😀 (100%).

Now comes the very important part i.e the implementation.

## Implementation

### Request

* Add 4 keys yo your web.config file inside .Development environment and production environment for both keys are different.We can only get the values from config files not set them.Storing them in web.config is the best place.

`````
<add key="CcAvenueMerchantId" value="your-merchant-id"/>
<add key="CcAvenueWorkingKey" value="your-working-key"/>
<add key="CcAvenueAccessCode" value="your-access-code"/>
<add key="CcAvenueCheckoutUrl" value="your-checkout-url"/>
/*checkout url for development is https://test.ccavenue.com/transaction/transaction.do?command=initiateTransaction
For production its https://secure.ccavenue.com/transaction/transaction.do?command=initiateTransaction */
`````

* Add a controller method called Payment.

<script src="https://gist.github.com/srimans/a1634da01a614a6cfd2a9fb6ede58ce0.js"></script>

* Add its view i.e Payment.cshtml and add the following code.

<script src="https://gist.github.com/srimans/b056156bc9a8013412e550438b9376d7.js"></script>

* Add a post action for payment.

<script src="https://gist.github.com/srimans/a3fb34d682d8bef3f72c5280272fa936.js"></script>

* Create a View called ccAvenue.cshtml.
  <br/>This bit of file does the trick.It redirects to the ccAvenue page on page load.

<script src="https://gist.github.com/srimans/27d4279ad1c3d2825e9dedcd983812f6.js"></script>

### Response

Create an Action method to which you will redirect after success.

<script src="https://gist.github.com/srimans/cd44a12874e019b6149c683f2b4cdb03.js"></script>

Thats it and you are done 🙂

## Solution

Download the sample project [here](https://github.com/srimans/BlogExamples).
