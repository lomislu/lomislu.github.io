---
layout: post
title: Linux 安装与配置 Kafka 环境
category: 运维
tags: Linux运维
keywords: 
description: 
---

由于工作中简单的用到了Apache Kafka框架，主要使用Kafka进行日志输出，方便后续对日志进行分析与统计，故整理一下，以作参考，方便后续查阅。

### 环境介绍

- 操作系统：CentOS 6.8 X64
- 软件版本：kafka_2.10-0.8.2.2

### Kafka的简单介绍

Kafka是一种高吞吐量的分布式发布订阅消息系统，它可以处理消费者规模的网站中的所有动作流数据。 这种动作（网页浏览，搜索和其他用户的行动）是在现代网络上的许多社会功能的一个关键因素。 这些数据通常是由于吞吐量的要求而通过处理日志和日志聚合来解决。 对于像Hadoop的一样的日志数据和离线分析系统，但又要求实时处理的限制，这是一个可行的解决方案。Kafka的目的是通过Hadoop的并行加载机制来统一线上和离线的消息处理，也是为了通过集群机来提供实时的消费。来源:[百度百科](http://baike.baidu.com/link?url=xDBVsk6F3B10AZIGZHzgIw23OPTZuyZoZthIAKL_TUn74rN8vjX05ee8IJy3bWdPldzOGzm6X5d-gNWdTy2-BK)

### 安装与简单使用

- 下载软件包

``` bash
$ wget http://apache.fayea.com/kafka/0.8.2.2/kafka_2.10-0.8.2.2.tgz
```

- 安装

``` bash
$ tar xzf kafka_2.10-0.8.2.2.tgz -c ~/
$ mv ~/kafka_2.10-0.8.2.2 ~/kafak-server
```

- 启动

``` bash
$ cd ~/kafka-server
$ nohup bin/zookeeper-server-start.sh config/zookeeper.properties &
$ nohup bin/kafka-server-start.sh config/server.properties &
```

### 常用命令

- 创建一个Topic

``` bash
$ bin/kafka-topics.sh --create --zookeeper localhost:2181 --topic test
```

- 查看所有Topic

``` bash
$ bin/kafka-topics.sh --list --zookeeper localhost:2181
```

- 连接一个Topic

``` bash
$ bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
```

- 查看并接收一个Topic的信息

``` bash
$ bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning
```

- 查看所有Topic的详细信息

``` bash
$ bin/kafka-topics.sh --describe --zookeeper localhost:2181
```

- 查看某一个Topic的详细信息

``` bash
$ bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic test
```

