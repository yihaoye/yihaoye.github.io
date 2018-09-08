---
layout: post
title:  "SAML认证工作原理"
date:   2018-02-2 15:19:01 +1200
categories: auth0
---
### 什么是SAML？
Security Assertion Markup Language (SAML)是一个基于XML的框架，用于在服务提供者（Service Provider）和身份提供者（Identity Provider）间提供认证和授权服务。  
Service Provider同意并信任Identity Provider从而对用户进行身份认证。另一方面，Identity Provider生成authentication assertion（认证断言），用来表示用户已被认证通过。  
SAML是标准SSO形式。传递在Service Provider和dentity Provider间的认证信息包含在已数字签名（加密）的XML文件里。SAML是一种无缝认证复杂SSO的实现方式，通常用于企业与业务间。SAML无需键入密码等credentials。  
  
使用SAML好处包括：标准化、提升使用体验、更安全、目录服务登陆易实现-无需用户在目录服务内的信息以及烦恼目录间信息的同步问题、减少Service Provider的成本-Service Provider（你的应用）无需存储维护用户账户信息，Identity Provider将承担这些任务。  
  
### SAML认证如何工作的？
以下例子讲述SAML认证流程，整个流程里通常包括一个信任建立流程和认证流程。  
例子里的Identity Provider是Auth0，Service Provider是Zagadat（企业HR系统）  
Identity Provider可以是任何其他Identity Provider。  
  
当用户尝试通过SAML登陆访问Zagadat时，他会:  
1. 用户通过浏览器尝试登陆Zagadat
2. Zagadat生成一个SAML请求（一个XML）
3. 用户被重定向到一个SSO地址，Auth0
4. Auth0解析SAML请求，对用户进行认证（用户需要选一种注册或登陆Auth0，已经登陆Auth0的话可跳过这一步），然后生成一条SAML回应（一个XML）
5. Auth0加密这条SAML回应并发送至用户浏览器
6. 浏览器发送该SAML回应至Zagadat
7. Zagadat校验SAML回应，校验成功后，用户登陆Zagadat并获得访问该系统内的资源权限
