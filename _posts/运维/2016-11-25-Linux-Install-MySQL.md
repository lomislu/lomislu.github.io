---
layout: post
title: Linux 安装与配置 MySQL 环境
category: 运维
tags: Linux运维
keywords: 
description: 
---

基于本人自己在CentOS 6.8系统下用不同的方式进行安装MySQL，现整理成本文，如有问题，欢迎指正！！！

### 环境介绍

- CentOS 6.8 X64
- MySQL：5.5

### MySQL安装

<!--### yum方式安装-->

- 要通过yum方式进行安装MySQL时，首先要通过以下命令来查看yum所提供的MySQL数据库的可下载版本

``` bash
$ yum list | grep mysql
```

- 通过以上命令查看到可下载的MySQL版本后，可执行下以命令进行MySQL的安装

``` bash
$ yum install -y mysql-server
```

- 执行以上命令之后，等待一段时间后，yum会帮我们选择MySQL数据库所需的软件以及其它依赖软件，并进行安装，安装过程视网络情况而定，等待一段时间之后，当出现Complete！就代表MySQL数据库安装成功
- 安装成功之后可用以下命令查看当前MySQL数据库的相关信息

``` bash
$ rpm -qi mysql-server
```

- 首次使用`service mysqld start`启动MySQL服务时，MySQL首先会进行初始化配置
- 首次启动MySQL服务时会提示非常多的信息，目的就是对MySQL数库进行初始化配置，当我们使用`service mysqld restart`再次重新启动时，就不会提示这么多的信息
- MySQL的开机自启动设置，命令如下：

``` bash
$ chkconfig —list | grep mysqld
$ chkconfig mysqld on
```

- 进行MySQL的配置

``` bash
$ mysql_secure_installation
```
> 执行以上命令时，所有需要确认的地方全部为：y
> 
> 在需要设置root的密码需要注意一下

- 设置root账户密码之后就可以通过以下命令登录MySQL数据库

``` bash
$ mysql -u root -p
```

- 相关命令

``` bash
# 启动服务
service mysqld start
# 重启服务
service mysqld restart
# 停止服务
service mysqld stop
# 查看服务状态
service mysqld status
```

- 主配置文件位置：`/etc/my.cnf`
- 数据文件存放位置：`/var/lib/mysql`
- MySQL远程访问配置

``` bash
# 使用以下命令连接MySQL
$ mysql -u root -p

# 连接后输入以下命令
use mysql;
update user set host = ‘%’ where user=‘root’ and host=‘localhost’;
flush privileges;
```
<!--### 源码编译安装-->

<!--- 持续更新中...-->

