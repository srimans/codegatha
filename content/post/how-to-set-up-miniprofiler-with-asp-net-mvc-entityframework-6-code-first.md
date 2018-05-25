---
author: "Sriman Saswat Suvankar"
date: 2017-07-03
linktitle: Set up Miniprofiler with ASP .Net MVC EntityFramework 6 CodeFirst?
title: How to Set up Miniprofiler with ASP .Net MVC EntityFramework 6 CodeFirst??
tags: ["Mini Profiler","c sharp","Entity Framework"]
weight: 10
---

## What is a Profiler?

Profiling helps in gathering information about an executing application, i.e how much time is spend where which in turn helps allowing to determine those improvements that are required in the application. Anything that helps us do profiling is called as a <b>profiler</b>.

Read more about <a herf="https://www.red-gate.com/simple-talk/dotnet/net-performance/the-why-and-how-of-net-profiling/" target="_blank">why profilers</a> and <a herf="https://dzone.com/articles/5-good-and-useful-net" target="_blank">good</a> .NET profilers.

One of them is <a href="https://miniprofiler.com/" target="_blank">Miniprofiler</a>

## MiniProfiler

Miniprofiler is developed by the famous team at StackOverflow. Clients using MiniProfiler are

* Godaddy
* StackOverflow

### Steps

* First of all we need to install two nuget packages <a herf="https://www.nuget.org/packages/MiniProfiler/" target="_blank">MiniProfiler</a> and <a herf="https://www.nuget.org/packages/MiniProfiler.EF6/" target="_blank">MiniProfiler.EF6</a>

* In order to use the profiler we need to add the following to Global.asax file.

<script src="https://gist.github.com/srimans/ae9fb85a7c632f677db81179fa10bb7e.js"></script>

* Then we need to add the following line in the SiteLayout.cshtml file just above the closing of the head.

<script src="https://gist.github.com/srimans/b7a6cef6788f4e25c8bf14bde35e3e3c.js"></script>

* Add the code that you want to profile. My case is <b>HomeController</b> and <b>Index</b> action.

<script src="https://gist.github.com/srimans/8e18b595956d51d3d1e4a8879510d1f7.js"></script>

* Doing the above steps you will still not be able to see the Profiler output when you run the application.To check the profiler output add the following code to <b>Web.Config</b> file.

`````
<system.data>
<DbProviderFactories>
<remove invariant="MvcMiniProfiler.Data.ProfiledDbProvider" />
<add name="MvcMiniProfiler.Data.ProfiledDbProvider" invariant="MvcMiniProfiler.Data.ProfiledDbProvider"
description="MvcMiniProfiler.Data.ProfiledDbProvider"
type="MvcMiniProfiler.Data.ProfiledDbProviderFactory, MvcMiniProfiler, Version=1.6.0.0, Culture=neutral, PublicKeyToken=b44f9351044011a3" />
</DbProviderFactories>
</system.data>
`````

* This is all for the simple MiniProfiler.If you run your application you may see something like this.

![MiniProfilerSuccess](/img/1.jpg)

* Now comes the part of setting up with CodeFirst. For implementing this we have already installed MiniProfiler.EF6.We just need to add it to Application_Start().

<script src="https://gist.github.com/srimans/405e4d201db25fe65c780fcf2aa3de69.js"></script>

* Add the following code to Web.Config file.This will help in profiling for the queries that are executing.

`````
<system.webServer>
<handlers>
<add name="MiniProfiler" path="mini-profiler-resources/*" verb="*" type="System.Web.Routing.UrlRoutingModule" resourceType="Unspecified" preCondition="integratedMode" />
</handlers>
</system.webServer>
`````

Thats it. Miniprofiler will be up and running.Yeah….. 🙂

## Errors

The above steps will help you in setting up MiniProfiler. But when I set it up, our project had some dependencies and I was getting few errors while setting this up. In this section I will take you through what errors you are likely to get and how you can resolve it 
if your project has some extra dependencies like mine on other third party libraries.

`````
Unable to define EFProfiledDbProviderServices class of type ‘ProfiledDbProviderServices’. Please check that your web.config defines a <DbProviderFactories> section underneath <system.data>
`````


* This error will come up when you have not done the last point.
* You have correctly added the code as mentioned in last point but still get the error.Make sure that you don’t have HibernatingRhinos initialization on. It isn’t compatible with EntityFrameworkProfiler.Check <a href="https://community.miniprofiler.com/t/will-mini-profiler-support-ef6/19/9" target="_blank">here</a>.

The next error that I was getting is almost same as the above one but a slightly different one related to Glimpse.It is such that in our project we had installed glimpse but we were not using it and then we decided to use this MiniProfiler.The error is

`````
Unable to define EFProfiledDbProviderServices class of type ‘GlimpseDbProviderServices’. Please check that your web.config defines a <DbProviderFactories> section underneath <system.data>
`````

You get this error when you have Glimpse installed in your project. Just make sure you uninstall Glimpse. If you still see this error coming then make sure you get to the bin folder of the application and delete Glimpse related files. Check <a href="https://stackoverflow.com/questions/23601378/why-is-glimpse-still-running" target="_blank">here</a>.

Read more about the implementation from <a href="https://www.hanselman.com/blog/NuGetPackageOfTheWeek9ASPNETMiniProfilerFromStackExchangeRocksYourWorld.aspx" target="_blank">here</a> and <a href="https://samsaffron.com/archive/2011/07/25/Automatically+instrumenting+an+MVC3+app" target="_blank">here</a>.

Thanks for reading the post. Comments and suggestions are welcome 🙂. 
