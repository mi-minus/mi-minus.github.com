---
layout: life
title: Elasticsearch集群部署
category: Mongo
duoshuo: true
date: 2017-05-20
---

******

	作者: minus
	版本: V 0.0.1
	日期: 2017年05月20日
	mail: minus@stu.xjtu.edu.cn

<!-- more -->

*******

### Elasticseach集群架构
1. ES基本情况及集群服务器情况
```
该mongo集群服务器一共使用8台服务器，其中6台服务器用来部署搭建shard /  config / arbiter 服务器，剩下两台服务器用来搭建mongos，以供外部应用连接
本集群使用的是mongo最新版本3.4, 其具有更强大的功能
```
