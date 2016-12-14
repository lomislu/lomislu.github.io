---
layout: post
title: Linux 安装与配置 Docker 环境
category: 运维
tags: Linux运维
keywords: 
description: 
---

总结一下自己在 CentOS 6.8系统下安装与配置 Docker 的全过程。并简单讲解了一下Docker的常用命令。
如有问题，欢迎指正！！！

### 环境介绍

- 操作系统：CentOS 6.8 X64
- 软件版本：Docker 1.11.2

### Docker的简单介绍
Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口。来源:[百度百科](http://baike.baidu.com/link?url=In6dGkZvsuAEfdgTiFmhFZY6VvXzG2ldEak8Pf_6ea0_iuxqVQou4B96yWxT4bA-vXBWDuu4pSYBbcNz7sgZZ_)

由于公司将整体采用Docker进行环境的部署，故简单学习了一下Docker的基本用法，现整理出来，以作参考！

### 安装Docker与使用

- 安装Docker服务，命令如下：

``` bash
$ yum install docker -y
```

- 安装完成之后，启动Docker服务，命令如下：

``` bash
$ service docker start      # 启动服务
$ service docker stop       # 停止服务
$ service docker restart    # 重启服务
$ service docker status     # 服务状态
```

### Images（镜像）篇

- 拉取Image，命令如下

``` bash
$ docker pull repository:tag
# 如拉取CentOS的Image，命令如下：
$ docker pull centos:latest
```

- 查看Image，命令如下

``` bash
$ docker images
```

- 删除Image，命令如下

``` bash
$ docker rmi [image id]/[repository:tag]
```

- 查看Image信息，命令如下

``` bash
$ docker inspect [image id]/[repository:tag]
```

- 搜索Image，命令如下

``` bash
$ docker search centos
```

- 提交一个容器为镜像，命令如下

``` bash
$ docker commit [container id]/[container name] repository:tag
```

### Container(容器）篇

- 创建Container，命令如下

``` bash
$ docker create -it centos:latest
```

- 新建并启动Container，通过下面命令可以启动一个bash终端，允许用户进行交互，命令如下：

``` bash
$ docker run -i -t centos:latest /bin/bash

# 常用参数：
# -t : 让Docker分配一个伪终端并绑定到容器的标准输入上；
# -i : 让容器的标准输入保持打开状态；
# -d : 让容器在后台以守护状态形式运行；
# -v ：可以在容器内创建一个数据卷，可多次使用；
# -P : 指定端口映射，允许外部访问容器需要暴露的端口，可多次使用；
# -name ：自定义容器的名称；
```

- 停止Container，命令如下

``` bash
$ docker stop [container id]/[container name]
```

- 查看Container，命令如下

``` bash
$ docker ps -a
```

- 进入Container，命令如下

``` bash
$ docker exec -it  [container id]/[container name] /bin/bash
```

- 删除Container，命令如下

``` bash
$ docker rm  [container id]/[container name]

# 常用参数：
# -f ：强行停止并删除一个运行中的容器；
# -l : 删除容器的连接，但保留容器； 
# -v : 删除容器挂载的数据卷；
```

- 查看 Container 的使用情况，命令如下：

``` bash
$ docker stats
```

### 数据卷篇

- 挂载一个目录作为数据卷，命令如下：

``` bash
$ docker run -d -P --name test-vol -v /home/ec2-user/vol:/home/vol centos:latest /run.sh
```

- 挂载一个本地主机文件作为数据卷，命令如下：

``` bash
$ docker run -d -P --name test-vol -v ~/.bash_profile:/home/.bash_profile centos:latest /run.sh
```


### 网络基础配置篇

- 映射端口地址，命令如下：

``` bash
# 将容器内的8080端口映射为本机的18080端口
$ docker run -d -P 18080:8080 --name test-vol centos:latest /run.sh
```


