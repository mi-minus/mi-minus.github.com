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
1. ES基本情况
```
ElasticSearch是一个基于Lucene的搜索服务器。它提供了一个分布式多用户能力的全文搜索引擎，基于RESTful web接口。Elasticsearch是用Java开发的，并作为Apache许可条款下的开放源码发布，是当前流行的企业级搜索引擎。设计用于云计算中，能够达到实时搜索，稳定，可靠，快速，安装使用方便
```
2. 及集群服务器情况
```
整个集群的部署采用4台服务器，其中一台作为master，其他三台作为slaves
```

3. 各服务器配置参数(舆情集群实例)
```
======================================== master[yuqing4] - configuration =============================================================
-------------------- Cluster --------------------------
cluster.name: yuqing
------------------- Node ----------------------------
node.name: node-yuqing4
------------------- Paths ----------------------------
path.data: /yuqing/elasticsearch/data
------------------- Network ----------------------------
network.bind_host: ['ip内网xx.xx.xx.xx', 'ip外网:xx.xx.xx.xx']
network.publish_host: ip内网xx.xx.xx.xx
------------------- Discovery ----------------------------
discovery.zen.ping.unicast.hosts: ['yuqing1-ip内网xx.xx.xx.xx', 'yuqing2-ip内网xx.xx.xx.xx', 'yuqing3-ip内网xx.xx.xx.xx', 'yuqing4-ip内网xx.xx.xx.xx']
------------------- Various ----------------------------
node.master: true
node.data: false
http.enabled: true
http.cors.enabled: true
http.cors.allow-origin: "*"
======================================== slave1 [yuqing1] - configuration =============================================================
-------------------- Cluster --------------------------
cluster.name: yuqing
------------------- Node ----------------------------
node.name: node-yuqing1
------------------- Paths ----------------------------
path.data: /yuqing/elasticsearch/data
------------------- Network ----------------------------
network.bind_host: ['ip内网xx.xx.xx.xx']
network.publish_host: ip内网xx.xx.xx.xx
------------------- Discovery ----------------------------
discovery.zen.ping.unicast.hosts: ['yuqing1-ip内网xx.xx.xx.xx', 'yuqing2-ip内网xx.xx.xx.xx', 'yuqing3-ip内网xx.xx.xx.xx', 'yuqing4-ip内网xx.xx.xx.xx']
------------------- Various ----------------------------
node.master: false
node.data: true
http.enabled: true
http.cors.enabled: true
http.cors.allow-origin: "*"
======================================== slave2 [yuqing2] - configuration =============================================================
-------------------- Cluster --------------------------
cluster.name: yuqing
------------------- Node ----------------------------
node.name: node-yuqing2
------------------- Paths ----------------------------
path.data: /yuqing/elasticsearch/data
------------------- Network ----------------------------
network.bind_host: ['ip内网xx.xx.xx.xx']
network.publish_host: ip内网xx.xx.xx.xx
------------------- Discovery ----------------------------
discovery.zen.ping.unicast.hosts: ['yuqing1-ip内网xx.xx.xx.xx', 'yuqing2-ip内网xx.xx.xx.xx', 'yuqing3-ip内网xx.xx.xx.xx', 'yuqing4-ip内网xx.xx.xx.xx']
------------------- Various ----------------------------
node.master: false
node.data: true
http.enabled: true
http.cors.enabled: true
http.cors.allow-origin: "*"
======================================== slave3 [yuqing3] - configuration =============================================================
-------------------- Cluster --------------------------
cluster.name: yuqing
------------------- Node ----------------------------
node.name: node-yuqing3
------------------- Paths ----------------------------
path.data: /yuqing/elasticsearch/data
------------------- Network ----------------------------
network.bind_host: ['ip内网xx.xx.xx.xx']
network.publish_host: ip内网xx.xx.xx.xx
------------------- Discovery ----------------------------
discovery.zen.ping.unicast.hosts: ['yuqing1-ip内网xx.xx.xx.xx', 'yuqing2-ip内网xx.xx.xx.xx', 'yuqing3-ip内网xx.xx.xx.xx', 'yuqing4-ip内网xx.xx.xx.xx']
------------------- Various ----------------------------
node.master: false
node.data: true
http.enabled: true
http.cors.enabled: true
http.cors.allow-origin: "*"
```
