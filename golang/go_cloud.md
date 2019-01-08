# go-cloud

# 一 概述
go_cloud、第三方包和开源项目的笔记

## 1 简介
Go Cloud Project是一项计划，允许应用程序开发人员在任何云提供商组合上无缝部署云应用程序。它通过为存储和数据库等常见用途提供稳定的惯用接口来实现此目的，旨在为各种云中最常用的服务提供中立于厂商的 API，这样可以轻松地将 Go 应用程序进行跨云迁移。

该项目的一个关键部分是提供一个名为Wire的代码生成器 。它创建了人类可读的代码，仅为您使用的提供程序导入云SDK。这允许Go Cloud增长以支持任意数量的云提供商，而不会增加编译时间或二进制大小，并避免init()功能的不良影响。Wire使用依赖注入自动连接组件。组件依赖关系表示为函数参数，并鼓励开发人员进行显式初始化，而不是使用全局变量。Wire可以在没有运行时状态或反射的情况下执行，从而可以使用手写的初始化代码。

目前，主要提供对 AWS 和 Google Cloud Platform 的支持。

Go Cloud 是一个可在开放云平台上进行开发的库和工具集

# 四 高级
## 1 groupcache

## 2 https://github.com/go-playground/validator/tree/v9.24.0

## 3 github.com/SebastiaanKlippert/go-wkhtmltopdf

## 4 猴子补丁
在测试用例中挺好用的：https://github.com/bouk/monkey。注意下载和引入是`bou.ke/monkey`，github地址只是放的代码，而不是引入用的地址。

参考：https://www.jianshu.com/p/2f675d5e334e?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation


# 七 未整理
## 2 未整理
1. Google Cloud Platform是干嘛的