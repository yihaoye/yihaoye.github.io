---
layout: post
title:  "在Visualforce中嵌入React应用"
date:   2018-06-08 14:05:11 +1200
categories: salesforce
---
原文参考：https://medium.com/@rajaraodv/developing-react-redux-apps-in-salesforce-s-visualforce-3ad7be560d1c
原文参考：https://sfdcnotes.github.io/2016/02/15/salesforce1-platform-guide/
原文参考：https://www.salesforce.com/video/304788/

Salesforce在设计之初时参考当时流行的MVC模式
Model：SObject （salesforce对象，比如Account、Contact等等）
View：Visualforce
Controller：Apex Code

Visualforce是服务器端模版语言，用来自定义用户桌面，其设计参考了当时JSP。而现在服务器端模版语言已经渐渐淘汰，因此是否能在Visualforce上使用React等新的前端框架会是一个有趣的探索。
在进入主题前讲一个题外话，也许是salesforce本身也认识到Visualforce技术已经老旧了，因此salesforce本身也推出了Lightning Components framework这一前端框架作为他们的改进方案。

一个简单Visualforce页面：
<apex:page>
    <html>
        <head></head>
        <body>
            <h1>hello, world</h1>
        </body>
    </html>
</apex:page>

未完待续...