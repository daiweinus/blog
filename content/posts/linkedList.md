---
title: "LinkedList"
date: 2021-10-20T11:05:33+08:00
draft: true
toc: false
images:
  - "/images/totoro.jpeg"
tags: 
  - java
---

```java
Module java.base
Package java.util

java.lang.Object
java.util.AbstractCollection<E>
java.util.AbstractList<E>
java.util.AbstractSequentialList<E>
java.util.LinkedList<E>
  
public class LinkedList<E>
extends AbstractSequentialList<E>
implements List<E>, Deque<E>, Cloneable, Serializable
```

![](https://img-blog.csdnimg.cn/20190227211326757.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NhcnRvb25f,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/img_convert/81117006f63098c29cceb5938fdc3199.png)

链表以节点为单位，每个元素都是一个独立对象，在内存空间的存储是非连续的。链表的节点对象具有两个成员变量：「值 `val`」，「后继节点引用 `next`」 。 可实现Stacks, Queues, and trees等数据结构。

```java
class ListNode {
    int val;       // 节点值
    ListNode next; // 后继节点引用
    ListNode(int x) { val = x; }
}
```

和ArrayList 一样，下面两种ArrayList初始化方式都是正确的，List is an **`interface`** and LinkedList is a **`class`**. 

```java
List<String> list1 = new LinkedList<>(); //generally preferred
LinkedList<String> list2 = new LinkedList<>(); // type-cast
```

`List<E>` is more generally preferred over `LinkedList<E>`, but If needed to add cells in the beginning/middle/end of the list LinkedList proved you  _`addFirst, addLast & removeFirst, removeLast & getFirst, getLast`_ method.

```java
list2.add(1); // list[1]
list2.addFirst(2); // list[2,1]     
list2.removeLast(); // list[2]
list2.getFirst(); // 2
```

## 
