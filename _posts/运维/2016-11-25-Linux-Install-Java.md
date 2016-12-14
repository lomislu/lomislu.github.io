---
layout: post
title: Linux 安装与配置 Java 环境
category: 运维
tags: Linux
keywords: 
description: 
---

基于本人自己在CentOS 6.8系统下用不同的方式进行Java，现整理成本文，如有问题，欢迎指正！！！

### 环境介绍

- CentOS 6.8 X64
- Java：7.79

### 文章要求

- 有一定的Linux基础
- 新人的话，建议先适当的了解一些Linux基础命令

### 卸载OpenJDK

- 可通过以下命令来查看当前系统是否已安装了Java

``` bash
$ rpm -qa | grep java
```

- 有的话，通过以下命令进行卸载OpenJDK

> 普通删除模式，删除时会提示有依赖其它文件
> 
``` bash
$ rpm -e java
```

或

> 强力删除模式
> 
``` bash
$ rpm -e —nodeps java
```


### RPM方式安装

- 从[Oracle](http://www.oracle.com)官网下载Java的RPM安装包

``` bash
$ wget http://download.oracle.com/otn-pub/java/jdk/7u79-b15/jdk-7u79-linux-x64.rpm
```

- 安装

``` bash
$ rpm -ivh jdk-7u79-linux-x64.rpm
```

- 环境变量设置，在`/etc/profile`文件结尾追加以下内容

``` bash
export JAVA_HOME=/usr/java/jdk1.7.0_79
export JRE_HOME=/usr/java/jdk1.7.0_79/jre
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
```
	
- 使环境变量生效
	
``` bash
$ source /etc/profile
```
	
- 查看Java版本

``` bash
$ java -version
```

### 软件包安装

- 从[Oracle](http://www.oracle.com)官网下载Java的安装包

``` bash
$ wget  http://download.oracle.com/otn-pub/java/jdk/7u79-b15/jdk-7u79-linux-x64.tar.gz
```

> 如果wget命令无法使用的话，请先执行:`yum install wget`

- 解压软件包

``` bash
$ mkdir /usr/local/java
$ tar -xzf jdk-7u79-linux-x64.tar.gz -C /usr/local/java/
```

- 环境变量设置，在`/etc/profile`文件结尾追加以下内容

``` bash
export JAVA_HOME=/usr/java/jdk1.7.0_79
export JRE_HOME=/usr/java/jdk1.7.0_79/jre
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
```
	
- 使环境变量生效
	
``` bash
$ source /etc/profile
```
	
- 查看Java版本

``` bash
$ java -version
```


