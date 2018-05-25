---
author: "Sriman Saswat Suvankar"
date: 2018-03-10
linktitle: Extension Methods
title: Extension Methods
tags: ["c sharp"]
topics: ["C Sharp Concepts"]
weight: 10
---


## Introduction

This post is about how we can take the advantage of Extension methods that is available in C#. This post will cover everything about C# extension methods. This is one of the posts under knowing C# better. In this post I will explain how we can create extension methods and how extension methods are used in real life situations.

Imagine there is a class file and some methods in the file which does some task. Today I have a requirement that I want to add some more power to the class. In order to do that I have to change the source code of the class. Let’s say now I have packaged the class into a .dll and I have given it to my customers/clients to use it. They ask for a change. Then I have to update the code and then republish the .dll and then the cycle goes on.

Now let’s say we have some thousands of clients. To manage each and every request it is very difficult. Hence the use of extension methods comes into picture.

## What are Extension Methods?

Extension methods are simply methods or functions. These methods gives us the capability to add new methods to an existing class or a type without changing its source code or inheriting from it.

They come to existence when the class that created them is in the scope.

#### Example
![ExtensionMethod example](/img/extensionmethod3.jpg)

The methods shown in the visual studio intelisense showing an arrow pointing down are all extension methods.

## How to create them?

* Create a static class.
* Create a static method inside the static class.
* First parameter of the method should be of the same type you are trying to extend.

<script src="https://gist.github.com/srimans/e84e34067e1637eb0cfe68f8cc1751ea.js"></script>


In the above example I am trying to add existing functionality to the string type. So I have created a static class called StringExtensions that has a static method GetFirstNWords().

To use this method GetFiirstNWords(), we can simply create a string variable and then use this method.

This doesn’t even require instantiating the class. The syntax can the following :

<script src="https://gist.github.com/srimans/30d6f3a7b6205475f2e666d542f7a621.js"></script>

In the above example we have created an extension for string type. We can get first N words of a any string that is within the scope of the extension method.

## Where not to use?

### On static class  
You can’t add static methods to a type. You can only add (pseudo-)instance methods to an instance of a type.

The point of the this modifier is to tell the C# compiler to pass the instance on the left-side of the . as the first parameter of the static/extension method.

In the case of adding static methods to a type, there is no instance to pass for the first parameter as single instance is created for the static method.

Extension method definitions require an instance of the type you’re extending. It is because an extension method is used to extend an instance of an object. If they didn’t do that they would just be regular static methods.

## Points to remember
1. We can generally use it on sealed classes as we cannot inherit from the sealed class.
1. An extension method with the same name and signature as an instance method will not be called.
Example: Let’s say we have a GetNWords() in the base System.String class. We would not  have been able to use our GetNWords() in extension method. GetNWords() in the System.String class will be called every time you try to invoke it.

1. Extension methods cannot be used to override existing methods. They are just there to add more power to existing class.

## Where I used it?
* <a href="/post/how-to-use-helper-methods-in-asp-net-mvc/" target="_blank">HtmlExtensions</a>
* <a href="/post/how-to-use-helper-methods-in-asp-net-mvc/" target="_blank">UrlExtensions</a>
* Extending the queries from the database and converting them to custom view objects.

Thank you 🙂

I am attaching the source code <a href="https://github.com/srimans/BlogExamples" target="_blank">here</a> . Keep following me for more updates.