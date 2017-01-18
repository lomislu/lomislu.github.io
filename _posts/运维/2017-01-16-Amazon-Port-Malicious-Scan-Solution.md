---
layout: post
title: Amazon端口被恶意扫描的解决方案
category: 运维
tags: Linux运维
keywords: 
description: 
---

以下是我在实际的工作中所遇到的问题，在这里主要记录一下我的处理过程，如有不当之处，欢迎指正！

### 1、背景介绍

最近公司针对大数据进行实时分析与统计，故此在 Amazon 云上搭建了一套 ELK 环境，在使用的过程中发现数据莫名其妙被删除，经排查发现是别有用心之人进行端口扫描使其服务器成为矿机，数据也被劫持。
故此发现是服务器端口直接暴露到公网导致的。

### 2、解决方案

- 取消 Nginx 对Elasticsearch 及 Kibana 服务的反向代理
- 所有程序统一使用内网进行访问
- 在部署了 ELK 环境的服务器上设置 Amazon 安全策略使其这些端口仅公司内部 IP 可访问


### 3、方案加强

虽然以上方案可以有效的解决端口被恶意扫描及数据劫持，但也把Nginx通过反向代理访问 Elasticsearch 及 Kibana 服务的路堵死了，带来了很多局限，在公网环境下（不使用公司网络）无法访问到对应的服务。

为了解决这一问题，只能重新打开Nginx对Elasticsearch 及 Kibana 服务的反向代理，使其在公网环境下（不使用公司网络）可通过域名进行访问服务。

针对这一处理，首先就是要考虑的就是安全问题，防止被恶意扫描端口，必须要对Nginx访问进行权限设置。

#### 3.1、安装 httpd

如果系统没有安装 httpd，请安装，以下是安装命令：

``` bash
$ yum install httpd
```

#### 3.2、通过htpasswd命令生成用户名及对应密码数据库文件

执行命令如下：

```bash
$ htpasswd -b -c /etc/nginx/nginx_passwd username password
```

#### 3.3、修改 Nginx 虚拟主机配置

如果是为了给网站加上认证，可以直接将认证语句写在 Nginx 的配置 server 段中，如下：

```bash
server {
	listen       80;
	server_name  xxx.xxx.com
	auth_basic "密码提示语";  
	auth_basic_user_file /vhost/nginx_passwd;
}
```

如果是为了给目录加上认证，需要在对应的目录中加入认证语句，如下：

```bash
location /webservice {
	auth_basic "密码提示语";  
	auth_basic_user_file /vhost/nginx_passwd;  
}
```