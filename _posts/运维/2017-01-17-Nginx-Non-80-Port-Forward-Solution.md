---
layout: post
title: Nginx服务器中非80端口的端口转发解决方案
category: 运维
tags: Linux运维
keywords: 
description: 
---

### 1、问题简介
之前在 Amazon 服务器的Tomcat上部署了一套系统的管理后台，Web 服务器采用Nginx 进行反向代理Tomcat 应用服务器，因为历史遗留问题Nginx采用的是非80端口，导致后端服务器中 request.getServerPort()无法获得正确的端口，返回的还是80端口。

Nginx 虚拟主机配置如下：

```bash
server {
	listen 81;
	server_name localhost;
	location / {
		proxy_pass http://x.x.x.x:8080;
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header Via "nginx";
	}
}
```

### 2、解决方案

关键就在于之前配置中的`proxy_set_header Host $host`，以下为修改后的完成配置：

```bash
server {
	listen 81;
	server_name localhost;
	location / {
		proxy_pass http://x.x.x.x:8080;
		proxy_set_header Host $host:81;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header Via "nginx";
	}
}
```