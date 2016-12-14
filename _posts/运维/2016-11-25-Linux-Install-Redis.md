---
layout: post
title: Linux 安装与配置 Redis 环境
category: 运维
tags: Linux
keywords: 
description: 
---

本文简单介绍了在CentOS 6.8系统下Redis的安装过程，及启动脚本的编写。
如有问题，欢迎指正！！！

### 环境介绍

- 操作系统：CentOS 6.8 X64
- 软件版本：Redis 2.8.9

### 安装tcl支持

- Reids需要tcl的依赖，所以先安装该依赖，命令如下：

``` bash
$ yum install tcl
```

### 下载Redis

``` bash
$ wget http://download.redis.io/releases/redis-2.8.9.tar.gz
```

### 安装Redis

``` bash
$ tar xzf redis-2.8.9.tar.gz
$ cd redis-2.8.9
$ make
$ make install
```

> 安装后会自动把redis-server,redis-cli,redis-benchmark,redis-check-aof,redis-check-dump复制到/usr/local/bin目录下

### 配置Redis

``` bash
$ vim redis.conf
# daemonize no修改为yes
$ cp redis.conf /etc
```

### 编写启动脚本

- 创建启动脚本文件

``` bash
$ touch redis
```

- 打开该文件并写入以下内容

``` bash
PATH=/usr/local/bin:/sbin:/usr/bin:/bin
   
REDISPORT=6379
EXEC=/usr/local/bin/redis-server
REDIS_CLI=/usr/local/bin/redis-cli
   
PIDFILE=/var/run/redis.pid
CONF="/etc/redis.conf"
   
case "$1" in
    start)
        if [ -f $PIDFILE ]
        then
                echo "$PIDFILE exists, process is already running or crashed"
        else
                echo "Starting Redis server..."
                $EXEC $CONF
        fi
        if [ "$?"="0" ] 
        then
              echo "Redis is running..."
        fi
        ;;
    stop)
        if [ ! -f $PIDFILE ]
        then
                echo "$PIDFILE does not exist, process is not running"
        else
                PID=$(cat $PIDFILE)
                echo "Stopping ..."
                $REDIS_CLI -p $REDISPORT SHUTDOWN
                while [ -x ${PIDFILE} ]
               do
                    echo "Waiting for Redis to shutdown ..."
                    sleep 1
                done
                echo "Redis stopped"
        fi
        ;;
   restart|force-reload)
        ${0} stop
        ${0} start
        ;;
  *)
    echo "Usage: /etc/init.d/redis {start|stop|restart|force-reload}" >&2
        exit 1
esac
```

- 拷贝该文件到`/etc/init.d/`目录下，命令如下：

``` bash
$ cp redis /etc/init.d/
```

- 设置启动脚本的执行权限，命令如下：

``` bash
$ chmod a+x /etc/init.d/redis
```

### 开机启动

- 设置redis开机启动，命令如下：

``` bash
$ chkconfig redis on
```

### 相关命令

``` bash
# 启动服务
service redis start
# 重启服务
service redis restart
# 停止服务
service redis stop
```

