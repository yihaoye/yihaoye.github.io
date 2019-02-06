---
layout: post
title:  "Salesforce CI/CD"
date:   2018-08-28 21:12:21 +1200
categories: crm
tags: salesforce
---
原文参考：https://trailhead.salesforce.com/trails/sfdx_get_started/modules/sfdx_travis_ci/units/sfdx_travis_ci_setup

## 使用Salesforce DX实现CI/CD： 
Salesforce DX允许开发者使用一系列第三方工具，这意味着你可以使用任何你想用的CI或CD服务。本文将使用GitHub和Travis CI举例实现CI/CD。  
另外，在此之前你需要在本机安装Salesforce CLI、Git，并注册了GitHub账号。  

<!-- more -->

### 一、准备工作 GitHub和Travis CI  
然后把GitHub上的repository clone至本地，如  
git clone https://github.com/<GH_username>/sfdx-travisci.git  
这个repository应该是包含了一个Salesforce DX项目，并已配置好的。  

使用GitHub账号注册Travis CI账号  
在Travis CI上设置以选择哪个GitHub repository（比如sfdx-travisci）启用Travis CI。这样意味着Travis CI已经开始跟进你的GitHub repository了。你将在该GitHub repository的.travis.yml配置文件上编写CI命令以决定CI过程的所有步骤行为。  

本地下载安装Travis CI CLI


### 二、创建你的Connected App  



未完待续...