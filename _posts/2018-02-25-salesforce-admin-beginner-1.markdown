---
layout: post
title:  "Salesforce Admin入门1"
date:   2018-02-25 17:42:33 +1200
categories: salesforce
---
原文链接：https://trailhead.salesforce.com/trails/force_com_admin_beginner/modules/starting_force_com

Salesforce平台入门基础

一、Salesforce平台初步
    备注：Salesforce有两个PC端的UI界面：Lightning Experience（新）和Salesforce Classic（旧）。本教程围绕新界面讲解。

    学习目标
        * 定义Salesforce平台
        * 描述DreamHouse场景
        * 创建一个Trailhead游乐场
        * 解释声明式开发和程序式开发之间的区别

    快速介绍Salesforce
        你可能认为Salesforce只是一个CRM。它存储你的客户数据，为你提供培养潜在客户的流程，并提供与你合作的人员进行协作的方法。它可以完成所有这些事情。但如果说Salesforce“只是一个CRM”，就像说房子只是一个厨房，Salesforce除CRM之外还有很多功能。
        Salesforce带有许多标准功能和可用于运行业务的开箱即用的产品和功能。以下是多数企业使用Salesforce的一些常见需求以及我们为支持这些需求、活动而提供的解决方案。

        你需要：推销给潜在客户和客户；所以Salesforce提供：Leads和Opportunities来管理销售工作。
        你需要：提供售后服务；所以Salesforce提供：提供Cases和Communities以帮助客户raise ticket并得到客服解答解决问题。
        你需要：随时随地工作；所以Salesforce提供：可自定义的Salesforce移动应用程序。
        你需要：与同事，合作伙伴和客户协作；所以Salesforce提供：Chatter和Communities来在你公司内架起沟通桥梁。
        你需要：向观众推销；所以Salesforce提供：Marketing Cloud来管理您的客户旅程。

        以上只是基础样板架构和功能，Salesforce强大之处在于你可以自定义和构建出满足你公司需求的独有解决方案、系统平台，当你有一个独有的商业应用程序时，你将更容易成功。

    Salesforce使用案例
        你会看到很多以不同方式使用Salesforce的公司和例子。以下是一些例子：
            * Cloud Kicks - 这家定制运动鞋公司正在制鞋行业引起轰动。他们使用Salesforce管理销售并使其复杂的订单创建和交货过程规范化流程化。
            * Ursa Major Solar - 在可再生能源的尖端，Ursa Major Solar需要不会回避开创性技术商业软件。他们使用Salesforce管理全国的销售和客户服务。
            * Get Cloudy Consulting - 作为业内最好的云咨询公司之一，Get Cloudy懂得CRM。他们使用Salesforce来管理现有和潜在的客户，他们一直在不断探索如何用Salesforce提供的服务来进行创新。
            * DreamHouse Realty - 以其新颖的房地产方式而闻名，DreamHouse使用Salesforce连接员工并提高住宅销售效率。

        我们将用DreamHouse的Salesforce使用案例来解释Salesforce平台的一些基本术语，概念和功能。
            Michelle是DreamHouse的主要房地产经纪人。她通过DreamHouse的网络和移动应用程序发现许多潜在的购房者。客户通过DreamHouse的应用程序浏览可用的房屋记录他们感兴趣的物业列表。他们还可以直接与Michelle或其他经纪人直接联系以获得详细信息。
            D'Angelo是DreamHouse的Salesforce管理员。他正在Salesforce平台上构建一套自定义功能来支持Michelle及其团队。Michelle可以使用此自定义功能来编辑和查看有关她正在推销的物业信息，并跟进她的潜在买家。
            请记住，Salesforce具有跟踪常见Sales Object（销售对象）（如Accounts，Contacts和Leads）的标准功能。但DreamHouse是一家房地产公司，因此它具有特定于其行业和商业模式的需求。在本单元中，我们与D'Angelo一起研究如何使用Salesforce平台以满足这些需求。

        先了解一些术语
            也许你在上面最后一段注意到一个奇怪的词：Object（对象）。 Object是你在了解Salesforce时学到的许多重要术语之一。
            首先，了解Salesforce背后的数据库非常重要。当我们谈论数据库时，可以想象成一个巨大的电子表格。将信息放入Salesforce时，它会存储在数据库中，以便稍后再次访问它。它以非常特定的方式存储，因此你始终可以访问所需的信息。
            让我们来看看DreamHouse应用中的一个页面，以定义它的一些重要元素以及它们与数据库的关系。
                * App: Salesforce中的App是支持业务流程的一组对象，字段和其他功能。你可以查看你正在使用的App，并使用App Launcher（https://res.cloudinary.com/hy4kyit2a/image/upload/doc/trailhead/en-usac36d6d74354107658cfcef0d828d06f.png）在切换App。
                * Object：Object是Salesforce数据库中用于存储特定类型信息的table（表）。有像Account和Contact这样的标准对象以及你在插图中看到的Property（物业、房产）等自定义Object（对象）。
                * Record：Record（记录）是Object（对象）数据库table（表）中的行。Record是与Object关联的实际数据。在这里，“211 Charles Street”的Property（物业）是一个Record。
                * Field：Field（字段）是Object（对象）数据库table（表）中的列。标准和自定义对象都有字段。在我们的Property（物业）对象中，我们有像Address和Price这样的字段。
            Org是组织的简称，它指的是Salesforce的具体实例。这里的DreamHouse就是一个实例、Org。你的公司可以有一个或多个Org。