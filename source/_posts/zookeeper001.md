---
title: zookeeper概览
date: 2016-07-09 11:58:47
tags:
---

## ZooKeeper: A Distributed Coordination Service for Distributed Applications ##
ZooKeeper is a distributed, open-source coordination service for distributed applications. It exposes a simple set of primitives that distributed applications can build upon to implement higher level services for synchronization, configuration maintenance, and groups and naming. It is designed to be easy to program to, and uses a data model styled after the familiar directory tree structure of file systems. It runs in Java and has bindings for both Java and C.

Coordination services are notoriously hard to get right. They are especially prone to errors such as race conditions and deadlock. The motivation behind ZooKeeper is to relieve distributed applications the responsibility of implementing coordination services from scratch.

## Design Goals ##
**ZooKeeper is simple.** ZooKeeper allows distributed processes to coordinate with each other through a shared hierarchal namespace which is organized similarly to a standard file system. The name space consists of data registers - called znodes, in ZooKeeper parlance - and these are similar to files and directories. Unlike a typical file system, which is designed for storage, ZooKeeper data is kept in-memory, which means ZooKeeper can acheive high throughput and low latency numbers.

*The ZooKeeper* implementation **puts** a premium on ***high*** performance, highly available, strictly ordered access. The performance aspects of ZooKeeper means it can be used in large, distributed systems. The reliability aspects keep it from being a single point of failure. The strict ordering means that sophisticated synchronization primitives can be implemented at the client.

ZooKeeper is replicated. Like the distributed processes it coordinates, ZooKeeper itself is intended to be replicated over a sets of hosts called an ensemble.

## ZooKeeper: 用于分布式应用的分布式协调服务 ##
Zookeeper是一个用于分布式应用上的分布式的、开源的协调服务。它暴露一组简单的组件，在此之上，分布式应用可以实现更高层次的服务，如同步、配置管理、分组和命名等。它被设计得易于开发，并且使用的数据模型也是基于熟识的文件系统的树形结构。运行在Java上，并且与Java和C绑定在一起。

众所周知，分布式服务很难保证正确性。特别易于出现竟态条件或是死锁这样的错误。Zookeeper背后的动机就是，减轻分布式系统从0开始实现协调服务的重担。

## 设计目标 ##


[原文](http://zookeeper.apache.org/doc/r3.4.8/zookeeperOver.html)
`本站独自翻译，转载请注明出处`