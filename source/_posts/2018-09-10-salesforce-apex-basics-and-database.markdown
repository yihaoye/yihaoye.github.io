---
layout: post
title:  "Salesforce Apex基础与数据库"
date:   2018-09-10 00:00:00 +1200
categories: crm
tags: salesforce
---


```java
List<String> colors = new List<String>();
String[] colors = new List<String>();

// Create a list and add elements to it in one step
List<String> colors = new List<String> { 'red', 'green', 'blue' };
// Add elements to a list after it has been created
List<String> moreColors = new List<String>();
moreColors.add('orange');
moreColors.add('purple');
```