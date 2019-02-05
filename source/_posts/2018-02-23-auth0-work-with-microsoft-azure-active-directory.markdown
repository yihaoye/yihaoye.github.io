---
layout: post
title:  "Auth0应用于Microsoft Azure Active Directory"
date:   2018-02-23 11:39:15 +1200
categories: security
tags: auth0
---
原文链接：https://auth0.com/docs/connections/enterprise/azure-active-directory/v2

零、准备工作：
应用Microsoft Azure AD的两个场景：
    1. 你想让用户通过Azure AD登入你的应用。
    2. 你想让用户通过公司的Azure AD账号登入应用（你想创建这些外部目录作为不同的connections）。

如果你计划让用户通过他们的公司或另外的Microsoft Azure AD账号登入应用，你必须先在微软的Azure官网注册你的应用。（注册是免费的）
    获得Azure AD的两种方式：
    1. 你可以访问https://manage.windowsazure.com并注册Azure。
    2. 如果你已有Office365账号，可以通过Office365直接获得Azure AD账号。（https://portal.office.com/adminportal/home#/homepage打开左上角菜单的Admin centers，点击Azure AD）
    （如果想在你的应用里集成微软Azure AD，你必须基于你自己的微软Azure AD账号）

一、创建新的Azure应用
    登入微软Azure管理界面，点击左侧菜单栏的Azure Active Directory。
    然后在MANAGE下，点击App registrations。
    点击添加按钮（+ ADD）以创建新的应用，然后为其命名，“Application Type”栏里选择Web app/API，“Sign-on URL”栏里输入你的应用的网址。

二、设置权限
    Azure应用创建好后，点击应用的名字打开Setting页面，点击“Required permissions”，然后点击“Windows Azure Active Directory”更改访问级别（access levels）更改你的应用权限从而可以读取directory，在“DELEGATED PERMISSIONS”下勾选“Sign in and read user profile”和“Read directory data”。最后点击保存（SAVE）按钮。
    （如果要启用扩展属性（如扩展配置文件或安全组），则还需要启用以下权限：Application Permissions项: Read directory data，Delegated Permissions项: Access the directory as the signed-in user。）

三、允许外部机构访问（可选项）
    如果你想让外部机构（比如其他的Azure directories）登陆你的应用，你需要启用你的Azure应用里的Multi-Tenant。
    具体步骤是在“setting”点击“Properties”，在下方“Multi-tenanted”点选“Yes”然后保存。

四、创建密匙（key）
    接下来我们需要创建密匙（key）用作Auth0 connection里的“Client Secret”。
    先在“Settings”菜单点击“Keys”。
    输入该key的name并选择Duration（密匙有效时间，不过你也可以选择让其永不过期）。
    点击保存，此时将展示密匙（key）的具体信息，确保在关闭该页面前复制其value值，不然你将需要重新创建一个（之前创建的密匙value以后不会再展示）。该密匙value值将用于设置接下来的“Client Secret”。

五、配置响应地址（Reply URLs）
    接下来你需要确保你的Auth0 callback URL被写进你的Azure应用的“Reply URLs”里。
    导航至Azure Active Directory -> Apps registrations并选择你的Azure应用，然后点击Settings -> Reply URLs并添加进你的Auth0 callback URL（https://{username}.{country}.auth0.com/login/callback）。
    不完成这一步的结果是届时Azure应用的consent page会返回“Bad request” error（该错误页面的页脚中的细小信息可用于查询是哪个Auth0 tenant和callback URL没设置好）。

六、创建Auth0 Connection
    登录你的Auth0 dashboard，并导航Connections > Enterprise。
    点选Microsoft Azure AD，会弹出connection的设置弹窗（Client ID是Azure应用的Application ID，Client Secret是密匙的value值，设置Microsoft Azure AD Domain和Domain Aliases）。

