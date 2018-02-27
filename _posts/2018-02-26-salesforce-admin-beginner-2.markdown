---
layout: post
title:  "Salesforce Admin入门2"
date:   2018-02-26 01:19:01 +1200
categories: salesforce
---
原文链接：https://trailhead.salesforce.com/trails/force_com_admin_beginner/modules/data_modeling

Data Modeling（数据模型、建模）

一、自定义与标准对象

    学习目标
        * 描述在Salesforce平台上使用Object（对象）的好处
        * 解释标准对象和自定义对象之间的区别
        * 列出对象可以具有的自定义字段的类型

    对象概述
        DreamHouse是一家房地产公司，为客户提供购买房屋和在线联系房地产经纪人的途径。DreamHouse经纪人使用Salesforce的一些标准功能（如Contact和Lead）来跟进购房者。
        但是在出售房屋时，公司需要数据还有很多。例如，Salesforce不包含跟踪属性的标准方法。DreamHouse如何可以知道有哪些房屋在出售，或者每个房屋的价格？
        公司的Salesforce管理员D'Angelo知道Salesforce平台提供了一个解决方案。我们将与D'Angelo一起工作，看看他正在建造什么。
        从数据模型开始。数据模型如其名，是一套满足业务数据结构（以便实现所有数据间的逻辑和相关性操作）的数据库表。
        如果你不熟悉数据库，请想象成数据存储在电子表格中。例如，D'Angelo可以使用电子表格来追踪所有DreamHouse的属性。列可以存储地址，成本和其他重要属性。行可以存储DreamHouse销售的每个房源的具体信息。数据库表格的设置方式与此类似。
    https://res.cloudinary.com/hy4kyit2a/image/upload/doc/trailhead/en-us8b58a5df5ac9b863c06372b1c16f7daf.png
        但是查看表格中的数据对于人类来说不直观。这就是数据模型的来源。
        在Salesforce中，我们将数据库表视为对象，我们将列视为字段，将行视为记录。因此，我们没有帐户电子表格或表格，而是拥有一个包含字段和一堆相同结构化记录的帐户对象。
        当我们谈论数据模型时，我们是在讨论应用程序中对象和字段的集合。

    了解对象
        Salesforce支持几种不同类型的对象。有标准对象，自定义对象，external objects（外部对象），platform events（平台事件）和BigObjects。本章中，我们主要讲两种最常见的对象类型：标准和自定义。
        标准对象是Salesforce自带的对象。通常的业务对象，如Account，Contact，Lead和Opportunity都是标准对象。
        自定义对象是你创建的对象，用于存储特定于你的公司或行业的信息。对于DreamHouse，D'Angelo希望建立一个自定义Property对象，存储有关其公司销售的房屋的信息。
        对象是你的信息容器，但它们也为你提供特殊功能。例如，当你创建自定义对象时，平台会自动构建用户界面的页面布局等内容。

    创建一个自定义对象
        让我们试试构建一个Property对象，以下是步骤
            点击右上角齿轮图标按钮，点击setup。
            setup页面内点击Object Manager选项卡。
            点击右上角Create | Custom Object。
            在Label输入栏中输入“Property”，Object Name和Record Name会自动填充相同字符串。
            在Plural Label输入栏中输入“Properties”。
            保存此自定义对象后，勾选Launch New Custom Tab Wizard。
            所有默认值不更改，点击保存。
            选择你想要的Tab Style，点击下一步两次，最后保存。
            成功创建了第一个自定义对象！现在来为这个对象添加字段。

    了解领域
        每个标准和自定义对象都有附加的字段。 先熟悉一下不同类型的字段。

        字段类型：Identity
            是为标识每个记录自动生成的15个区分大小写的字符的字段。你可以在URL中找到记录的ID。
            例子：帐户ID看起来像0015000000Gv7qJ。
        字段类型：System
            是只读字段，提供有关记录的系统信息。
            例子：CreatedDate，LastModifiedById和LastModifiedDate。
        字段类型：Name
            所有记录都需要名称，以便你可以区分它们。每次创建新记录时名称会自动递增（无论数据类型是text或auto-numbered）。
            例子：一位Contact的名称可以是Julie Bean。一个Support Case的名称可以是CA-1024。
        
        在标准或自定义对象上创建的自定义字段称为自定义字段。比如你可以在Contact对象上创建自定义字段以存储Contact的生日。