---
layout: post
title: 修改 Linux 的最大文件连接数
category: 运维
tags: Linux运维
keywords: 
description: 
---

在项目上线过一段时间后，发现程序报 Too many open files 异常，今天给主要是为大家分析一下该问题的原因及解决方案。

### 1、原因分析

一般出现该异常，通常情况下是程序打的文件连接数过多，超过了系统的设定值；

解决该问题最好还是先从程序的角度入手，审核代码一下代码看有没有打开的文件或 Socket 没有正常关闭；

以下是通过调整系统参数进行解决该问题的方案；

### 2、解决方案

网上的解决方案有很多，大致分为了两个方案，分别为：临时方案、永久方案

具体采用哪种方案，可根据各自的需求进行选择，我这里选择的是永久方案；

#### 2.1、临时方案

采用 `ulimit -n 65535` 进行设置，但该方案只能当前终端有效，一旦退出则恢复为系统默认值；


#### 2.2、永久方案

- 在 `/etc/security/limits.conf` 文件的后面加上以下两行内容：

``` bash
*   soft    nofile  65535
*   hard    nofile  65535
```

- 该方案需要重启服务器才可生效。

- 重启完成后可能过以下命令查看结果：

```bash
$ ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 128630
max locked memory       (kbytes, -l) 64
max memory size         (kbytes, -m) unlimited
open files                      (-n) 65535
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 128630
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```


