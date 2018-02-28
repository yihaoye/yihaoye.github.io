---
layout: post
title:  "Auth0 Hosted Pages"
date:   2018-02-27 11:45:22 +1200
categories: auth0
---
原文链接：https://auth0.com/docs/hosted-pages

使用Auth0以助你认证用户有两种方式：
    1. Universal Login（包含三种：Lock Widget、Lock Passwordless Widget、Custom Login Form。前两种使用lock.js，最后一个使用auth0.js）（用户进行登录或注册操作时会redirect到托管在Auth0的服务器的Hosted Page页面，完成后再被redirect回你的App的网址）
    2. 自定义页面（不托管在Auth0的服务器而是你的前端代码）你的App代码使用Lock库或Auth0的SDK或直接调用Auth0的API（Authentication API）。（在自己的代码里使用Lock库就类似Hosted Page里的实例代码一样，比如lock.show()，弹出来的登录框造型一样）
    Auth0 Hosted Page就是第一种情况。
    注意库Lock和库Auth0 SDK是两码事。（Lock包括CDN的lock.js、Lock for iOS、Lock for Android，只提供一些常用标准Authentication操作和UI）（Auth0 SDK包括CDN或npm的auth0.js、Auth0.Swift、Auth0.Android、Node-Auth0 etc，Auth0 SDK不包括UI但包括所有Authentication操作）（Auth0 SDK让开发者更方便直观的实现Authentication API提供的所有功能并提供一些额外的功能或便利，Lock和Auth0 SDK都是基于Authentication API的）

    Auth0可以Host的Page有四种：Login、Password Reset、Guardian Multifactor、Error Page，分别处理不同的业务需求。
    使用Auth0 Hosted Page的好处是更安全更方便，因为该登陆页面是托管在Auth0的服务器上的，因此更容易无缝接入CSRF保护，比如防止第三方冒充或sessions劫持。






Auth0有两套API：
    1. Authentication API：所有关于自定义的用户认证、登录登出、注册等后端操作。
    2. Management API：几乎所有Auth0 Dashboard上的操作（比如配置等等）都可以用此API完成。

题外话：应该何时选择使用Auth0 Universal Login（即Hosted Page）何时选择结合Auth0 API使用自定义页面？
    Universal Login：当你想方便或允许多种登陆方式（第三方认证登陆、账号密码等等）（第三方认证登陆包括企业网站或社交网站），你想更安全
    自定义页面并使用SDK或API：你有多个数据库或Active Directory Connections（但是此方式需要实现Cross-origin Authentication，即处理不同域名间发送用户credentials要面对的安全问题比如网络钓鱼等等，Cross-origin Authentication有一定限制所以要注意）（不过Cross-origin authentication仅限于针对directory的账号密码登陆方式，其他如OpenID Connect或SAML等不需要）