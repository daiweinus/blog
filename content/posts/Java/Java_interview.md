---
title: "Java Interview Questions"
date: 2021-12-28T15:25:50+08:00
draft: true
toc: false
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Interview
---

## 一、开场介绍
自我介绍。

项目经验。

数据结构:

Arraylist vs Linklist

HashSet vs HashMap

Binary Tree vs Binary Search Tree

## 二、JVM
垃圾回收算法有几种类型？ 他们对应的优缺点又是什么？
类的加载过程是什么？简单描述一下每一个步骤
JVM 预约义的类加载器有哪几种？分别什么做用？
什么是双亲委派模式？有什么做用？
什么是内存溢出， 内存泄露？ 他们的区别是什么？
引发类加载操做的行为有哪些？
介绍一下 JVM 提供的经常使用工具
Full GC 、 Major GC 、Minor GC 之间区别？
何时触发 Full GC ？

## 三、Java并发
什么是可重入锁、乐观锁、悲观锁、公平锁、非公平锁、独占锁、共享锁？
讲讲ThreadLocal 的实现原理？
ThreadLocal 做为变量的线程隔离方式，其内部是如何作的？
说说InheritableThreadLocal 的实现原理？
并发包中锁的实现底层（对AQS的理解）？
讲讲独占锁 ReentrantLock 原理？

## 四、Java集合
HashSet 和 TreeSet 有什么区别？
HashSet 的底层实现是什么?
LinkedHashMap 的实现原理?
为何集合类没有实现 Cloneable 和 Serializable 接口？
什么是迭代器 (Iterator)？
Iterator 和 ListIterator 的区别是什么？

## 五、Spring全家桶
 Spring bean的生命周期能不能结合源码回答一下这个问题、或者结合一下bean的生命的意义来回答，就是Spring为何须要找个生命周期

Spring容器当中包含了哪些常用组件（至少说5个），作用是什么，场景是什么；比如BeanDefinition；再比如BeanDefinitionMap

Spring自动注入的原理是什么？能不能从源码来说明一下这个问题；我们常常说的自动注入，到底怎么注入的？有什么坑？怎么让你一个属性不自动注入

Spring源码当中如何来搞定循环依赖的？Spring支持循环依赖？生命情况不支持？支持的原理是什么？能不能从源码来说明一下？

如何来二次扩展Spring，比如自定义一个实现自动注入的注解；不使用@Autowried，自己如何开发一个@XXX来完成自动注入？ 

mybatis源码当中利用了Spirng的那些扩展？mybatis扩展Spring以后有哪些问题是没法解决的？好比二级缓存怎么解决

eureka源码当中如何扩展的Spring？好比怎么动态插拔eureka的功能，利用了Spring的那个技术点，或者从源码说一下 

## 六、Redis
Redis 持久化机制有哪些？ 区别是什么？优缺点是什么？

Redis支持的数据类型

为何 Redis 须要把全部数据放到内存中？

Redis 是单线程的吗？

Redis 的缓存失效策略有哪几种？

什么是缓存命中率？提升缓存命中率的方法有哪些？

Redis全局命令及数据库管理

Redis设计订单应用场景

Redis缓存雪崩讲讲看？

什么是缓存穿透？

Redis重启时加载AOF与RDB的顺序

## 七. 中间件
Dubbo完整的一次调用链路介绍；

Dubbo支持几种负载均衡策略？

Dubbo Provider服务提供者要控制执行并发请求上限，具体怎么作？

Dubbo启动的时候支持几种配置方式？

了解几种消息中间件产品？各产品的优缺点介绍；

消息中间件如何保证消息的一致性和如何进行消息的重试机制？

Spring Cloud熔断机制介绍；

Spring Cloud对比下Dubbo，什么场景下该使用Spring Cloud？

## 八、分布式
消息中间件如何解决消息丢失问题

Dubbo的服务请求失败怎么处理

重连机制会不会形成错误

对分布式事务的理解

如何实现负载均衡，有哪些算法能够实现？

Zookeeper的用途，选举的原理是什么？

数据的垂直拆分水平拆分。

zookeeper原理和适用场景

zookeeper watch机制

redis/zk节点宕机如何处理

分布式集群下如何作到惟一序列号

如何作一个分布式锁

用过哪些MQ，怎么用的，和其余mq比较有什么优缺点，MQ的链接是线程安全的吗

MQ系统的数据如何保证不丢失

列举出你能想到的数据库分库分表策略；分库分表后，如何解决全表查询的问题。

## 九、数据库
MySQL InnoDB存储的文件结构

索引树是如何维护的？

数据库自增主键可能的问题

MySQL的几种优化

mysql索引为何使用B+树

数据库锁表的相关处理

索引失效场景

高并发下如何作到安全的修改同一行数据，乐观锁和悲观锁是什么，INNODB的行级锁有哪2种，解释其含义

数据库会死锁吗，举一个死锁的例子，mysql怎么解决死锁

## 十、计算机网络

OSI vs TCP/IP Model

TCP vs UDP Protocol

Http vs Https

IPv4 vs IPv6

3 ways handshake connection

4 ways handshake disconnection

What happen after your type 'google.com' in the borrower

DNS / MAC

## 十一、算法

Leetcode