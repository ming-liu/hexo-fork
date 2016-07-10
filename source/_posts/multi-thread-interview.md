---
title: Java多线程面试题汇集
date: 2016-03-01 07:27:58
tags:
---

#### 1、Thread.sleep、Thread.yield和Object.wait的区别 ####


	a) Thread.yield: 通知scheduler,当前线程准备放弃当前正在使用的cpu。scheduler也可以忽略此通知。让出cpu,进入待执行状态。有可能继续获得cpu时间片。不会让给优先级低的线程。不释放锁。
	b) Thread.sleep: 释放cpu,可能会让给优先级低的线程。不释放锁。
	c) Object.wait:释放cpu,释放锁，必须在synchronized中执行。


#### 2、哪些原因会导致共享变量，在其他线程无法及时看到最新值？####

	a) 在编译器中生成的指令顺序，可以与源码中的顺序不同。此外，编译器还会把变量保存在寄存器中而不是内存中。
	b) 处理器可以采用乱序或并行等方式来执行指令。
	c) 缓存可能会改变将写入变量提交到内存的次序。
	d) 保存在处理器本地缓存中的值，对于其他处理器是不可见的。

#### 3、volatile的作用####

	a) 64位(double、long)原子操作
	b) 内存可见性,volatile变量不会被缓存在寄存器或者对其他处理器不可见的地方。JIT编译器生成的汇编指令,多了一行lock前缀的指令,作用是这个变量所在缓存行的数据写回到系统内存。每个处理器通过嗅探在总线上传播的数据来检查自己缓存的值是不是过期，置为无效。
	c) 禁止指令重排(Instruction Reorder),包含编译器和运行时指令重排。
	R) http://www.infoq.com/cn/articles/ftf-java-volatile

#### 4、ThreadLocal的用法#### 

	关键字:静态key,每个线程不同的value; 线程局部变量。Thread对象有个实例变量java.lang.Thread.threadLocals,类型是ThreadLocalMap,是ThreadLocal的内部类。理解为map,ThreadLocal对象就是map的key。initialValue方法，在首次调用get时会被调用。
	常用：com.ibatis.sqlmap.engine.impl.SqlMapClientImpl.localSqlMapSession、hibernate.session。
	ThreadLocal和Synchonized都用于解决多线程并发访问。但是ThreadLocal与synchronized有本质的区别。Synchronized用于线程间的数据共享，而ThreadLocal则用于线程间的数据隔离。
#### 5、IllegalMonitorStateException#### 

	wait/notify/notifyAll ,在没有获得锁的情况下,想要释放锁或是唤起其他线程获得锁。

#### 6、Thread.isInterrupted() 和 interrupted()区别#### 
	interrupted()静态方法,清理中断状态。isInterrupted,不清理中断状态。2个方法其实调用的同一个native方法
	private native boolean isInterrupted(boolean ClearInterrupted);


#### 7、使用notify() 还是 notifyAll()#### 
	关键字: block状态/wait状态
	单一条件的时候notify(),否则notifyAll()
	例: size = 1 的buffer,按照下面的顺序
	P1
	P2,P3 wait
	C1
	C2,C3 block
	C1->P2
	P2,C2,C3竞争 C2 wati C3wait
	P2->P3 P3wait
	3个都wait

#### 8、Synchronized关键字锁的是什么对象#### 
	
	a) 对于同步方法，锁是当前示例的对象。
	b) 对于静态同步方法，锁是当前对象的Class对象。
	c) 对于同步方法块，锁是Synchonized括号里配置的对象。

#### 9、Callable和Runnable有什么区别#### 
	
	a) 两个接口,Callable的方法是call,Runnable的方法是run。
	b) Runnable作为基本的任务表示形式，但有一定的局限性：不能返回一个值或是跑出一个受检查的异常。
	c) Callable是一个更好的抽象：它认为主入口点(即call)将返回一个值,并可能抛出一个异常。
	d) Callable和Runnalbe都可以应用于Executors框架,Thread只支持Runnable。

#### 10、Synchronized和Lock的区别#### 
	
	a) Lock是接口,Synchronized是关键字,内置锁。
	b) Synchronized是JVM软件层面的实现，Lock依赖于机器指令。CAS  ??
	c) Lock提供了轮询锁、定时锁、可中断锁、非结构加锁、读写锁、公平锁。
	d) Synchronized自动释放锁。lock一般要在finally手动释放。

#### 11、预防和防止数据库死锁 ####
	
	a) 避免并行的占用多个锁、多个资源。比如，某些业务可以不使用事务。
	b) 如果一定是事务的，尝试在事务中，获取锁的顺序一致。
	c) 缩小锁的范围，将大的事务分解为几个小事务。
	d) 缩短占锁的时间,事务时间。 
	d) 使用乐观锁代替独占锁。

	
