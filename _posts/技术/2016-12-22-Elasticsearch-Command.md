---
layout: post
title: Elasticsearch 命令详解
category: 技术
tags: Elasticsearch
keywords: 
description: 
---

记录一下Elasticsearch的常用命令，以便查阅！

### Elasticsearch常用命令

- 查看所有indices信息

```bash
http://localhost:9200/_cat/indices?v
```

- 查看某 index 下的所有信息，例如：`test`

```bash
http://localhost:9200/test
```

- 查看所有mapping信息

```bash
http://localhost:9200/_mapping
```

- 查看某 index 下的所有mapping，例如：`test`

```bash
http://localhost:9200/test/_mapping
```

- 查看某 index 下某 type 的mapping，例如：`test`下的`access`

```bash
http://localhost:9200/test/access
```
