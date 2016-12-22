---
layout: post
title: MySQL异常大全
category: 运维
tags: MySQL
keywords: 
description: 
---

本文主要收集平常在工作及开发过程中所遇到的 MySQL 异常解决方案，持续完善中......

##### 1、Lost connection to MySQL server at 'waiting for initial communication packet', system error: 60


很明显这是连接初始化阶段就丢失了连接的错误，只需要在 my.conf 文件的[mysqld]项中加入以下内容即可：

```bash
skip-name-resolve
```
