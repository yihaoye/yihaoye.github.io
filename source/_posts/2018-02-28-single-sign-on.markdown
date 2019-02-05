---
layout: post
title:  "Single Sign On"
date:   2018-02-28 10:45:32 +1200
categories: authentication
---
本文不止讨论Single Sign On（简称SSO），也讨论其他一些容易混淆的登录机制概念。  
  
### SSO的例子：  
1. 一个谷歌账号可以登录所有谷歌应用（如Gmail，Google Drive，Youtube等等）
2. 一个微软Azure Active Directory账号可以登录多个微软应用（如Azure，Office365等等）
  
### 一个容易与SSO混淆的概念 -- 第三方认证登录:  
你可能熟悉这样的场景，你尝试注册Instagram，但你不想手动填写邮箱地址、密码、账号名等等信息以进行传统的注册机制（很烦很啰嗦），此时Instagram提供使用你的Facebook账号认证并创建Instagram账号。  
所以你只需要点击“Facebook认证”，浏览器就会把你转到Facebook网址下的授权页面（如果你在此浏览器未登录Facebook则你需要先登录Facebook）点击“同意授权”，然后浏览器又会回到Instagram网址并显示成功注册并登录。  
此时你也可以发现Instagram已获得了一些你没有在Instagram输入过的个人信息（如头像、邮箱、联系方式、名字等等），当然这些是Facebook给予的因为你已经授权让Instagram从Facebook得到这些信息。（PS：Facebook的这些信息当然不是凭空来的，是你以前注册Facebook时输入或注册Facebook时也使用了第三方认证登录，所以如果你没有Facebook账号是不能执行基于Facebook的认证登录）  
  
一般现在的第三方认证登录是基于OAuth2.0的。  
  
https://www.cnblogs.com/ywlaker/p/6113927.html  
SSO和第三方认证登录区别在于SSO看起来像是使用同一个用户credential数据库并使用同一个cookie的，而第三方认证登录则是简易地复制粘帖似地完成了一次之前的注册过程。  