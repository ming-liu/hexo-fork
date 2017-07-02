---
title: NIOServerCnxnFactory
date: 2017-07-02 16:36:13
tags:
---


## 简介 ##

Zookeeper 默认的ServerCnxnFactory的实现。顾名思义，采用非阻塞通信方式。特点是采用了多个线程来分别处理各类型事件。

### 1、1个accept thread.###
##### 1.1 类结构 ##### 
```AcceptThread->AbstractSelectThread->ZooKeeperThread```
##### 1.2 解释 #####
+ a) 每个AbstractSelectThread的对象都维持这一个 selector```this.selector = Selector.open()``` 。
+ b) acceptThread对象把ServerSocketChannel的OP_ACCEPT事件注册到本对象的 selector 上。
+ c) 当一个新的链接 被 accept之后,就把此链接的处理交给某个selectThread,通过调用```SelectorThread.addAcceptedConnection(SocketChannel)```,采用Round-robin策略,其实就是```iterator.next()```。这个时候一个socket接入完成，剩下的是selector thread的事了。

### 2、1-n个 selector threads.###
##### 2.1 类结构 ##### 
SelectorThread->AbstractSelectThread->ZooKeeperThread
##### 2.2 解释 #####
+ a) 当一个acceptThread把SocketChanel传给selectorThread时,调用的addAcceptedConnection，这个方法是把socketChannel加到acceptedQueue里,每个acceptThread有一个LinkedBlockingQueue类型的队列。(而且我看的版本LinkedBlockingQueue没设置大小。)
+ b) acceptThread的run方法里。
	1. select 
	2. 把readable和writable的selectionKey封装成IOWorkRequest对象,放到workerPool(work threads)里。
	3. 把acceptedQueue的socket的OP_READ注册到selector上。
	4. 处理updateQueue 目前未知...

### 3、0-m个 work threads.###
##### 3.1 结构 ##### 
org.apache.zookeeper.server.WorkerService,其中实例变量:ArrayList<ExecutorService> workers = new ArrayList<ExecutorService>();
##### 3.2 解释 #####


### 4、connection expiration thread ###
类结构ConnectionExpirerThread->ZooKeeperThread