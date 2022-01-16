---
title: "Java Data Structure 5: Collection_List"
date: 2022-01-05T16:00:11+08:00
draft: true
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Data Structure

---

**Module** [java.base](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/module-summary.html)

**Package** [java.util](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/package-summary.html)

## Interface List<E>

- - **Type Parameters:**

    `E` - the type of elements in this list

  - All Superinterfaces:

    `Collection<E>`, `Iterable<E>`

  - All Known Implementing Classes:

    `AbstractList`, `AbstractSequentialList`, **`ArrayList`**, `AttributeList`, `CopyOnWriteArrayList`, **`LinkedList`**, `RoleList`, `RoleUnresolvedList`, **`Stack`**, **`Vector`**

```java
public interface List<E> extends Collection<E>
```

the** `List`** interface includes operations method for the following:

- `Positional access` — manipulates elements based on their numerical position in the list. This includes methods such as **`get`, `set`, `add`, `addAll`, and `remove`**.
- `Search` — searches for a specified object in the list and returns its numerical position. Search methods include **`indexOf` and `lastIndexOf`**.
- `Iteration` — extends `Iterator` semantics to take advantage of the list's sequential nature. The **`listIterator`** methods provide this behavior.
- `Range-view` — The **`sublist`** method performs arbitrary *range operations* on the list.

The Java platform contains two general-purpose `List` implementations. [`ArrayList`](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html), which is usually the better-performing under access and search, and [`LinkedList`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html) which offers better performance under insert and delete.

---

## How to create a List in Java?

```java
List<String> arrayList = new ArrayList<>();
List<Integer> linkedList = new LinkedList<>();
List<Object> vector = new Vector<>();
List<?> stack = new Stack<>();
```

## When to use List?

\1. List can be used when we want to allow or store duplicate elements. 允许存储重复元素
\2. It can be used when we want to store null elements. 允许存储 null 元素
\3. When we want to preserve my insertion order, we should go for list.  可以保持元素插入顺序



---

## ArrayList

```java
java.util.ArrayList<E>

public class ArrayList<E>
extends AbstractList<E>
implements List<E>, RandomAccess, Cloneable, Serializable // 可以实现List
```

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201121247012.png)

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201062043165.png)

ArrayList类底层数据结构为数组**Array**，初始化大小：DEFAULT-CAPACITY=10，扩容方式：oldCapacity+oldCapacity>>1,即**1.5倍**扩容。数据有序性；可添加多个null值。

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

对ArrayList进行添加元素的操作的时候是分两个步骤进行的，即第一步先在object[size]的位置上存放需要添加的元素；第二步将size的值增加1。由于这个过程在多线程的环境下是不能保证具有原子性的，因此ArrayList在多线程的环境下是**线程不安全**的。

线程不安全, 多线程问题需要使用 `synchronizedList`  进行封装：

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201101301158.png)



```java
ArrayList<String> al = new ArrayList<String>(); // Non-synchronized.
List l = Collections.synchronizedList( al ); // synchronized

// Collection synchronized method 1
List<String> synlist = Collections.synchronizedList( new ArrayList<String>); 
// Collection synchronized method 2
CopyOnWriteArrayList<String> al = new CopyOnWriteArrayList<String>(); 
```



Similarly, we can get the synchronized version of Set, Map objects by using the following syntax:

```java
public static Set synchronizedList( Set s );
public static Map synchronizedList( Map m );
```





---

## LinkedList

```java
java.util.LinkedList<E>

public class LinkedList<E>
extends AbstractSequentialList<E>
implements List<E>, Deque<E>, Cloneable, Serializable // 可以实现List, Deque
```

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201121248412.png)

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201101448421.png)

**LinkedList**的底层实现是**双向链表Doubly-linked list**，链表以节点为单位，每个元素都是一个独立对象，在内存空间的存储是非连续的。链表的节点对象具有两个成员变量：「值 `val`」，「后继节点引用 `next`」 。 可实现Stacks, Queues, and trees等数据结构。

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

> LinkedList 继承了 AbstractSequentialList 类。
>
> LinkedList 实现了 Queue 接口，可作为队列使用。
>
> LinkedList 实现了 List 接口，可进行列表的相关操作。
>
> LinkedList 实现了 Deque 接口，可作为队列使用。
>
> LinkedList 实现了 Cloneable 接口，可实现克隆。
>
> LinkedList 实现了 java.io.Serializable 接口，即可支持序列化，能通过序列化去传输。

### `Deque` 

用 LinkedList 实现Deque:

```java
Deque<String> deque = new LinkedList<>();

deque.add("Love ");// Love
deque.addFirst("I "); // I Love
deque.addLast("You!"); // I Love You! 
deque.push("lol "); // lol I Love You!
deque.pop(); // I Love You!
deque.peek(); // I
deque.poll(); // Love You!
```



---



## ArrayList vs LinkedList

> * ArrayList **底层是数组Array,内存地址连续可随机访问元素，查询快O(1),**
> * ArrayList **动态扩容和元素拷贝 增删慢, 实现了List 接口;**
> * LinkedList **底层是链表List,内存地址不连续必须按顺序访问元素，查询慢O(N),**
> * LinkedList **只需要修改节点指针指向 增删快O(1), 实现List & Deque 接口。**  

## 

## ArrayList vs Array

> * Array长度`length()`是固定的，需要提前申明初始化数组的大小; ArrayList大小`size()`是可以动态增加的。
> * Array可以存储primitives原始数据类型`int, char`和object; ArrayList只可以存储object。
> * Array不能随意增删其中的项，ArrayList提供更多的方法和特性去处理数据，例如`add(),remove()`
> * Array处理固定长度的数据时速度更快，在不确定数据大小的时候ArrayList更方便和节省内存空间。
> * ArrayList的底层数据结构是Array.

```java
public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        int[] array = new int[3];
        array[0] = 1;
        array[1] = 2;
        System.out.println(Arrays.toString(array));
        // [1, 2, 0]
        list.add(1);
        list.add(2);
        list.remove(1);
        System.out.println(list);
        // [1]
}
```

---

## Vector

```java
public class Vector<E>
extends AbstractList<E>
implements List<E>, RandomAccess, Cloneable, Serializable // 实现 list
```

- All Implemented Interfaces:

  `Serializable`, `Cloneable`, `Iterable<E>`, `Collection<E>`, `List<E>`, `RandomAccess`

- Direct Known Subclasses:

  **`Stack`**

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201121302194.png)



**Vector class in Java** was introduced in JDK 1.0 version. It is present in Java.util package. It is a dynamically resizable array (growable array) which means it can grow or shrink as required.

Java Vector class is similar to [ArrayList class](https://www.scientecheasy.com/2020/09/arraylist-in-java.html/) with two main differences.

- Vector is synchronized. It is used for thread safety.
- It contains many legacy methods that are not now a part of the collections framework.



创建 Vector 方法：  

```java
Vector<Integer> vector1 = new Vector<>();
Vector<Integer> vector2 = new Vector(initialCapacity: 10, capacityIncrement: 5); //可以只放capacity
Vector<Integer> vector3 = new Vector(Collection c); //只可以添加 collection 类 
```



**When to Use Vector?**

➤ We are developing a multi-threaded application but it can reduce the performance of the application because it is “thread-safety”.

Vector  是线程安全的，当我们需要多线程问题下开发可以考虑使用它。

 **Why sing `Vector` is considered to be a bad thing in most contexts. 为什么不要使用vector**

- `Vector` synchronizes on every operation. Most contexts do not require fine-grained synchronization, and as such it is an unwanted performance overhead. 每一个步骤都需要同步，效率低。
- The `Vector.elements()` method returns an `Enumeration` which does not have fail-fast semantics. 返回枚举类，速度慢。

如果涉及线程安全问题，我们可以使用 Collections.synchronizedList 来代替，避免使用vector.



----



## Difference between ArrayList and Vector in Java

| ArrayList                                                    | Vector                                                       |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| ArrayList is not synchronized.                               | Vector is synchronized.                                      |
| Since ArrayList is not synchronized. Hence, its operation is faster as compared to vector. | Vector is slower than ArrayList.                             |
| ArrayList was introduced in JDK 2.0.                         | Vector was introduced in JDK 1.0.                            |
| ArrayList is created with an initial capacity of 10. Its size is increased by 50%. | Vector is created with an initial capacity of 10 but its size is increased by 100%. |
| In the ArrayList, Enumeration is fail-fast. Any modification in ArrayList during the iteration using Enumeration will throw ConcurrentModificatioException. | Enumeration is fail-safe in the vector. Any modification during the iteration using Enumeration will not throw any exception. |

---

### Stack

```java
public class Stack<E>
extends Vector<E>
```

The `Stack` class represents a last-in-first-out (LIFO) stack of objects. It extends class `Vector` with five operations that allow a vector to be treated as a stack. The usual `push` and `pop` operations are provided, as well as a method to `peek` at the top item on the stack, a method to test for whether the stack is `empty`, and a method to `search` the stack for an item and discover how far it is from the top.

`Stack`类表示对象的后进先出（LIFO）堆栈。提供了常用的 `push`和`pop`操作，以及`peek`在堆栈顶部项目的方法，测试堆栈是否为`empty`的方法，`search` 以及对项目的堆栈并发现它离顶部多远的方法。

A more complete and consistent set of LIFO stack operations is provided by the [`Deque`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html) interface and its implementations, which should be used in preference to this class. For example:

[`Deque`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html)接口及其实现提供了一组更完整和一致的 LIFO 堆栈操作，应优先使用此类。

```
Deque<Integer> stack = new ArrayDeque<Integer>();
```