---
layout: post
title: Linux 安装与配置 Tomcat 环境
category: 运维
tags: Linux运维
keywords: 
description: 
---

基于本人自己在CentOS 6.8系统下用不同的方式进行Tomcat，现整理成本文，如有问题，欢迎指正！！！

### 环境介绍

- CentOS 6.8 X64
- Tomcat：6.0

### Tomcat安装

- 从[Apache官网](http://tomcat.apache.org)下载包

``` bash
$ wget http://mirror.stjschools.org/public/apache/tomcat/tomcat-6/v6.0.45/bin/apache-tomcat-6.0.45.tar.gz
```

- 解压、复制、重命名

``` bash
# 解压并复制到/usr/local/下
$ tar -xzf apache-tomcat-6.0.45.tar.gz -C /usr/local/
# 重命名
$ mv /usr/local/apache-tomcat-6.0.45 /usr/local/tomcat
```

- 相关命令

``` bash
$ cd /usr/local/tomcat/bin
# 启动服务
$ ./startup.sh
# 停止服务
$ ./shutdown.sh
```


