---
layout: post
title:  "Auth0 Hosted Pages"
date:   2018-02-27 11:45:22 +1200
categories: auth0
---
原文链接：https://auth0.com/docs/hosted-pages

使用Auth0进行SSO登陆有两种方式：
    1. Auth0 Lock Widget（也叫Universal Login）（插入iframe，托管在Auth0的服务器）
    2. 自定义页面（Custom Login Form / Custom UI）（非iframe，不托管在Auth0的服务器）并在后端使用Auth0的SDK或直接调用Auth0的API（Authentication API）
    Auth0 Hosted Page就是第一种情况。

    Auth0可以Host的Page有四个：Login，Password Reset，Guardian Multifactor，Error Page
    使用Auth0的好处是更安全更方便，因为该登陆页面是iframe，托管在Auth0的服务器上，比如更容易无缝接入CSRF保护，比如防止第三方冒充或sessions劫持。




注意cdn的lock.js和cdn的auth0.js是两码事。（Auth0.js SDK和cdn的auth0.js是一样的）

Auth0有两套API：
    1. Authentication API：所有关于自定义的用户认证、登录登出、注册等后端操作。
    2. Management API：几乎所有Auth0 Dashboard上的操作（比如配置等等）都可以用此API完成。

题外话：应该何时选择使用Auth0 Lock Widget何时选择结合Auth0 API使用自定义页面？
    Auth0 Lock Widget：当你想方便或允许多种登陆方式（第三方认证登陆、账号密码等等）（第三方认证登陆包括企业网站或社交网站），你想更安全
    自定义并使用API：你有多个数据库或Active Directory Connections（但是此方式需要实现Cross-origin Authentication，即处理不同域名间发送用户credentials要面对的安全问题比如网络钓鱼等等，Cross-origin Authentication有一定限制所以要注意）（不过Cross-origin authentication仅限于针对directory的账号密码登陆方式，其他如OpenID Connect或SAML等不需要）