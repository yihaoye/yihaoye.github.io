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

    描述Account对象
        现在将使用Workbench进行一些API调用作为练习。Workbench是一套用于通过API与你的Salesforce org（组织）进行交互的工具。你也可以使用任何其他的基于HTTP协议发送REST请求的工具（例如，check out cURL或Postman）。由于Workbench为Salesforce API提供了一个友好的框架，因此在你准备实现你的Salesforce org（组织）的完整系统前，这是最好的方式/工具。
        
        练习：
            登录Workbench。对于这个模块，我们只使用Workbench的许多工具之一，即REST Explorer。在顶部菜单中，选择utilities | REST Explorer。
            你可以从REST explorer调用REST API，就像从任何其他HTTP协议工具调用REST API一样。输入框中的文本表示资源URI，为了方便起见，显示的URI中已省略了顶级域名。例如，预填充到URI输入框中的资源的完整URI是https://foo.my.salesforce.com/services/data/v36.0（但这里只显示/services/data/v36.0）
            URI上方的单选按钮代表标准的HTTP方法。要进行API调用，请输入目标资源的URI，选择适当的HTTP方法，根据需要添加headers（HTTP请求头字段），然后单击执行。
            现在试试SObject描述资源。此资源与GET方法结合使用时，会返回有关对象及其字段的元数据。现在将尝试描述Account对象。将URI输入框中的现有文本替换为/services/data/vXX.0/sobjects/account/describe，其中XX应替换为你正在使用的API版本。
                /services/data - 表示发送的是REST API请求
                /v36.0 - API版本号
                /sobjects - 指定我们正在访问sObject分组下的资源
                /account - 被操作的sObject; 这里被操作的是Account对象
                /describe - 操作动作;在这里是“描述”请求
            执行结果是Account元数据出现在屏幕上（Workbench会自动格式化了响应数据）。若要查看原始JSON响应，请单击Show Raw Response。
            Account元数据以JSON形式显示在一些HTTP响应头字段下方。由于REST API支持JSON和XML，因此可以更改请求头字段以指定XML格式的响应。在HTTP方法旁边，单击Headers，对于Accept的header值，将“application/json”替换为“application/xml”，点击执行，则这次返回原始的XML响应结果。

    创建一个Account
            现在使用SObject资源和POST方法创建一个Account。在URI输入框中，将现有文本替换为/services/data/vXX.0/sobjects/account。选择POST。这时出现了请求报文主体输入框，在这里可以为新Account指定其相关字段的值。
            请求报文主体例子：
            {
                "Name" : "NewAccount1",
                "ShippingCity" : "San Francisco"
            }
            点击执行后如果返回“success:true”，则Account已被成功创建，返回的ID即Account的ID。（否则可以展开errors文件夹以查询反馈的错误信息）

    执行查询
            现在假设你或其他用户创建了数百个Account，而你想查找航运城市是旧金山的所有Account的Name。你可以使用查询资源执行SOQL查询，并根据需要准确记录。
            URI输入框文本：/services/data/vXX.0/query/?q=SELECT+Name+From+Account+WHERE+ShippingCity='San+Francisco'。（我们用查询字符串中的+字符替换了空格，以正确编码URI，更多知识请链接阅读HTML URL编码）选择GET方法，然后单击执行。
            展开records文件夹。可以看到刚刚创建的Account - NewAccount1。点击该Account的文件夹，再点击attributes，url旁边是该Account的资源URI。

    Salesforce提供了不同语言的SDK，这样你调用API时更方便易用，比如Nforce（Node.js）和Restforce（Ruby）。
    Nforce用例：
        var nforce = require('nforce');
        // create the connection with the Salesforce connected app
        var org = nforce.createConnection({
            clientId: process.env.CLIENT_ID,
            clientSecret: process.env.CLIENT_SECRET,
            redirectUri: process.env.CALLBACK_URL,
            mode: 'single'
        });
        // authenticate and return OAuth token
        org.authenticate({
            username: process.env.USERNAME,
            password: process.env.PASSWORD+process.env.SECURITY_TOKEN
        }, function(err, resp){
            if (!err) {
                console.log('Successfully logged in! Cached Token: ' + org.oauth.access_token);
                // execute the query
                org.query({ query: 'select id, name from account limit 5' }, function(err, resp){
                    if(!err && resp.records) {
                        // output the account names
                        for (i=0; i<resp.records.length;i++) {
                            console.log(resp.records[i].get('name'));
                        }
                    }
                });
            }
            if (err) console.log(err);
        });
    Restforce用例：
        require 'restforce'
        // create the connection with the Salesforce connected app
        client = Restforce.new :username => ENV['USERNAME'],
            :password       => ENV['PASSWORD'],
            :security_token => ENV['SECURITY_TOKEN'],
            :client_id      => ENV['CLIENT_ID'],
            :client_secret  => ENV['CLIENT_SECRET']
        // execute the query
        accounts = client.query("select id, name from account limit 5")
        // output the account names
        accounts.each do |account|
            p account.Name
        end