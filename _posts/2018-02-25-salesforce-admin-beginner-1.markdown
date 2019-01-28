---
layout: post
title:  "Salesforce Admin入门1"
date:   2018-02-25 17:42:33 +1200
categories: salesforce
---
原文链接：https://trailhead.salesforce.com/trails/force_com_admin_beginner/modules/starting_force_com  
  
## Salesforce平台入门基础  

## 一、Salesforce平台初步
备注：Salesforce有两个PC端的UI界面：Lightning Experience（新）和Salesforce Classic（旧）。本教程围绕新界面讲解。  

### 学习目标
* 定义Salesforce平台  
* 描述DreamHouse场景  
* 创建一个Trailhead游乐场  
* 解释声明式开发和程序式开发之间的区别  

### 快速介绍Salesforce
你可能认为Salesforce只是一个CRM。它存储你的客户数据，为你提供培养潜在客户的流程，并提供与你合作的人员进行协作的方法。它可以完成所有这些事情。但如果说Salesforce“只是一个CRM”，就像说房子只是一个厨房，Salesforce除CRM之外还有很多功能。
Salesforce带有许多标准功能和可用于运行业务的开箱即用的产品和功能。以下是多数企业使用Salesforce的一些常见需求以及我们为支持这些需求、活动而提供的解决方案。  
  
你需要：推销给潜在客户和客户；所以Salesforce提供：Leads和Opportunities来管理销售工作。  
你需要：提供售后服务；所以Salesforce提供：提供Cases和Communities以帮助客户raise ticket并得到客服解答解决问题。  
你需要：随时随地工作；所以Salesforce提供：可自定义的Salesforce移动应用程序。  
你需要：与同事，合作伙伴和客户协作；所以Salesforce提供：Chatter和Communities来在你公司内架起沟通桥梁。  
你需要：向观众推销；所以Salesforce提供：Marketing Cloud来管理您的客户旅程。  
  
以上只是基础样板架构和功能，Salesforce强大之处在于你可以自定义和构建出满足你公司需求的独有解决方案、系统平台，当你有一个独有的商业应用程序时，你将更容易成功。  

### Salesforce使用案例
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
![](https://res.cloudinary.com/hy4kyit2a/image/upload/f_auto,q_auto/doc/trailhead/en-uscc692c3f83b52641f81d56b626616a0b.png)  
* App: Salesforce中的App是支持业务流程的一组对象，字段和其他功能。你可以查看你正在使用的App，并使用App Launcher(![](https://res.cloudinary.com/hy4kyit2a/image/upload/doc/trailhead/en-usac36d6d74354107658cfcef0d828d06f.png))在切换App。  
* Object：Object是Salesforce数据库中用于存储特定类型信息的table（表）。有像Account和Contact这样的标准对象以及你在插图中看到的Property（物业、房产）等自定义Object（对象）。  
* Record：Record（记录）是Object（对象）数据库table（表）中的行。Record是与Object关联的实际数据。在这里，“211 Charles Street”的Property（物业）是一个Record。  
* Field：Field（字段）是Object（对象）数据库table（表）中的列。标准和自定义对象都有字段。在我们的Property（物业）对象中，我们有像Address和Price这样的字段。  
Org是组织的简称，它指的是Salesforce的具体实例。这里的DreamHouse就是一个实例、Org。你的公司可以有一个或多个Org。  
  
### 你的第一个Trailhead Playground
Trailhead Playground（TP）组织是一个在正式在工作中使用Salesforce前练习Salesforce的安全环境。TP配备了测试应用程序开发记录所需的所有标准应用程序构建和定制工具。你可能听说过Developer版（DE）组织，TP就是一种特殊类型的DE。  
当你注册Trailhead时，我们已自动为你创建一个TP。因此如果你已经登录，请滚动至该页面底部并点击“Launch”以打开你的TP。  
TP组织是免费的，一次最多可以有10个组织。如果你想要管理您的TP，则可以从Trailhead配置文件查看并删除它们。尝试启动你的TP，以开始实操。  
  
### 自定义Salesforce平台
你已经知道你可以使用Salesforce平台来开发特用于你业务的自定义对象和功能。你可以在不写一行代码的情况下完成大部分这类开发工作。  
无代码开发被称为声明式开发。通过声明式开发，你可以使用表单和拖放工具来执行强大的自定义任务。该平台还提供程序化开发，该开发使用Lightning组件，Apex代码和Visualforce页面等。但是如果你不是程序员，你仍然可以在平台上构建一些令人惊叹的东西。  
  
## 二、用户案例





## 三、了解Salesforce架构

### 学习目标
* 了解Salesforce架构相关的关键术语
* Salesforce 云隐私与信任
* Salesforce API用例
  
### 什么是Salesforce架构？
你知道可以使用Salesforce为你的客户，员工和合作伙伴提供高度定制的产品、工作体验，可以在不编写太多（或任何）代码的情况下快速实现这一点。这一切都得益于Salesforce的系统架构。  
![](https://res.cloudinary.com/hy4kyit2a/image/upload/f_auto,q_auto/doc/trailhead/en-usa9185345b101cb48cf45a802bc266bf6.png)  

-----
* Salesforce是一家云计算公司。 我们提供的一切都在于可靠的多租户云。
* Salesforce Platform是我们服务的基础。 它由元数据提供支持，由不同的部分组成，如数据服务，人工智能和用于开发的强大API。
* 我们所有的应用程序都位于平台之上。 我们的预建产品如Sales Cloud和Marketing Cloud，以及您使用该平台构建的应用程序，具有一致，强大的功能。
* 一切都融为一体。 我们的平台技术，如爱因斯坦预测智能和Lightning开发框架，内置于我们提供的一切和您构建的一切。
这里有一些对您来说非常重要的术语：信任，多租户，元数据和API。
  
### 为何信任云？  
在Salesforce，信任是我们的首要任务。 您不仅要将敏感数据保存在组织中，还要构建对您公司在我们的平台上取得成功至关重要的功能。 我们保证您的数据和功能安全的责任不是我们轻视的，这就是我们对服务始终保持透明的原因。  
我们的信任站点trust.salesforce.com是一个重要的资源。 您可以使用它来查看性能数据并获取有关我们如何保护数据的更多信息。 它还向您显示我们将执行的任何计划维护，这可能会影响您对Salesforce的访问。  
  
### 共享关注多租户云
到目前为止，我们已经谈了很多关于房屋的事情。 但实际上，Salesforce更像是一座公寓楼。 您的公司在云中拥有自己的空间，但您拥有各种邻居，从妈妈和流行商店到跨国公司。  
这个想法是多租户的。 多租户是让你在晚宴上听起来很聪明的一个好词，但实际上它意味着你要分享资源。 Salesforce为多租户云中的所有客户提供核心服务。 无论您的业务规模如何，您都可以访问相同的计算能力，数据存储和核心功能。  
信任和多租户齐头并进。 尽管您与其他公司共享空间，但您可以信任Salesforce以确保您的数据安全。 您还可以相信，您可以通过一年三次自动无缝升级获得最新，最强大的功能。 由于Salesforce是一项云服务，因此您无需安装新功能或担心硬件问题。 由于多租户，所有这一切都是可能的。  

### 元数据的魔力
简而言之，元数据是关于数据的数据。当我们说有关数据的数据时，我们真的在谈论Salesforce org的结构。  
让我们考虑像Property这样的对象。 当我们在DreamHouse的朋友使用Salesforce时，他们会输入和查看有关属性的数据。 例如，一处房产可以位于波士顿，价格为500,000美元，并有3间卧室。  
现在，想象一下你删除了所有特定数据。 你还剩下什么？ 您将获得Property对象及其所有字段，例如地址，价格和卧室数量。 您还可以拥有页面布局，安全设置以及您所做的任何其他自定义。  
您组织中的所有这些标准和自定义配置，功能和代码都是元数据。 您可以在平台上快速移动的部分原因是Salesforce知道如何在创建元数据后立即存储和提供元数据。  

### All About That API
从根本上说，API允许不同的软件相互连接并交换信息。
如果这听起来有点抽象，请快速浏览一下您正在使用的计算机。您可以找到一系列支持不同类型连接的各种形状和大小的端口。这些就像API的硬件版本。您不必知道USB端口的工作原理。您需要了解的是，当您将手机插入USB端口时，它会将信息传递给您的计算机。
API类似。在不知道细节的情况下，您可以将应用程序与其他应用程序或软件系统连接底层技术负责处理信息在整个系统中的传递方式。
那么这与Salesforce有什么关系呢？
早些时候，我们谈到了数据库。添加自定义对象或字段时，平台会自动创建一个API名称，该名称用作组织与数据库之间的访问点。 Salesforce使用该API名称来检索您要查找的元数据和数据。
例如，我们可以在一堆地方使用联系人的姓名字段，例如Salesforce移动应用程序，自定义页面甚至电子邮件模板。由于API名称，这一切都是可能的。
![](https://res.cloudinary.com/hy4kyit2a/image/upload/f_auto,q_auto/doc/trailhead/en-us4f0900e54e0dd0cca78bfd71956dc715.png)
API的核心功能是所有数据和元数据都支持API。 这可能现在看起来不是什么大问题，但API为Salesforce提供了极大的灵活性。 它可以让您超越商业软件的正常理念，为您的公司构建独特而富有创意的解决方案。 观看此视频，了解您可以走多远的示例。
Every time you use Salesforce, whether you’re using standard functionality or building a custom app, you’re interacting with the API.



## 导航设置（了解Setup页面）

### 学习目标
* 找到Setup页面并了解其关键选项卡
* 确定用于自定义组织的重要菜单
* 使用“快速查找”可访问菜单项

### 设置：您的新工作之家
之前，我们曾提到您在Salesforce管理员期间会花费大量时间在安装程序中。 我们不是在开玩笑。 安装程序是您定制，配置和支持组织的一站式服务。
由于您可以在“设置”区域中执行此操作，因此轻松导航它非常重要。 有几种方法可以解决它。 当您了解可用的内容时，您可以更轻松地找到所需的内容。
您可以从Salesforce组织中的任何页面进入安装程序。 从屏幕顶部的齿轮菜单（齿轮图标打开“设置”），单击“设置”。 让我们熟悉一下Setup区域。
![](https://res.cloudinary.com/hy4kyit2a/image/upload/f_auto,q_auto/doc/trailhead/en-us3ec0e902d611a435b5b6fc7fd462bb39.png)

1. 对象管理器：您可以在对象管理器中查看和自定义组织中的标准和自定义对象。
2. 设置菜单：该菜单为您提供了一系列页面的快速链接，使您可以执行从管理用户到修改安全设置等所有操作。
3. 主窗口：我们正在向您显示设置主页，但您可以在此处查看您正在尝试处理的任何内容。
设置菜单是最难以导航的部分，因为您可以访问许多不同的页面。 有两种方法可以到达你想去的地方。 如果您已经知道要查看的位置，请展开相应的菜单并选择所需的页面。 如果您不确定在哪里查看，请使用“快速查找”框进行搜索。 假设您想要管理用户权限集。 如果您碰巧知道权限集位于“管理”下的“用户”菜单中，则只需打开该菜单并单击“权限集”。 否则，请在“快速查找”框中输入“权限集”。

### 使用设置菜单获得舒适感
“设置”菜单中有三个主要类别：“管理”，“平台工具”和“设置”。我们来看看有什么可用的。
* 管理：管理类别是您管理用户和数据的位置。您可以执行添加用户，更改权限，导入和导出数据以及创建电子邮件模板等操作。
* 平台工具：您可以在平台工具中完成大部分自定义。您可以查看和管理数据模型，创建应用程序，修改用户界面以及为用户部署新功能。如果您决定尝试编程开发，那么Platform Tools也是您管理代码的地方。
* 设置：最后，您可以使用“设置”管理公司信息和组织安全性。您可以执行诸如添加营业时间，更改区域设置以及查看组织历史记录等操作。

当然，这些只是您可以在“设置”菜单中访问的部分页面。为了让您从正确的方向开始，这里列出了我们要了解的五大安装页面。

##＃Item为什么它是必须看到的
1公司信息
您的组织一览无余
找到您的组织ID
查看您的许可信息
监控数据和文件使用等重要限制
2个用户
重置密码
创建新用户并停用或冻结现有用户
查看有关您用户的信息
3简介
管理谁可以查看用户个人资料的内容
创建定制配置文件
4查看设置审计跟踪
在您的组织中查看6个月的更改历史记录
找出谁做出了改变，何时做出改变
解决组织配置问题的工具
5登录历史
查看组织的6个月登录历史记录
查看日期，时间，用户，IP地址和更多登录数据
用于安全跟踪和采用监控

