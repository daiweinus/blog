---
title: "arrayList vs linkedList"
date: 2021-10-20T11:11:34+08:00
draft: true
toc: false
images:
  - "totoro.jpeg"
tags: 
  - java
---

## ArrayList vs LinkedList

![img](https://static.studytonight.com/data-structures/images/array-vs-linked-list.png)

> * ArrayList **底层是数组,内存地址连续可随机访问元素，查询快O(1),**
> * ArrayList **动态扩容和元素拷贝 增删慢, 实现了List 接口;**
> * LinkedList **底层是链表,内存地址不连续必须按顺序访问元素，查询慢O(N),**
> * LinkedList **只需要修改节点指针指向 增删快O(1), 实现List & Deque 接口。**  

