---
layout: post
title:  "Salesforce Apex基础与数据库"
date:   2018-09-10 00:00:00 +1200
categories: crm
tags: salesforce
---

## Salesforce Apex基础与数据库

## 一、Apex 入门

![](https://res.cloudinary.com/hy4kyit2a/f_auto,fl_lossy,q_70/learn/modules/apex_database/apex_database_intro/images/b5f118b227075065ebbc42ff4e9ea26b_apex_database_architecture.png)

......

### 数据类型

#### Apex Collections: List

Lists 里包含了一个排了序的 objects 集，它和 Java 里的 List 是一样的，是数组类数据结构。
下面的两个例子是同义的，即 colors 变量数组通过 List 语法声明。
```java
List<String> colors = new List<String>();
```
以数组形式声明但赋值给 List 而不是 array。
```java
String[] colors = new List<String>();
```
  
通过 List 声明通常更为简易，因为无需在一开始声明数组长度。List 语法可以在一开始声明元素，也可以在之后通过 add() 方法增添元素。
```java
List<String> colors = new List<String>();
String[] colors = new List<String>();

// Create a list and add elements to it in one step
List<String> colors = new List<String> { 'red', 'green', 'blue' };
// Add elements to a list after it has been created
List<String> moreColors = new List<String>();
moreColors.add('orange');
moreColors.add('purple');
```

......

### Apex Classes

......

<!-- more -->

## 二、使用 sObjects

在 Salesforce 里，标准和自定义的 object records 在 Apex 里一一对应它们的 sObject types。以下是一些 Apex 里常用的标准 object 的 sObject type 名。
* Account
* Contact
* Lead
* Opportunity


## 三、通过 DML 操作 Records

### 学习目标
* 通过 DML 插入, 更新, 以及删除 records
* 批处理 DML 命令
* 使用 upsert 来进行插入或更新一个 record
* Catch 一个 DML 指令的 Exception
* 使用一个数据库方法/函数来插入新的带有部分成功选项的 records 并处理其结果
* 应何时使用 DML 指令以及何时使用数据库操作/方法
* 在相关 records 上执行 DML 指令操作
  
### 通过 DML 操作 Records
创建或更新一个 Salesforce 记录（record）时需要使用 Data Manipulation Language (DML)，其功能包括插入、更新、合并、删除和恢复记录（record）。  
Apex 是一个 data-focused 语言且保存在 Lightning Platform, 它可以直接访问你的 Salesforce 上的数据。Apex不像其他语言，它不需要任何 setup。  
以下例子是创建了一个 Acme 的 Account 后再在 insert 命令里调用，最后保存该 Account 到 Salesforce 上：  
```java
// Create the account sObject 
Account acct = new Account(Name='Acme', Phone='(415)555-1212', NumberOfEmployees=100);
// Insert the account by using DML
insert acct;
```
  
### DML 命令/指令
以下是可用的 DML 命令/指令：
* insert
* update
* upsert
* delete
* undelete
* merge

每个 DML 指令后可以跟随单个 sObject 或一组 sObjects。操纵一组 sObjects 对记录处理更加高效。  
所有这些指令，除了两个（upsert 和 merge 是 Salesforce 为开发者方便而自创的）之外，都是和主流数据库指令相似的。  
DML 指令 upsert 将新建或更新一个 sObject 记录，通过指定的一个判断 field 去判定是否已存在旧 objects，否则创建新的 ID field（如果没有指定判断 field）。  
DML 指令 merge 最多可以合并三个记录（sObject 类型需一致）到其中一个记录里，并删除其余两个记录，并可以重新指定相关的父记录。


