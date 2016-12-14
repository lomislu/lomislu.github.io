---
layout: post
title: Linux 安装与配置 Nginx 环境
category: 运维
tags: Linux
keywords: 
description: 
---

基于本人自己在CentOS 6.8系统下用不同的方式进行安装Nginx，现整理成本文，如有问题，欢迎指正！！！

### 环境介绍

- CentOS 6.8 X64
- Nginx：1.8.1

### 文章要求

- 有一定的Linux基础
- 新人的话，建议先适当的了解一些Linux基础命令

### Nginx

<!--### yum方式安装-->

- 可通过以下命令查看yum所提供的Nginx服务器的可下载版本

``` bash
$ yum list | grep nginx
```

- 通过以上命令查看到可下载的Nginx版本后，可执行下以命令进行Nginx的安装

``` bash
$ yum install -y nginx
```

- 相关命令

``` bash
# 启动服务
$ service nginx start
# 重启服务
$ service nginx restart
# 停止服务
$ service nginx stop
# 查看服务状态
$ service nginx status
```

- 相关文件位置位于：`/etc/nginx`
- 查看相关信息：`rpm -qi nginx`

<!--### 源码编译安装-->

<!-- - 持续更新中... -->

