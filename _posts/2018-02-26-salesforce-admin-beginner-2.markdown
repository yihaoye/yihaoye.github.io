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

    了解Field（字段）
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
        字段类型：Custom
            在标准或自定义对象上创建的自定义字段称为Custom字段。
            例子：比如你可以在Contact对象上创建自定义字段以存储Contact的生日。

        Identity，System和Name字段是Salesforce中每个对象的标准字段。每个标准对象还附带一组预制、内置的标准字段。你可以通过添加自定义字段来自定义标准对象，也可以将自定义字段添加到自定义对象中。
        每个字段都有一个数据类型。数据类型表示字段存储的是什么类型的信息。Salesforce支持许多不同的数据类型，一下几个比较有趣：
            * Checkbox - 用来存储布尔值（true/false）
            * Date or DateTime - 用来存储日期或日期加具体时间，比如生日或销售里程碑
            * Formula - 存储可以自动计算的你输入的方程式。比如D'Angelo可以输入一个方程式以自动计算出一个房产经纪人在某次房屋销售后获得的佣金
        还有很多其他类型的字段，他们都是很常见的数据类型，一看就明白。

    自定义责任
        看起来一切都很容易但实际要考虑很多复杂的问题。在开始自定义自己的Org时，请记住以下一些指导。
            仔细考虑名字 - 一旦你开始创建一堆对象，可能会给他们“懒惰”的名字。例如，如果D'Angelo创建了另一个自定义对象来跟踪共管公寓，他可能会试图将其命名为“Property2”而不是“共管公寓”。为了不造成混淆，请给你的对象和字段以独特、清晰、描述性的名称。
            帮助你的用户 - 即使仔细命名，你的用户可能还是不清楚特定对象或字段的用途。所以需要详细的自定义对象和字段的说明。对于专业或复杂的术语，请使用help text以提供更多详细信息。
            必填字段 - 有时候，当用户在某个对象上创建一条记录时，你需要强制用户填写某一个字段。比如每个物业都需要一个价格。设置好必填字段以避免不完整的数据。



    操作练习
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

        创建一个自定义字段
            以下是添加一些自定义字段的步骤
                setup页面，进入Object Manager | Property（或点击某个Object）。
                在边栏中，点击Fields & Relationships。你会发现那里已经有一些字段，比如Name字段和我们之前谈到的一些系统字段。
                点击右上角的New。
                选择数据类型（比如Currency），点击Next。
                填写Field Label：“Price”、Description：“The listed sale price of the home”。
                选中Required框。
                点击下一步两次，然后保存。
            你会在Property字段列表中看到新的Price字段。在Field Name列中会显示“Price__c”。 “__c”暗示该字段是自定义字段。

        创建一个记录
            让我们创建一个财产记录
                进入App页面，选择Sales应用。
                单击导航栏中的“Properties”选项卡。如果你没有看到它，请查看最右的“More”下拉菜单。
                点击顶部的New。
                输入Property的Name和Price，然后单击保存。


二、创建对象关系（Object Relationships）

    学习目标
        * 定义不同类型的“对象关系”及其应用案例
        * 创建或修改lookup（查找）关系
        * 创建或修改master-detail（主从）关系

    什么是对象关系？
        对象关系是将两个对象关联在一起的特殊字段类型。
        举例：一个像Account这样的标准对象。如果销售代表打开一个Account，他们可能已经与该Account的几个Contact（联系人，比如高管或IT经理）谈过话或已经建立了联系，并将这些Contact（联系人）的信息存储在Salesforce中。
        因此，在Account对象和Contact对象之间应该存在某种关系。且当你查看Salesforce中的Account记录（records）时，可以看到“相关”选项卡上有Contact（联系人）部分。你还可以看到有一个按钮，可让你快速将新的Contact添加到该Account。

        Account与Contact关系是Salesforce中标准关系的一个示例。就像自定义对象和自定义字段一样，你也可以建立自定义关系。

    对象关系的世界
        主要有两种对象关系类型：lookup（查找）和master-detail（主从）。

        查找关系
        在上面的Account与Contact关系示例中，两个对象之间的关系是查找关系。查找关系基本上将两个对象链接在一起，以便你可以从另一个对象上的“相关”项目中“查找”一个对象。
        查找关系可以是一对一或一对多。Account到Contact关系是一对多的，因为一个Account可以有许多相关的Contact。对于DreamHouse场景，你可以在Property对象和Home Seller对象之间创建一对一的关系。

        主从关系
        相较于查找关系的随意性，主从关系更加紧密。在这种关系中，一个对象是主人，另一个是细节。主对象控制着细节对象的某些行为，比如谁可以查看细节的数据。例如，假设一个Property（房产）的房主不希望他们的房子再在市场上挂牌，DreamHouse不希望保留任何对该Property（房产）的Offer（报价）。通过Property和Offer之间的主从关系，你可以从系统中一次性删除该Property对象及其所有关联的Offer记录（关联删除）。