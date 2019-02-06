---
layout: post
title:  "Salesforce常见问题"
date:   2018-02-27 15:31:20 +1200
categories: crm
tags: salesforce
---
## 常见问题：  

一、当我创建了Object后，怎么去查看该Object的Record？  
答：当你创建了一个新的自定义Object后，你可以在Salesforce的setup页面左侧菜单栏中点击User Interface然后点击Tabs，在Tabs设置页面的Custom Object Tabs栏中点击New，然后设置Object的Tab的访问权限以及哪个App显示该Tab。保存设置完成后进入相关App，可以在Tabs栏中看到该Tab（如果看不到请点击右侧的“More”下拉按钮），点击Tab则即可翻看该Object的所有、最近Records，或手动创建新的Record。  
<!-- more -->

二、查看我的Salesforce账号client_id或client_secret？  
答：这是一个非常常见和恼人的问题。目前似乎Salesforce Light中不能查看，所以你需要先切换去Salesforce Classic，然后根据以下这个链接（https://developer.salesforce.com/forums/?id=906F0000000AfcgIAC）里的工作人员提示去获得指定Connected App（如果你之前未创建Connected App则需要先在Salesforce Classic下新建一个Connected App，另外注意IP限制等设置）的customer key（即client_id）和customer secret（即client_secret）信息，默认情况下customer secret（即client_secret）是藏起来的，你需要点击"click to reveal"的按钮链接才显示。  
另外你也可能会需要一个security token（比如在IP限制之外的第三方访问API时「1」），这需要你去reset（这个在Light里就可以做的，首次创建或重设都是执行该reset），该token不会在你的salesforce org的portal或任何控制面板中显示，它只会发送至org的主联系人/管理员的联系邮箱，在这里你需要注意有些时候对salesforce的一些敏感信息（比如主联系人/管理员的密码改动）改动会触发该token的自动reset。更多请参考https://success.salesforce.com/answers?id=90630000000glADAAY  
  
  
「1」: When you access Salesforce from an IP address that isn’t trusted for your company, and you use a desktop client or the API, you need a security token to log in. What’s a security token? It’s a case-sensitive alphanumeric code that’s tied to your password. Whenever your password is reset, your security token is also reset.  
