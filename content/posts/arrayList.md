---
title: "ArrayList"
date: 2021-10-20T10:52:00+08:00
draft: true
toc: false
images:
  - "/images/totoro.jpeg"
tags: 
  - Java
---

```java
Module java.base
Package java.util
  
java.lang.Object
java.util.AbstractCollection<E>
java.util.AbstractList<E>
java.util.ArrayList<E>
  
public class ArrayList<E>
extends AbstractList<E>
implements List<E>, RandomAccess, Cloneable, Serializable
```

![](https://img-blog.csdnimg.cn/20190227211326757.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NhcnRvb25f,size_16,color_FFFFFF,t_70)

![img](https://java2blog.com/wp-content/webpc-passthru.php?src=https://java2blog.com/wp-content/uploads/2016/05/ArrayList.jpg&nocache=1)

下面两种ArrayList初始化方式都是正确的，List is an **`interface`** and ArrayList is a **`class`**. 

```java
List<Integer> list1 = new ArrayList<>(); //generally preferred
ArrayList<Integer> list2 = ArrayList<>(); // type-cast
```

* initialize as **`List<E>`** 更加灵活flexible, preferable，可以随后选择 LinkedList or ArrayList.
* initialize as **`ArrayList<E>`** 可以访问使用所有的ArrayList class method, such as such as _`ArrayList#ensureCapacity`_ or _`ArrayList#trimToSize`_.
* 通常情况下，尽量使用方法1 **List<E>** 来初始化 arrayList.

```java
List<String> list = new ArrayList<>();// 初始化可变数组
list.add("one"); // list["one"]
list.add("two"); // list["one","two"]
list.remove(0); //list["two"]
list.add(1,4); //list["two",4]
boolean a = list.contains(2); //true
```

ArrayList的 **toArray** 方法返回一个数组, ArrayList的 **asList** 方法返回一个列表.

