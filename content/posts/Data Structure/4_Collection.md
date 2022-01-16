---
title: "Java Data Structure 4: Collection"
date: 2022-01-04T15:00:11+08:00
draft: true
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Data Structure

---

**Java Collection Framework** 是 Java语言最重要的特性，也是Java面试无法躲避的内容，可以说没有collection framework 我们就无法开发出任何产品级别的软件。

因为 collection framework 所有的 类和接口都存放在 **Java.util.package** 包里， 所以最初被称为 **Java.util.package** or **Collection API**, 后来 Sun Microsystem 在 Java 1.2 中 开始正式引入 collection framework。

### What is Collection in Java?

A collection is a group of objects. In Java, these objects are called elements of the collection. Technically, a collection is an object or container which stores a group of other objects as a single unit or single entity. Therefore, it is also known as container object or collection object in java. A container object means it contains other objects. In simple words, a collection is a container that stores multiple elements together.

Collection 就是一个可以容纳很多各种各样的对象的容器。

### What is Collections Framework in Java?

A framework in java is a set of several classes and interfaces which provide a ready-made architecture.

java框架是一组提供现成架构的类和接口。

In simple words, a collections framework is a class library to handle groups of objects. It is present in java.util package. It allows us to store, retrieve, and update a group of objects.

简单来说，集合框架是一个处理对象组的类库。它存在于 java.util 包中。它允许我们存储、检索和更新一组对象。

Collections framework in Java supports two types of containers:

- One for storing a collection of elements (objects), that is simply called a collection.
- The other, for storing key/value pairs, which is called a map.

Java 中的集合框架支持两种类型的容器：

- 一个用于存储元素（对象）的集合，简称为集合。
- 另一个，用于存储键/值对，称为映射。



![Screenshot 2021-10-11 at 12.49.02.png](https://i.loli.net/2021/10/11/BMOvJ6Fg89VbsTS.png)

### List of Interfaces defined in java.util package

| Collection    | List         | Queue        |
| ------------- | ------------ | ------------ |
| Comparator    | ListIterator | RandomAccess |
| Deque         | Map          | Set          |
| Enumeration   | Map.Entry    | SortedMap    |
| EventListener | NavigableMap | SortedSet    |
| Formattable   | NavigableSet |              |
| Iterator      | Observer     |              |

### List of classes defined in java.util package

| AbstractCollection | EventObject            | Random          |
| ------------------ | ---------------------- | --------------- |
| AbstractList       | FormattableFlags       | ResourceBundle  |
| AbstractMap        | Formatter              | Scanner         |
| AbstractQueue      | AbstractSequentialList | HashMap         |
| AbstractSet        | HashSet                | Stack           |
| ArrayDeque         | Hashtable              | StringTokenizer |
| ArrayList          | LinkedList             | Vector          |
| Collections        | EnumMap                | EnumSet         |
| Calender           | LinkedHashMap          | TreeMap         |

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201062015575.png)

***e➝ extends, I➝ implements***

---



![Two interface trees, one starting with Collection and including Set, SortedSet, List, and Queue, and the other starting with Map and including SortedMap.](https://docs.oracle.com/javase/tutorial/figures/collections/colls-coreInterfaces.gif)

- `Collection` — the root of the collection hierarchy. A collection represents a group of objects known as its *elements*. The `Collection` interface is the least common denominator that all collections implement and is used to pass collections around and to manipulate them when maximum generality is desired. Some types of collections allow duplicate elements, and others do not. Some are ordered and others are unordered. The Java platform doesn't provide any direct implementations of this interface but provides implementations of more specific subinterfaces, such as `Set` and `List`. Also see [The Collection Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/collection.html) section.

- `Set` — a collection that cannot contain duplicate elements. This interface models the mathematical set abstraction and is used to represent sets, such as the cards comprising a poker hand, the courses making up a student's schedule, or the processes running on a machine. See also [The Set Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/set.html) section.

- `List` — an ordered collection (sometimes called a *sequence*). `List`s can contain duplicate elements. The user of a `List` generally has precise control over where in the list each element is inserted and can access elements by their integer index (position). If you've used `Vector`, you're familiar with the general flavor of `List`. Also see [The List Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/list.html) section.

- Queue — a collection used to hold multiple elements prior to processing. Besides basic Collection operations, a Queue provides additional insertion, extraction, and inspection operations.

  Queues typically, but do not necessarily, order elements in a FIFO (first-in, first-out) manner. Among the exceptions are priority queues, which order elements according to a supplied comparator or the elements' natural ordering. Whatever the ordering used, the head of the queue is the element that would be removed by a call to `remove` or `poll`. In a FIFO queue, all new elements are inserted at the tail of the queue. Other kinds of queues may use different placement rules. Every `Queue` implementation must specify its ordering properties. Also see [The Queue Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/queue.html) section.

- Deque — a collection used to hold multiple elements prior to processing. Besides basic Collection operations, a Deque provides additional insertion, extraction, and inspection operations.

  Deques can be used both as FIFO (first-in, first-out) and LIFO (last-in, first-out). In a deque all new elements can be inserted, retrieved and removed at both ends. Also see [The Deque Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/deque.html) section.

- `Map` — an object that maps keys to values. A `Map` cannot contain duplicate keys; each key can map to at most one value. If you've used `Hashtable`, you're already familiar with the basics of `Map`. Also see [The Map Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/map.html) section.



The `Collection` interface contains methods that perform basic operations, such as **`int size()`, `boolean isEmpty()`, `boolean contains(Object element)`, `boolean add(E element)`, `boolean remove(Object element)`, and `Iterator<E> iterator()`.**

It also contains methods that operate on entire collections, such as **`boolean containsAll(Collection<?> c)`, `boolean addAll(Collection<? extends E> c)`, `boolean removeAll(Collection<?> c)`, `boolean retainAll(Collection<?> c)`, and `void clear()`.**

Additional methods for array operations (such as **`Object[] toArray()` and `<T> T[] toArray(T[] a)`** exist as well.

---

Collection所有的 object 的 methods 都是一层一层继承自父类的，

- ### Methods declared in interface java.util.[Collection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Collection.html)

  ```java
  parallelStream, removeIf, stream, toArray
  ```

- 

  ### Methods declared in interface java.lang.[Iterable](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Iterable.html)

  ```java
  forEach
  ```

例如  ArrayList.methods = Iterable.methods + Collection.methods + List.methods + ArrayList.methods 

```java
List<?> list = new ArrayList<>(); // list 只可以使用Collection和List的方法

ArrayList<?> arraylist = new ArrayList<>(); //arraylist 可以使用所有Colleciton,List & ArrayList 的方法。

// 虽然 declare List 不可以使用arraylist的私有方法，但是在真实案例中 在需要的时候更容易转换object的类型
// 例如：
List<String> a = new ArrayList<>();
a = new LinkedList<>();

List<String> b = new LinkedList<>();
b = new ArrayList<>();
```



**The `toArray` methods are provided as a bridge between collections and older APIs that expect arrays on input.**

```java
Object[] a = c.toArray();
String[] a = c.toArray(new String[0]);
```

Example String LinkedList to String Array:

```java
List<String> linkedList = new LinkedList<String>();

linkedList.add("Hello");
linkedList.add("world");
linkedList.add("!");

String[] str = linkedList.toArray(new String[0]);

System.out.println(linkedList);
for(String s : str) System.out.println(s);
System.out.println(str[1]);
```

```java
> Task :ListTest.main()
[Hello, world, !]
Hello
world
!
world
```



---



**Q.** Does a collection object store copies of other objects?

**A:** No, a collection object works with reference types. It stores references of other objects, not copies of other objects.

**Q.** Can we store a primitive data type into a collection?

**A:** No, collections store only objects.



---

- ### Methods declared in interface java.util.[Collection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Collection.html)

  ```java
  addAll, clear, contains, containsAll, equals, hashCode, isEmpty, iterator, parallelStream, remove, removeAll, removeIf, retainAll, size, spliterator, stream, toArray, toArray, toArray
  ```

- 

  ### Methods declared in interface java.lang.[Iterable](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Iterable.html)

  ```java
  forEach
  ```

  

---

### Summary

The Java Collections Framework hierarchy consists of two distinct interface trees:

- The first tree starts with the `Collection` interface, which provides for the basic functionality used by all collections, such as `add` and `remove` methods. Its subinterfaces — `Set`, `List`, and `Queue` — provide for more specialized collections.
- The **`Set`** interface does **not allow duplicate elements.** This can be useful for storing collections such as a deck of cards or student records. The `Set` interface has a **subinterface**, **`SortedSet`**, that provides for **ordering of elements** in the set.
- The **`List`** interface provides for an ordered collection, for situations in which you need precise control over where each element is inserted. You can retrieve elements from a `List` by their exact position.
- The **`Queue`** interface enables additional insertion, extraction, and inspection operations. Elements in a `Queue` are typically ordered in on a **FIFO** basis.
- The **`Deque`** interface enables insertion, deletion, and inspection operations at **both the ends**. Elements in a `Deque` can be used in **both LIFO and FIFO**.
- The second tree starts with the **`Map`** interface, which maps keys and values similar to a `Hashtable`.
- `Map`'s **subinterface**, **`SortedMap`**, maintains its key-value pairs in **ascending order** or in an order specified by a `Comparator`.

These interfaces allow collections to be manipulated independently of the details of their representation.
