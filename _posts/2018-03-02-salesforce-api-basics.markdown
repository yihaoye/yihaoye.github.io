---
layout: post
title:  "Salesforce API入门基础"
date:   2018-03-02 11:09:08 +1200
categories: salesforce
---
原文链接：https://trailhead.salesforce.com/modules/api_basics

一、Salesforce API概述


二、使用REST API
    学习目标
        * 登录Workbench并使用REST Explorer
        * 使用describe resource
        * 使用REST API创建一个Account
        * 使用REST API执行一次查询

    REST资源及方法
        REST资源是一份信息或动作的抽象，例如单个数据记录，记录集合或查询（query）。REST API中的每个资源都由一个已命名的Uniform Resource Identifier（URI）标识，并可通过标准HTTP方法（HEAD，GET，POST，PATCH，DELETE）进行访问。REST API是基于资源的使用情况，资源的URI以及资源之间的链接。

        你通过使用资源与你的Salesforce org（组织）进行交互。例如，你可以：
            * 检索有关可用的API版本的摘要信息。
            * 获取有关Salesforce对象的详细信息，例如Account，Contact或自定义对象。
            * 执行查询或搜索。
            * 更新或删除记录。
        一个REST请求由四个部分组成：一个资源URI，一个HTTP方法，request headers（HTTP请求头字段）和request body（HTTP请求报文主体）。request headers指定请求的meta data（元数据）。request body可以为请求添加指定数据（比如认证、令牌等等），但它有很多时候可以被省去/省略为空的。