---
title: "Java Data Structure 8: Map"
date: 2022-01-08T16:00:11+08:00
draft: true
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Data Structure

---

**Module** [java.base](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/module-summary.html)

**Package** [java.util](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/package-summary.html)

## Interface Map<K,V>

- - **Type Parameters:**

    `K` - the type of keys maintained by this map

    `V` - the type of mapped values

  - **All Known Subinterfaces:**

    `Bindings`, `ConcurrentMap<K,V>`, `ConcurrentNavigableMap<K,V>`, `NavigableMap<K,V>`, `SortedMap<K,V>`

  - **All Known Implementing Classes:**

    `AbstractMap`, `Attributes`, `AuthProvider`, **`ConcurrentHashMap`**, `ConcurrentSkipListMap`, `EnumMap`, **`HashMap`**, **`Hashtable`**, `Headers`, `IdentityHashMap`, **`LinkedHashMap`**, `PrinterStateReasons`, `Properties`, `Provider`, `RenderingHints`, `ScriptObjectMirror`, `SimpleBindings`, `TabularDataSupport`, **`TreeMap`**, `UIDefaults`, `WeakHashMap`

  ------

  ```java
  public interface Map<K,V>
  ```

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201122005617.png)

A **map in Java** is a container object that stores elements in the form of key and value pairs. A key is a unique element (object) that serves as an “index” in the map.

A map **cannot have duplicate keys**, but values may be duplicate.

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201122004768.png)

- ### Methods declared in interface java.util.[Map](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Map.html)

  ```java
  clear, containsKey, containsValue, entrySet, equals, get, hashCode, isEmpty, keySet, put, putAll, remove, size, values
  ```

**Key point:** The main difference between maps and sets is that **maps contain keys and values**, whereas **sets contain only keys.**



Map接口的实现。它们如下:

**1、AbstractMap：**是实现map接口的抽象类。它是HashMap、TreeMap、LinkedHashMap等所有具体地图实现类的父类。它实现了 Map 接口中除了 entrySet() 方法之外的所有方法。

**2. [EnumMap](https://www.scientecheasy.com/2020/12/enummap-in-java.html/) :** EnumMap 类扩展了 AbstractMap 并实现了 Map 接口。它特别适用于 Enum 类型的键。

**3. [HashMap](https://www.scientecheasy.com/2020/11/hashmap-in-java.html/)：**它是一个扩展AbstractMap的具体类。它使用哈希表来存储元素。它主要用于定位值、插入和删除条目。

**4. [TreeMap](https://www.scientecheasy.com/2020/11/treemap-in-java.html/) :**扩展 AbstractMap 并实现 NavigableMap 接口的具体类。它使用树来存储元素。它用于按排序顺序遍历键。可以使用 Comparable 接口或 Comparator 接口对键进行排序。

**5. [LinkedHashMap](https://www.scientecheasy.com/2020/11/linkedhashmap-in-java.html/)：**是一个提供Java map接口实现的具体类。它使用支持映射中条目插入顺序的链表实现扩展了 HashMap 类。

HashMap 中的条目没有排序，但 LinkedHashMap 中的条目可以按照它们插入映射的顺序检索。

**6. [WeakHashMap](https://www.scientecheasy.com/2020/12/weakhashmap-in-java.html/) :** WeakHashMap 类扩展了 AbstractMap 接口以使用带有弱类型键的哈希表。弱键允许映射中的元素在其键不再在程序中的任何位置使用时被垃圾收集。

**7. [IdentityHashMap](https://www.scientecheasy.com/2020/12/identityhashmap-in-java.html/)：**这个类扩展了 AbstractMap 并使用引用相等来比较条目。此类不用于一般目的。

---

### Interface Map.Entry<K,V>

```java
public static interface Map.Entry<K,V>
```

The **Map.Entry interface** enables us to work on an entry in the map. An entry of a map is an object of type Map.Entry interface, where Entry is an inner interface of Map interface. 

The `Map.entrySet` method returns a collection-view of the map, whose elements are of this class.  

Map.Entry 是Map的封闭接口，可以在map 接口里操控 entry。 `Map.entrySet` 方法可以通过遍历返回map里的元素。

**Methods define in Map.Entry**

```java
comparingByKey(), comparingByValue(), equals(Object o), getKey(), getValue(), hashCode(), setValue(V value)
```

---

The general syntax to create a map object is as follows:

```java
a) Map<K, V> map = new HashMap<>(); // It create an empty map.
b) Map<K, V> map = new HashMap<>(Map m); // It creates a map with initializing elements of m.
c) Map<K, V> map = new HashMap<>(int initialCapacity); // It creates a map with initialization of initial capacity of HashMap.
d) Map<K, V> map = new HashMap<>(int initialCapacity, float fillRatio); // It creates a map object with initializing both initial capacity and fill ratio of HashMap.
```



----

## 

什么是Map? 在数组中我们是通过数组下标来对其内容索引的，而在Map中我们通过对象来对对象进行索引，用来索引的对象叫做key,其对应的对象叫做value.这就是我们平时说的键值对。

java.util 中的集合类包含 Java 中某些最常用的类。最常用的集合类是 List 和 Map。List 的具体实现包括 ArrayList 和 Vector，它们是可变大小的列表，比较适合构建、存储和操作任何类型对象元素列表。List 适用于按数值索引访问元素的情形。

Map 提供了一个更通用的元素存储方法。Map 集合类用于存储元素对（称作“键”和“值”），其中每个键映射到一个值。从概念上而言，您可以将 List 看作是具有数值键的 Map。而实际上，除了 List 和 Map 都在定义 java.util 中外，两者并没有直接的联系。

| Constructor                                      | Description                                                  |
| :----------------------------------------------- | :----------------------------------------------------------- |
| `HashMap()`                                      | Constructs an empty `HashMap` with the default initial capacity (16) and the default load factor (0.75). |
| `HashMap(int initialCapacity)`                   | Constructs an empty `HashMap` with the specified initial capacity and the default load factor (0.75). |
| `HashMap(int initialCapacity, float loadFactor)` | Constructs an empty `HashMap` with the specified initial capacity and load factor. |
| `HashMap(Map<? extends K,? extends V> m)`        | Constructs a new `HashMap` with the same mappings as the specified `Map`. |

**比较 Map 对象的等价性**

| `equals(Object o)` | 比较指定对象与此 Map 的等价性 |
| ------------------ | ----------------------------- |
| **`hashCode()`**   | 返回此 Map 的哈希码           |

**返回视图的 Map 方法：** 使用这些方法返回的对象，您可以遍历 Map 的元素，还可以删除 Map 中的元素。

| entrySet() | 返回 Map 中所包含映射的 Set 视图。Set 中的每个元素都是一个 Map.Entry 对象，可以使用 getKey() 和 getValue() 方法（还有一个 setValue() 方法）访问后者的键元素和值元素 |
| ---------- | ------------------------------------------------------------ |
| keySet()   | 返回 Map 中所包含键的 Set 视图。删除 Set 中的元素还将删除 Map 中相应的映射（键和值） |
| values()   | 返回 map 中所包含值的 Collection 视图。删除 Collection 中的元素还将删除 Map 中相应的映射（键和值） |

**访问元素**

| get(Object key)             | 返回与指定键关联的值                               |
| --------------------------- | -------------------------------------------------- |
| containsKey(Object key)     | 如果 Map 包含指定键的映射，则返回 true             |
| containsValue(Object value) | 如果此 Map 将一个或多个键映射到指定值，则返回 true |
| isEmpty()                   | 如果 Map 不包含键-值映射，则返回 true              |
| size()                      | 返回 Map 中的键-值映射的数目                       |

## Java 自带了各种 Map 类。这些 Map 类可归为三种类型：

- 通用 Map，用于在应用程序中**管理映射**，通常在 java.util 程序包中实现
  - **HashMap**
  - **Hashtable**
  - Properties
  - **LinkedHashMap**
  - IdentityHashMap
  - **TreeMap**
  - WeakHashMap
  - **ConcurrentHashMap**
- 专用 Map，您通常不必亲自创建此类 Map，而是**通过某些其他类对其进行访问**
  - java.util.jar.Attributes
  - javax.print.attribute.standard.PrinterStateReasons
  - java.security.Provider
  - java.awt.RenderingHints
  - javax.swing.UIDefaults
- 一个用于帮助实现您自己的 Map 类的**抽象类**
  - AbstractMap

---

### 调整 Map 实现的大小

在哈希术语中，内部数组中的每个位置称作“存储桶”(bucket)，而可用的存储桶数（即内部数组的大小）称作容量 (capacity)。为使 Map 对象有效地处理任意数目的项，Map 实现可以调整自身的大小。但调整大小的开销很大。调整大小需要将所有元素重新插入到新数组中，这是因为不同的数组大小意味着对象现在映射到不同的索引值。先前冲突的键可能不再冲突，而先前不冲突的其他键现在可能冲突。这显然表明，**如果将 Map 调整得足够大，则可以减少甚至不再需要重新调整大小，这很有可能显著提高速度**。

---

### 负载因子

为确定何时调整大小，而不是对每个存储桶中的链接列表的深度进行记数，基于哈希的 Map 使用一个额外参数并粗略计算存储桶的密度。Map 在调整大小之前，使用名为“负载因子”的参数指示 Map 将承担的“负载”量，即它的负载程度。负载因子、项数（Map 大小）与容量之间的关系简单明了：

- **如果（负载因子）x（容量）>（Map 大小），则调整 Map 大小**

例如，如果默认负载因子为 0.75，默认容量为 11，则 11 x 0.75 = 8.25，该值向下取整为 8 个元素。因此，如果**将第 8 个项添加到此 Map，则该 Map 将自身的大小调整为一个更大的值**。相反，要计算避免调整大小所需的初始容量，用将要添加的项数除以负载因子，并向上取整，例如，

- 对于负载因子为 0.75 的 100 个项，应将容量设置为 100/0.75 = 133.33，并将结果向上取整为 134（或取整为 135 以**使用奇数**）

**奇数个存储桶使 map 能够通过减少冲突数来提高执行效率**。虽然所做的测试（关联文件中的 并未表明质数可以始终获得更好的效率，但理想情形是容量取质数。1.4 版后的某些 Map（如 HashMap 和 LinkedHashMap，而非 Hashtable 或 IdentityHashMap）使用需要 2 的幂容量的哈希函数，但下一个最高 2 的幂容量由这些 Map 计算，因此您不必亲自计算。

**负载因子本身是空间和时间之间的调整折衷。较小的负载因子将占用更多的空间，但将降低冲突的可能性，从而将加快访问和更新的速度**。使用大于 0.75 的负载因子可能是不明智的，而使用大于 1.0 的负载因子肯定是不明知的，这是因为这必定会引发一次冲突。使用小于 0.50 的负载因子好处并不大，但只要您有效地调整 Map 的大小，应不会对小负载因子造成性能开销，而只会造成**内存开销**。但较小的负载因子将意味着如果您未预先调整 Map 的大小，则导致更频繁的调整大小，从而**降低性能**，因此在调整负载因子时一定要注意这个问题。

---

**为什么负载因子选择0.75？而不是0.5或者1.0？**

因为负载因子本身是空间开销和时间开销之间折衷选择。

较小的负载因子例如0.5，意味着将占用更多的内存，造成内存开销，而且较小的负载因子会导致map频繁调整大小，又造成性能开销。

而选择较大的负载因子例如1.0，则意味着只有当Map的内存被元素填满时才会调整大小，这样必定会引发冲突。

---

**为啥HashMap中初始化大小为什么是16呢？**

hahmap每次扩容都是以 2的整数次幂进行扩容

因为是将二进制进行按位于，(16-1) 是 1111,末位是1，这样也能保证计算后的index既可以是奇数也可以是偶数，并且只要传进来的key足够分散，均匀那么按位于的时候获得的index就会减少重复，这样也就减少了hash的碰撞以及hashMap的查询效率。

那么到了这里你也许会问？ 那么就然16可以，是不是只要是2的整数次幂就可以呢？

答案是肯定的。那为什么不是8,4呢？ 因为是8或者4的话很容易导致map扩容影响性能，如果分配的太大的话又会浪费资源，所以就使用16作为初始大小。

---

### 选择适当的 Map

应使用哪种 Map？ 它是否需要同步？ 要获得应用程序的最佳性能，这可能是所面临的两个最重要的问题。当使用通用 Map 时，调整 Map 大小和选择负载因子涵盖了 Map 调整选项。

**应使用哪种 Map？答案很简单：** 不要为您的设计选择任何特定的 Map，除非实际的设计需要指定一个特殊类型的 Map。设计时通常不需要选择具体的 Map 实现。您可能知道自己需要一个 Map，但不知道使用哪种。而这恰恰就是使用 Map 接口的意义所在。直到需要时再选择 Map 实现 — 如果随处使用“Map”声明的变量，则更改应用程序中任何特殊 Map 的 Map 实现只需要更改一行，这是一种开销很少的调整选择。

- 将您的所有 Map 变量声明为 Map，而不是任何具体实现，即不要声明为 HashMap 或 Hashtable，或任何其他 Map 类实现。

  ```java
  Map criticalMap = new HashMap(); //好
  
  HashMap criticalMap = new HashMap(); //差
  ```

- 这使您能够只更改一行代码即可非常轻松地替换任何特定的 Map 实例。

- 下载 Doug Lea 的 util.concurrent 程序包。将 ConcurrentHashMap 用作默认 Map。当移植到 1.5 版时，将 java.util.concurrent.ConcurrentHashMap 用作您的默认 Map。不要将 ConcurrentHashMap 包装在同步的包装器中，即使它将用于多个线程。使用默认大小和负载因子。

- 监测您的应用程序。如果发现某个 Map 造成瓶颈，则分析造成瓶颈的原因，并部分或全部更改该 Map 的以下内容：Map 类；Map 大小；负载因子；关键对象 equals() 方法实现。专用的 Map 的基本上都需要特殊用途的定制 Map 实现，否则通用 Map 将实现您所需的性能目标。



### Map的线程安全问题

1. 可以使用 `Collections.synchronizedMap()` 将未同步的 Map 转换为同步的 Map，但是维护复杂，执行效率很低。
2. Doug Lea 是纽约州立大学奥斯威戈分校计算机科学系的教授。他创建了一组公共领域的程序包（统称 util.concurrent），该程序包包含许多可以简化高性能并行编程的实用程序类。这些类中包含两个 Map，即 ConcurrentReaderHashMap 和 ConcurrentHashMap。这些 Map 实现是线程安全的。Java 1.5 版将把这些 Map 包含在一个新的 java.util.concurrent 程序包中。
3. 所以当面临线程安全问题时，只需要使用 ConcurrentHashMap。



---

### **HashMap和TreeMap比较**

（1）HashMap:适用于在Map中插入、删除和定位元素。

（2）Treemap:适用于按自然顺序或自定义顺序遍历键（key）。

（3）HashMap通常比TreeMap快一点（树和哈希表的数据结构使然），建议多使用HashMap,在需要排序的Map时候才用TreeMap.

（4）HashMap 非线程安全 TreeMap 非线程安全

（5）HashMap的结果是没有排序的，而TreeMap输出的结果是排好序的。

（6）HashMap底层基于数组+链表和红黑树实现，TreeMap底层基于红黑树 red-black-tree 实现。

　在HashMap中通过`get()`来获取value,通过`put()`来插入`value, ContainsKey()`则用来检验对象是否已经存在。可以看出，和ArrayList的操作相比，HashMap除了通过key索引其内容之外，别的方面差异并不大。

HashMap通过hashcode对其内容进行快速查找，而 TreeMap中所有的元素都保持着某种固定的顺序，如果你需要得到一个有序的结果你就应该使用TreeMap（HashMap中元素的排列顺序是不固定的）。



---

- ### Methods declared in class java.util.[HashMap](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashMap.html)

  ```
  clear, clone, compute, computeIfAbsent, computeIfPresent, containsKey, isEmpty, merge, put, putAll, remove, size
  ```

- 

  ### Methods declared in class java.util.[AbstractMap](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/AbstractMap.html)

  ```
  equals, hashCode, toString
  ```

- 

  ### Methods declared in class java.lang.[Object](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Object.html)

  ```
  finalize, getClass, notify, notifyAll, wait, wait, wait
  ```

- 

  ### Methods declared in interface java.util.[Map](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Map.html)

  ```java
  clear, compute, computeIfAbsent, computeIfPresent, containsKey, equals, forEach, getOrDefault, hashCode, isEmpty, merge, put, putAll, putIfAbsent, remove, remove, replace, replace, replaceAll, size
  ```

- ### Methods declared in interface java.util.[SortedMap](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/SortedMap.html)

  ```
  comparator
  ```