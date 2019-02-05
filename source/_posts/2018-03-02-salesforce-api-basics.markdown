---
layout: post
title:  "Salesforce API入门基础"
date:   2018-03-02 11:09:08 +1200
categories: salesforce
---
原文链接：https://trailhead.salesforce.com/modules/api_basics

## 一、Salesforce API概述
### 学习目标
* 了解Salesforce开发中API优先策略的好处  
* REST API, SOAP API, Bulk API以及Streaming API的使用场景  
* 了解每种API限制并描述它们如何计算运行  
  
### Salesforce的API优先策略
Salesforce采用API优先策略来让你构建你的Salesforce应用上的features。"API优先"意味着在专注于设计公司的Salesforce应用UI之前为该应用features构建强大的API。这种方法使Salesforce开发人员能够灵活地根据需要操纵数据。  
Salesforce知道其客户和合作伙伴总想有新的方式去扩展Salesforce功能和AppExchange应用程序，也因此提供了用于在平台上开发的综合工具箱，这样使得Salesforce可以在API之上构建UI，以确保它们之间的行动相同协调。  
  
### Salesforce Data APIs
在这里将重点介绍了常用API们：它们是REST API，SOAP API，Bulk API和Streaming API。它们一起组成了Salesforce Data APIs。它们的目的是让你操纵Salesforce数据，而其他API可让你执行自定义页面布局或构建自定义开发工具等功能。你也可以使用其他Salesforce API来操纵Salesforce数据的子集，例如，Analytics REST API侧重于Analytics。但是，这四种API是广泛使用在核心Salesforce数据上的API。  
  
* REST API:  
REST API是基于RESTful原则的简单而强大的Web服务。它通过REST资源和HTTP方法公开各种Salesforce功能。例如，你可以创建，读取，更新和删除（CRUD）记录，搜索或查询数据，检索Object元数据以及访问Org中有关限制的信息。REST API支持XML和JSON。  
由于REST API具有轻量级的请求和响应框架，并且易于使用，因此非常适合编写移动和Web应用程序。  
* SOAP API:  
SOAP API是基于SOAP标准协议的健壮且功能强大的Web服务。它使用Web服务描述语言（WSDL）文件来严格定义通过API访问数据的参数。SOAP API仅支持XML。大部分SOAP API功能也可以通过REST API获得。这取决于哪个标准更好地满足你的需求。  
因为SOAP API使用WSDL文件作为API和使用者之间的协议，所以编写服务器到服务器的集成非常适合。  
* Bulk API（批量API）:  
Bulk API是专门用于一次加载和查询大量数据的RESTful API，"大量"的意思是50,000条或更多记录。Bulk API是异步的，这意味着你可以提交请求并稍后返回结果。处理大量数据时，这种方法是首选方法。Bulk API现版本是2.0。  
Bulk API非常适合执行涉及大量记录的任务，例如首次将数据加载到你的Org中。  
* Streaming API:  
Streaming API是一种专门的API，用于设置每当数据被更改时会触发的通知。它使用发布-订阅或发布/订阅模型，用户可以在其中订阅频道，这些频道将广播某些数据的更改。  
发布/订阅模型通过消除轮询的需要来减少API请求的数量。Streaming API对于编写应用程序非常有用，否则这些应用程序需要频繁轮询API请求以检查数据是否更改。  
  
API访问和身份验证  
访问Salesforce API，你所需要的只是先注册有以下版本中的一个Org：企业版，无限制版，开发人员版，性能版或专业版（带add-on），确保你具有“API启用”权限，并且已准备好开始集成。  
除SOAP API login（）调用外，所有API调用都需要进行身份验证。你可以使用其中一个受支持的OAuth流或使用从SOAP API login（）调用返回的session ID进行身份验证。查看developer guide，了解选择的API以便开始使用。  
  
API限制  
Salesforce会限制每个Org的API调用次数，以确保实例（Instance）的健康状况。这些限制旨在防止流氓脚本攻击服务器，限制不妨碍你的日常工作。但熟悉它们是必要的。  
有两种类型的API限制。并发限制限制了同时运行的长时间调用（20秒或更长时间）的数量。总限制限制了在24小时内的调用数量。  
并发限制因Org类型而异。对于开发者版本的Org，并发限制是一次五个长时间运行的调用。对于Sandbox的Org，限制是25个长时间运行的调用。  
根据你购买的Org版本，license类型、扩展包和总限制会有所不同。例如，Enterprise Edition Org每个Salesforce license可获得1,000个调用，每个Salesforce Light App license可获得200个调用。使用Unlimited Apps Pack，同一个企业版Org可以获得额外的4000个调用。根据Org版本总数限制也受到最低限额和最高限额的限制。  
你有几种方法来检查你的剩余API调用限制，你可以在"System Overview"页面的"API Usage box"框中查看它们，在"Setup"中，在"Quick Find"框中输入"System Overview"，然后选择"System Overview"。你也可以设置通知，在当Org收到超出指定的API调用限制时作出通知，在"Setup"中，在"Quick Find"方框中输入"API Usage Notifications"，然后选择结果中的"API Usage Notifications"。  
在使用REST或SOAP API时，HTTP返回数据里的LimitInfoHeader response header会为你提供有关剩余调用的信息。你还可以访问REST API限制资源，了解组织中各种限制的信息。  
  
什么时候应该使用哪个API？  
根据需求选择正确的API是重要的，以下是最常用的API的一些信息，包括支持的协议，数据格式，通信范例和实用案例。  

API名	                | 协议	                 | 数据格式	              | 通信
---                    | ---                    | ---                   | ---
REST API	           | REST	                | JSON, XML	            | 同步Synchronous
SOAP API	           | SOAP(WSDL)	            | XML	                | 同步Synchronous
Chatter REST API	   | REST	                | JSON, XML	            | 同步Synchronous (photos are processed asynchronously)
Analytics REST API	   | REST	                | JSON, XML	            | 同步Synchronous
Bulk API	           | REST	                | CSV, JSON, XML	    | 异步Asynchronous
Metadata API	       | SOAP(WSDL)	            | XML	                | 异步Asynchronous
Streaming API	       | Bayeux	                | JSON	                | 异步Asynchronous (stream of data)
Apex REST API	       | REST	                | JSON, XML, Custom	    | 同步Synchronous
Apex SOAP API	       | SOAP(WSDL)	            | XML	                | 同步Synchronous
Tooling API	           | REST or SOAP(WSDL)	    | JSON, XML, Custom	    | 同步Synchronous
  
* 何时使用REST API:  
REST API的优点包括易于集成和开发，并且它是用于移动应用程序和Web项目的优秀技术选择以用于与Salesforce进行交互。但是，如果你有多个要处理的记录，请考虑使用Bulk API，该API基于REST原则并针对大量数据集进行了优化。大部分场景下一般使用REST API。  
* 何时使用SOAP API:  
SOAP API也用于与Salesforce进行交互，你可以使用SOAP API创建，检索，更新或删除记录。你还可以使用SOAP API执行搜索等等。  
例如，你可以使用SOAP API将Salesforce与你的Org的ERP和财务系统集成。你还可以向公司portal提供实时销售和支持信息，并使用客户信息填充关键业务系统。  
* 何时使用Chatter REST API:  
使用Chatter REST API显示Salesforce数据，特别是在移动应用程序中。除Chatter feeds, users, groups, 和followers外，Chatter REST API还提供对files, recommendations, topics, notifications, Data.com采购等salesforce数据的程式访问方法。Chatter REST API提供feeds，就像Facebook和Twitter提供的API一样，它还提供了了Chatter之外的Salesforce功能。  
* 何时使用Analytics REST API:  
你可以使用Analytics REST API以访问Salesforce Analytics的信息（如datasets，lenses，和dashboards）。例如可以直接向Analytics平台发送查询，访问已导入到Analytics平台的datasets、创建和获取lenses、访问XMD信息、获取datasets版本的列表、创建和获取Analytics applications、创建，更新和获取Analytics dashboards、获取application的依赖关系列表、确定用户可以使用哪些功能、使用snapshots、操作重复的datasets。  
* 何时使用Bulk API:  
Bulk API基于REST协议，并针对加载或删除大量数据进行了优化。你可以用它来一次性异步地查询，查询所有，插入，更新，插入或删除许多记录，Salesforce会在后台处理每批次。  
SOAP API针对实时客户端应用程序，对一次更新几条记录的进行了优化。所以你也可以使用SOAP API处理多个记录，但是当数据集包含数十万条记录时，SOAP API不太实用，Bulk API旨在使处理从数千条到数百万条记录的数据变得简单。  
使用Bulk API的最简单方法是使其能够使用CSV文件处理Data Loader中的记录，使用Data Loader可以避免编写复杂的API调用程序与逻辑。  
* 何时使用Metadata API:  
使用Metadata API可以获取，部署，创建，更新或删除你的Org的自定义项/信息，最常见的用途是将sandbox或testing的Org里的更改更新迁移到production的Org。Metadata API旨在用于管理自定义设置和构建可以管理元数据模型的工具，而不是处理数据本身。  
访问Metadata API中功能的最简单方法是使用Force.com IDE或Ant Migration Tool，这两个工具都是基于Metadata API构建的，分别使用标准的Eclipse和Ant工具来简化使用Metadata API。  
Force.com IDE构建在Eclipse平台上，适用于熟悉集成开发环境的程序员，开发者可以在该IDE中进行代码编译，测试和部署。  
如果你倾向使用脚本或命令行在本地目录和Salesforce Org之间传递元数据，则应选择Ant Migration Tool。  
* 何时使用Streaming API:  
使用Streaming API接收与你定义的SOQL查询相匹配的数据更改通知。  
如果你希望将通知从服务器推送到客户端时，建议使用Streaming API。持续对Salesforce服务器或基础架构进行轮询的应用程序会消耗不必要的API调用和处理时间，Streaming API减少了无效的请求（不返回数据或更新），且非常适用于大部分数据更改通知的需求。  
Streaming API使你可以减少API调用的数量并提高性能。  
* 何时使用Apex REST API:  
当你想通过API调用自己写好的Apex类/程序时，你需要使用Apex REST API，这样外部应用程序可以通过REST访问调用你的Apex代码。Apex REST API支持OAuth 2.0和用于授权的Session ID。  
* 何时使用Apex SOAP API:  
如果要将你的Apex程序公开为SOAP Web服务API，请使用Apex SOAP API，以便外部应用程序可以通过SOAP访问调用你的Apex代码。（基本与Apex REST API类似只是一个支持REST一个支持SOAP）  
Apex SOAP API支持OAuth 2.0和Session ID进行授权。  
* 何时使用Tooling API:  
使用Tooling API将Salesforce元数据与其他系统集成。元数据类型公开为sObjects，因此你可以访问一个复杂类型的一个component，此字段级访问加快了对复杂元数据类型的操作。你还可以为Force.com应用程序构建自定义开发工具，例如，使用Tooling API来管理和部署Apex类、triggers、Visualforce pages和components的工作副本。你还可以设置checkpoints或heap dump markers、执行匿名的Apex程序、访问日志和代码覆盖信息。  
REST和SOAP都支持。  
  
  
## 二、使用REST API
### 学习目标  
* 登录Workbench并使用REST Explorer  
* 使用describe resource  
* 使用REST API创建一个Account  
* 使用REST API执行一次查询  
  
### REST资源及方法
REST资源是一份信息或动作的抽象，例如单个数据记录，记录集合或查询（query）。REST API中的每个资源都由一个已命名的Uniform Resource Identifier（URI）标识，并可通过标准HTTP方法（HEAD，GET，POST，PATCH，DELETE）进行访问。REST API是基于资源的使用情况，资源的URI以及资源之间的链接。  
  
你通过使用资源与你的Salesforce org（组织）进行交互。例如，你可以：  
    * 检索有关可用的API版本的摘要信息。  
    * 获取有关Salesforce对象的详细信息，例如Account，Contact或自定义对象。  
    * 执行查询或搜索。  
    * 更新或删除记录。  
一个REST请求由四个部分组成：一个资源URI，一个HTTP方法，request headers（HTTP请求头字段）和request body（HTTP请求报文主体）。request headers指定请求的meta data（元数据）。request body可以为请求添加指定数据（比如认证、令牌等等），但它有很多时候可以被省去/省略为空的。  
  
### 描述Account对象
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
  
### 创建一个Account
现在使用SObject资源和POST方法创建一个Account。在URI输入框中，将现有文本替换为/services/data/vXX.0/sobjects/account。选择POST。这时出现了请求报文主体输入框，在这里可以为新Account指定其相关字段的值。  
请求报文主体例子：  
```json
{
    "Name" : "NewAccount1",
    "ShippingCity" : "San Francisco"
}
```
点击执行后如果返回“success:true”，则Account已被成功创建，返回的ID即Account的ID。（否则可以展开errors文件夹以查询反馈的错误信息）  

### 执行查询
现在假设你或其他用户创建了数百个Account，而你想查找航运城市是旧金山的所有Account的Name。你可以使用查询资源执行SOQL查询，并根据需要准确记录。  
URI输入框文本：/services/data/vXX.0/query/?q=SELECT+Name+From+Account+WHERE+ShippingCity='San+Francisco'。（我们用查询字符串中的+字符替换了空格，以正确编码URI，更多知识请链接阅读HTML URL编码）选择GET方法，然后单击执行。  
展开records文件夹。可以看到刚刚创建的Account - NewAccount1。点击该Account的文件夹，再点击attributes，url旁边是该Account的资源URI。  
  
Salesforce提供了不同语言的SDK，这样你调用API时更方便易用，比如Nforce（Node.js）和Restforce（Ruby）。  
Nforce用例：  
```javascript
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
```
  
Restforce用例：  
```ruby
require 'restforce'
# create the connection with the Salesforce connected app
client = Restforce.new :username => ENV['USERNAME'],
    :password       => ENV['PASSWORD'],
    :security_token => ENV['SECURITY_TOKEN'],
    :client_id      => ENV['CLIENT_ID'],
    :client_secret  => ENV['CLIENT_SECRET']
# execute the query
accounts = client.query("select id, name from account limit 5")
# output the account names
accounts.each do |account|
    p account.Name
end
```

未完待续...