---
author: "Sriman Saswat Suvankar"
date: 2018-04-02
linktitle: Helper Methods in .NET MVC
title: How to use Helper Methods in .NET MVC?
tags: ["ASP.NET","MVC","c sharp"]
weight: 10
---


## Introduction

Helper Methods are nothing but simply extension methods. If you are wondering what actually an extension method is then check <a href="/post/how-to-use-extension-methods-in-c-sharp" target="_blank">this</a>. This post will talk about different types of helpers -:

* HtmlHelpers
* UrlHelpers

Implementing both of them is same like implementing extension methods. Before implementing them it is important to know why we will implement them. Things can also work without them also.

## Why Implement Helper Methods?
The main reason why we want to use helper methods is code reusability.

If you are new to razor or you have used razor then you must have used

* @Html.Textbox(….)
* @Html.Label(…)
* @Html.Partial(…)
* @Url.Action(…)
* @Url.Content(…)

These are nothing but in built helper methods.You can use them as soon as you create a view. If you have a piece of html that you want to use in many places, then go ahead and create a helper method. The main advantage of keeping them is any change done to that piece of code will be done in one place only.

## How to Implement Helper Methods?

I will create one simple custom helper method. Custom means it will be my own method. I will not use any of the in built .Net helper methods. I will give examples each for <b>HtmlHelper</b> and <b>UrlHelper</b>.

### HtmlHelper

For HtmlHelper there is a simple horizontal box that needs to be rendered in many views. For that we will use HtmlHelper.

* Create a class called HtmlExtensions
* Create a Method called HorizontalBox

<script src="https://gist.github.com/srimans/5943bd88f5e14b8a5563459fa950336d.js"></script>

* Create a partial view called HorizontalBox.cshtml
* In the view add @Html.HorizontalBox()

Lets say tomorrow we need to change the name of HorizontalBox to something else,we have to do it in one place only. Lot of time is saved. Hence life of a developer is easy.

### UrlHelper

For UrlHelper we have a ContentService built that uploads our documents somewhere into cloud and gets url of the uploaded file. To know more about how to build a service and upload files,check <a href="/post/how-to-upload-file-to-amazon-s3-bucket-using-csharp-code/" target="_blank">this</a>.

* Create a class called UrlExtension
* Add a method Logo. 

<script src="https://gist.github.com/srimans/6efae97f6f37cc2f9fd229c3aa3063ab.js"></script>

* In the view add @Url.Logo(some-id-or-filename)
<b>ContentType</b> can be an enum of different types of files you are saving. One may be a PAN card, one may be a Voter Id etc..

You do not need to hardcode the path in many views. Updating the things becomes difficult and code maintainability becomes a headache. So taking help of helper methods is an easy option to have.

## IMPORTANT!!!

When you do @Html. Or a @Url. you still cannot find them in the view. So we are missing some reference here. Go to View/Web.Config and under add the following

`````
<add namespace="HelperMethods.Web.Extensions"/>
`````

<b>Namespace value must be replaced with your namespace in which the helper class resides.</b>

Without this things won’t work.

As you saw things are very easy to implement. Under the hood @Html.TextBox or any inbuilt .Net Html helper or UrlHelper works the same way.These are extension methods extending from <b>UrlHelper</b> class or a <b>HtmlHelper</b> class.

You can find the full source code <a href="https://github.com/srimans/BlogExamples" target="_blank">here</a>. Keep following me for more updates.

 


