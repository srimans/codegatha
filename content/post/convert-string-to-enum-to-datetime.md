---
author: "Sriman Saswat Suvankar"
date: 2016-11-29
linktitle: String conversions in C#
title: String conversions in C#
weight: 10
tags : ["c sharp"]
---


## Introduction

This post will contain small code snippets that will convert a string to different types like a datetime,enum etc...

### string to enum
The below snippet will convert string to an enum value.

<script src="https://gist.github.com/srimans/72069a4c39497e177bc940f3e1149287.js"></script>

### string to DateTimeOffset

The below snippet will convert string to DateTimeOffset object. If the string cannot be converted then return current DateTimeOffset.

<script src="https://gist.github.com/srimans/2c451780b578d83552ba810468f36403.js"></script>

