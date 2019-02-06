---
layout: post
title:  "在Visualforce中嵌入React应用"
date:   2018-06-08 14:05:11 +1200
categories: crm
tags: salesforce
---
原文参考：https://medium.com/@rajaraodv/developing-react-redux-apps-in-salesforce-s-visualforce-3ad7be560d1c  
原文参考：https://sfdcnotes.github.io/2016/02/15/salesforce1-platform-guide/  
原文参考：https://www.salesforce.com/video/304788/  

Salesforce在设计之初时参考当时流行的MVC模式  
Model：SObject （salesforce对象，比如Account、Contact等等）  
View：Visualforce  
Controller：Apex Code  

Visualforce是服务器端模版语言，用来自定义用户桌面，其设计参考了当时JSP。而现在服务器端模版语言已经渐渐淘汰，因此是否能在Visualforce上使用React等新的前端框架会是一个有趣的探索。  
在进入主题前讲一个题外话，也许是salesforce本身也认识到Visualforce技术已经老旧了，因此salesforce本身也推出了Lightning Components framework这一SPA前端框架作为他们的改进方案。  

一个简单Visualforce页面：
```html
<apex:page>
    <html>
        <head></head>
        <body>
            <h1>hello, world</h1>
        </body>
    </html>
</apex:page>
```

<!-- more -->

Salesforce的Visualforce的["Container" Page](https://developer.salesforce.com/docs/atlas.en-us.214.0.pages.meta/pages/pages_html_container_page.htm)：
```html
<apex:page docType="html-5.0" applyHtmlTag="false" applyBodyTag="false" showHeader="false" sidebar="false" standardStylesheets="false" title="Container Page">
<html>
    <head>
        <title>HTML5 Container Page</title>
    </head>
    <body>
        <apex:remoteObjects>
            <apex:remoteObjectModel name="Post__c" jsShorthand="Post" fields="Id, Name, Categories__c, Content__c" />
        </apex:remoteObjects>
    
        <!-- react.js  -->
        <div id="body" />
        <!-- For development environment -->
        <script src="http://localhost:8080/bundle.js" />
        <!-- Uncomment and use the below for production to point to final static resource "reactreduxblog"(bundle.js) -->
        <!-- <script src="{!URLFOR($Resource.reactreduxblog)}"/> -->
    </body>
</html>
</apex:page>
```

上面的代码可知，当需要在本地测试时，就把<script src="http://localhost:8080/bundle.js"/>的注释去掉并注释掉<script src="{!URLFOR($Resource.reactreduxblog)}"/>即可。每次本地改动代码后，react server（webpack和express.js）会重编译并生成新的bundle.js，刷新你的salesforce app页面即可看到更新。  

如果你的React应用需要Ajax请求动作，则要使用[Visualforce Remote Objects](https://developer.salesforce.com/docs/atlas.en-us.pages.meta/pages/pages_remote_objects_example_simple.htm)，即上面的```<apex:remoteObjects>...</apex:remoteObjects>```  


未完待续...
