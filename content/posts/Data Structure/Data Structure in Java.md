---
title: "Data Structure In Java"
date: 2021-10-06T18:30:40+08:00
draft: true
toc: false
images:
  - "/images/totoro.jpeg"
tags: 
  - Java
---

According to the properties they possess, data types are divided into two groups:

#### **Primitive Data Types:**

 A primitive data type is pre-defined by the programming language. The size and type of variable values are specified, and it has no additional methods. 

* **byte, short, int, long, float, double, char, boolean.**

![DataTypes - Data types in Java - Edureka](https://www.edureka.co/blog/wp-content/uploads/2017/04/Primitive_Data_Type.png)

#### **Non-Primitive Data Types: ** 

![Java Collections](https://beginnersbook.com/wp-content/uploads/2013/12/Java-collection-framework-hierarchy.png)

These data types are not actually defined by the programming language but are created by the programmer, they have additional methods.

![Non Primitive data types - Data types in Java - Edureka](https://www.edureka.co/blog/wp-content/uploads/2019/06/Picture4-3.png)

{{< figure src="https://docs.oracle.com/javase/tutorial/figures/collections/colls-coreInterfaces.gif" alt="image" caption="The core collection interfaces">}}

[java.lang](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/package-summary.html): 

*  [Byte](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Byte.html), [Short](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Short.html), [Integer](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Integer.html), [Long](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Long.html), [Float](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Float.html), [Double](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Double.html), [Character](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Character.html), [Boolean](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Boolean.html).
* java.lang.Sting: [String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html).
* [java.lang.reflect](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/reflect/package-summary.html): [Array](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/reflect/Array.html) .

[java.util](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/package-summary.html): Interface:

![Screenshot 2021-10-11 at 12.49.02.png](https://i.loli.net/2021/10/11/BMOvJ6Fg89VbsTS.png)

* [List](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/List.html)<E>:  [LinkedList](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/LinkedList.html)<E>, [ArrayList](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/ArrayList.html)<E>，[Vector](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Vector.html)<E> <--  [Stack](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Stack.html)<E>

* [Set](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Set.html)<E>:   [HashSet](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashSet.html)<E>, [LinkedHashSet](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/LinkedHashSet.html)<E>`,[TreeSet](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/TreeSet.html)<E>.

* [Queue](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Queue.html)<E>:  [Deque](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html)<E>, [PriorityQueue](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/PriorityQueue.html)<E>.

* [Map](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Map.html)<K,V>: [HashMap](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashMap.html)<K,V>, [Hashtable](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Hashtable.html)<K,V>,  [LinkedHashMap](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/LinkedHashMap.html)<K,V>, [TreeMap](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/TreeMap.html)<K,V>

![img](https://miro.medium.com/max/2000/1*RyCRTcbKIxHiPe5AObrvqQ.png)

#### The difference between **primitive** and **non-primitive** data types are as follows:

1. Primitive types are predefined in [Java](https://www.edureka.co/blog/what-is-java/). Non-primitive types are created by the programmer.
2. Non Primitive types can be used to call methods to perform certain operations, while primitive types cannot.
3. A primitive type always has a value, whereas non-primitive types can be null.
4. A primitive type starts with a lowercase letter, while non-primitive types start with an uppercase letter.
5. The size of a primitive type depends on the data type, while non-primitive types have all the same size.

很多人说编程等于 数据结构 + 操作数据的算法，不一定是完全正确的，但是先学习整体框架，再一个个深入了解。可能开始会觉得学的很慢，怎么还不能写一个东西出来，但等到把基础知识掌握牢靠后，后面的面向对象编程，学起来就会更加得心应手。

大学老师是没有教Java官方文档，也并没有从头给我们讲解Java的语言框架，开始就是面向对象编程，和一些Java 语法，导致后来很多问题都学的很困惑，比如为什么 `int[] a = {1,2,3}` 不需要new， `ArrayList<Integer> a = new ArrayList<>()` 需要new？为什么会有 `a.lenght` 和`a.size()`，为什么一个需要后面加括号，一个不需要？`List<Integer> a = new Arraylist<>() `和 `ArrayList<Integer> a = new ArrayList<>()`有什么区别？等等这些问题都是看官方文档后，才开始慢慢理解的。
