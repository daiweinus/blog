---
title: "Java Data Structure 6: Collection_Set"
date: 2022-01-06T16:00:11+08:00
draft: true
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Data Structure

---

**Set** a unordered collection that contains no duplicate elements, and at most one null element.

**Set**的底层实现是**map**。常用HashSet, LinkedHashSet, TreeSet.(只有 TreeSet 不允许存在 null 元素) 

```java
Module java.base
Package java.util
Interface Set<E>
  
// All Superinterfaces:
Collection<E>, Iterable<E>
// All Known Subinterfaces:
EventSet, NavigableSet<E>, SortedSet<E>
// All Known Implementing Classes:
AbstractSet, ConcurrentHashMap.KeySetView, ConcurrentSkipListSet, CopyOnWriteArraySet, EnumSet, HashSet, JobStateReasons, LinkedHashSet, TreeSet
  
public interface Set<E>
extends Collection<E>
```

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201111541761.png)

Set 创建对象：

```java
Set<String> hashSet = new HashSet<>();
Set<Integer> treeSet = new TreeSet<>();
Set<String> linkedHashSet = new LinkedHashSet<>();
```

 Iterate SET :

```java
// method 1 for
for(String s : hashSet) {
    System.out.println(s);
}

// method 2 foreach after java 1.8
hashSet.forEach(System.out::println);

// method 3 Iterable
Iterator<String> s = hashSet.iterator();
while(s.hasNext()) {
      System.out.println(s.next());
}
```

---

## HashSet

```JAVA
public class HashSet<E> // 底层实现是 HashMap
extends AbstractSet<E>
implements Set<E>, Cloneable, Serializable // 实现了 Set
```

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201121249726.png)

This class implements the `Set` interface, backed by a hash table (actually a `HashMap` instance).

HashSet 类实现了`Set`接口，由一个哈希表（实际上是一个`HashMap`实例）支持。它不保证集合的迭代顺序；特别是，它不保证订单会随着时间的推移保持不变。此类**允许一个`null` **元素。

* HashSet 基于 **HashMap** 来实现的，利用**HashMap** 中 **Key** 的唯一性，来保证HashSet中**没有重复值**。而 HashMap 的 value 则存储了一个 `PRESENT`，它是一个静态的 Object 对象。

* HashSet **允许有 null 值**。

* HashSet 是无序的，即不会记录插入的顺序。

* HashSet 不是线程安全的， 如果多个线程尝试同时修改 HashSet，则最终结果是不确定的。 

* HashSet 实现了 Set 接口。

线程安全

```java
Set s = Collections.synchronizedSet(new HashSet(...));
```

Define HashSet:

```java
Set<String> set1 = new HashSet<>();
Set<Integer> set2 = new HashSet<>(initialCapacity: 10); //申明容量
Set<Integer> set3 = new HashSet<Integer>(initialCapacity: 10,loadFactor: 0.75f); // 申明容量和加载因子
```



### HashSet 的实现原理？

首先，我们需要知道它是Set的一个实现，所以保证了当中没有重复的元素。

其次，HashSet使用的是散列函数，那么它当中的元素也就无序可寻。当中是允许元素为null的。

先对实现原理进行一个总结：

(1)基于HashMap实现的，默认构造函数是构建一个初始容量为16，负载因子为0.75 的HashMap。封装了一个 HashMap 对象来存储所有的集合元素，所有放入 HashSet 中的集合元素实际上由 HashMap 的 key 来保存，而 HashMap 的 value 则存储了一个虚拟的Object对象 PRESENT，它是一个静态的 Object 对象。

(2)当我们试图把某个类的对象当成 HashMap的 key，或试图将这个类的对象放入 HashSet 中保存时，重写该类的equals(Object obj)方法和 hashCode() 方法很重要，而且这两个方法的返回值必须保持一致：当该类的两个的 hashCode() 返回值相同时，它们通过 equals() 方法比较也应该返回 true。通常来说，所有参与计算 hashCode() 返回值的关键属性，都应该用于作为 equals() 比较的标准。

(3)HashSet的其他操作都是基于HashMap的。



**HashSet in Java is used when**

1. We don’t want to store duplicate elements. 不想要重复的数据
2. We want to remove duplicate elements from the list. 想要去移除重复数据
3. HashSet is more preferred when add and remove operations are more as compared to get operations. 添加和删除数据比查询快
4. We are not working in a multithreading environment. 线程不安全

```java
import java.util.HashSet;

public class HashSetTest {
    public static void main (String[] args) {
        HashSet<String> hashSet = new HashSet<>();
        hashSet.add("Google");
        hashSet.add("FACEBOOK");
        hashSet.add("twitter");
        hashSet.add(null);
        hashSet.add("Instagram");
        hashSet.add("Google"); // hashCode相同，返回true，不会被存储进hashSet
        System.out.println(hashSet); //[Google, FACEBOOK, twitter, Instagram]
        boolean a = hashSet.contains("Tencent");
        System.out.println(a); // hashSet中不包含Tencent，返回false
    }
}
```



---

## LinkedHashSet

```java
public class LinkedHashSet<E> // 底层实现是 double-linked-list 双向链表
extends HashSet<E>
implements Set<E>, Cloneable, Serializable // 实现了 Set
```

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201121249942.png)



**LinkedHashSet**是继承**HashSet**一样都实现了**Set**, 不同之处是 `LinkedHashSet`它维护一个贯穿其所有条目的双向链表 `doubly linked list`。这个链表定义了迭代顺序，即元素插入集合的插入顺序。 **简而言之，HashSet 没有顺序, LinkedHashSet 有顺序。**

```java
Set<String> hashSet = new HashSet<>();
Set<String> linkedHashSet = new LinkedHashSet<>();

hashSet.add("aaa");
hashSet.add("bbb");
hashSet.add(null);

linkedHashSet.add("aaa");
linkedHashSet.add("bbb");
linkedHashSet.add(null);

System.out.println(hashSet); // [aaa, null, bbb] 和插入顺序不一样
System.out.println(linkedHashSet); // [aaa, bbb, null] 顺序和插入顺序一样
```



**When to use LinkedHashSet in Java?**

LinkedHashSet can be used when you do not want duplicate elements (i.e. want to remove duplicate elements) and want to maintain order in which elements are inserted.

If you want to impose different orders such as increasing or decreasing order, you can use TreeSet class that you will learn in the next tutorial.

**Which is better to use: HashSet or LinkedHashSet?**

If you do not require to maintain order in which elements are inserted then use HashSet that is more fast and efficient than LinkedHashSet.



---

## TreeSet

```java
public class TreeSet<E> // 底层实现是 TreeMap
extends AbstractSet<E>
implements NavigableSet<E>, Cloneable, Serializable // 实现了 NavigableSet
```

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201121250758.png)

A [`NavigableSet`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/NavigableSet.html) implementation based on a [`TreeMap`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/TreeMap.html). The elements are ordered using their [natural ordering](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Comparable.html), or by a [`Comparator`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Comparator.html) provided at set creation time, depending on which constructor is used.

This implementation provides guaranteed **log(n) time cost** for the basic operations (`add`, `remove` and `contains`).

TreeSet里面有一个私有化的成员变量NavigableMap，通过构造函数可以发现，NavigableMap实际上是一个TreeMap。TreeSet的所有搜索功能都是借助TreeMap的key的相关操作实现的。

**所以TreeSet 的底层实现是TreeMap。**



**TreeSet 不可以插入 null 元素， 内部顺序是按生序排列。**

```java
Set<Integer> treeSet = new TreeSet<>();
treeSet.add(3);
treeSet.add(0);
treeSet.add(2);
System.out.println(treeSet); // [0, 2, 3] 自动按生序排列
```



**NavigableSet 常用 methods**

```java
        NavigableSet<Integer> navigableSet=new TreeSet<Integer>();
 
        navigableSet.add(1);
        navigableSet.add(2);
        navigableSet.add(3);
        navigableSet.add(4);
        navigableSet.add(5);
        navigableSet.add(8);
        navigableSet.add(10);
 
        System.out.println("元素个数：" + navigableSet.size());
        System.out.println("返回大于等于6的最小元素：" + navigableSet.ceiling(6));
        System.out.println("返回小于等于6的最大元素：" + navigableSet.floor(6));
        System.out.println("返回倒序迭代器：" + navigableSet.descendingIterator());
        System.out.println("返回倒序的NavigableSet：" + navigableSet.descendingSet());
        System.out.println("返回小于4的所有元素（不包括4）的所有元素的集合：" + navigableSet.headSet(4));
        System.out.println("返回大于5的最小元素:" + navigableSet.higher(5));
        System.out.println("返回小于5的最大元素：" + navigableSet.lower(5));
 
        System.out.println("返回2（包含）到8（不包含）之间的所有元素的有序集合" + navigableSet.subSet(2,8));
        System.out.println("返回大于5的所有元素的有序集合：" + navigableSet.tailSet(5));
        System.out.println("返移除并返回集合中最小的元素：" + navigableSet.pollFirst());
        System.out.println("返移除并返回集合中最大的元素：" + navigableSet.pollLast());
```

```java

元素个数：7
返回大于等于6的最小元素：8
返回小于等于6的最大元素：5
返回倒序迭代器：java.util.TreeMap$NavigableSubMap$DescendingSubMapKeyIterator@2d8e6db6
返回倒序的NavigableSet：[10, 8, 5, 4, 3, 2, 1]
返回小于4的所有元素（不包括4）的所有元素的集合：[1, 2, 3]
返回大于5的最小元素:8
返回小于5的最大元素：4
返回2（包含）到8（不包含）之间的所有元素的有序集合[2, 3, 4, 5]
返回大于5的所有元素的有序集合：[5, 8, 10]
返移除并返回集合中最小的元素：1
```

**TreeSet 常用 methods**

```java
TreeSet<Integer> treeSet = new TreeSet<>();

treeSet.add(3);
treeSet.add(0);
treeSet.add(2);
treeSet.add(1);
treeSet.add(4);

System.out.println(treeSet); // [0, 1, 2, 3, 4]
System.out.println(treeSet.first()); // [0]
System.out.println(treeSet.last()); // [4]
System.out.println(treeSet.headSet(2)); // [0,1]   头set不包含2
System.out.println(treeSet.tailSet(2)); // [2,3,4] 尾set包含2
System.out.println(treeSet.subSet(1,3)); // [1,2]  subset只含头，不含尾
System.out.println(treeSet.descendingSet()); // [4, 3, 2, 1, 0] 倒序
```

**When to Use TreeSet in Java?**

TreeSet can be used when we want unique elements in sorted order. 

**Which is better to use: HashSet or TreeSet?**

If you want to store unique elements in sorted order then use TreeSet, otherwise, use HashSet with no ordering of elements. This is because HashSet is much faster than TreeSet.



---

### HashSet Source Code

```java
public class HashSet<E> extends AbstractSet<E> implements Set<E>, Cloneable, java.io.Serializable
{
    static final long serialVersionUID = -5024744406713321676L;

    // 底层使用HashMap来保存HashSet中所有元素。
    private transient HashMap<E,Object> map;

    // 定义一个虚拟的Object对象作为HashMap的value，将此对象定义为static final。
    private static final Object PRESENT = new Object();

    /**
     * 默认的无参构造器，构造一个空的HashSet。
     * 
     * 实际底层会初始化一个空的HashMap，并使用默认初始容量为16和加载因子0.75。
     */
    public HashSet() {
        map = new HashMap<E,Object>();
    }

    /**
     * 构造一个包含指定collection中的元素的新set。
     *
     * 实际底层使用默认的加载因子0.75和足以包含指定
     * collection中所有元素的初始容量来创建一个HashMap。
     * @param c 其中的元素将存放在此set中的collection。
     */
    public HashSet(Collection<? extends E> c) {
        map = new HashMap<E,Object>(Math.max((int) (c.size()/.75f) + 1, 16));
        addAll(c);
    }

    /**
     * 以指定的initialCapacity和loadFactor构造一个空的HashSet。
     *
     * 实际底层以相应的参数构造一个空的HashMap。
     * @param initialCapacity 初始容量。
     * @param loadFactor 加载因子。
     */
    public HashSet(int initialCapacity, float loadFactor) {
        map = new HashMap<E,Object>(initialCapacity, loadFactor);
    }

    /**
     * 以指定的initialCapacity构造一个空的HashSet。
     *
     * 实际底层以相应的参数及加载因子loadFactor为0.75构造一个空的HashMap。
     * @param initialCapacity 初始容量。
     */
    public HashSet(int initialCapacity) {
        map = new HashMap<E,Object>(initialCapacity);
    }

    /**
     * 以指定的initialCapacity和loadFactor构造一个新的空链接哈希集合。
     * 此构造函数为包访问权限，不对外公开，实际只是是对LinkedHashSet的支持。
     *
     * 实际底层会以指定的参数构造一个空LinkedHashMap实例来实现。
     * @param initialCapacity 初始容量。
     * @param loadFactor 加载因子。
     * @param dummy 标记。
     */
    HashSet(int initialCapacity, float loadFactor, boolean dummy) {
        map = new LinkedHashMap<E,Object>(initialCapacity, loadFactor);
    }

    /**
     * 返回对此set中元素进行迭代的迭代器。返回元素的顺序并不是特定的。
     * 
     * 底层实际调用底层HashMap的keySet来返回所有的key。
     * 可见HashSet中的元素，只是存放在了底层HashMap的key上，
     * value使用一个static final的Object对象标识。
     * @return 对此set中元素进行迭代的Iterator。
     */
    public Iterator<E> iterator() {
        return map.keySet().iterator();
    }

    /**
     * 返回此set中的元素的数量（set的容量）。
     *
     * 底层实际调用HashMap的size()方法返回Entry的数量，就得到该Set中元素的个数。
     * @return 此set中的元素的数量（set的容量）。
     */
    public int size() {
        return map.size();
    }

    /**
     * 如果此set不包含任何元素，则返回true。
     *
     * 底层实际调用HashMap的isEmpty()判断该HashSet是否为空。
     * @return 如果此set不包含任何元素，则返回true。
     */
    public boolean isEmpty() {
        return map.isEmpty();
    }

    /**
     * 如果此set包含指定元素，则返回true。
     * 更确切地讲，当且仅当此set包含一个满足(o==null ? e==null : o.equals(e))
     * 的e元素时，返回true。
     *
     * 底层实际调用HashMap的containsKey判断是否包含指定key。
     * @param o 在此set中的存在已得到测试的元素。
     * @return 如果此set包含指定元素，则返回true。
     */
    public boolean contains(Object o) {
        return map.containsKey(o);
    }

    /**
     * 如果此set中尚未包含指定元素，则添加指定元素。
     * 更确切地讲，如果此 set 没有包含满足(e==null ? e2==null : e.equals(e2))
     * 的元素e2，则向此set 添加指定的元素e。
     * 如果此set已包含该元素，则该调用不更改set并返回false。
     *
     * 底层实际将将该元素作为key放入HashMap。
     * 由于HashMap的put()方法添加key-value对时，当新放入HashMap的Entry中key
     * 与集合中原有Entry的key相同（hashCode()返回值相等，通过equals比较也返回true），
     * 新添加的Entry的value会将覆盖原来Entry的value，但key不会有任何改变，
     * 因此如果向HashSet中添加一个已经存在的元素时，新添加的集合元素将不会被放入HashMap中，
     * 原来的元素也不会有任何改变，这也就满足了Set中元素不重复的特性。
     * @param e 将添加到此set中的元素。
     * @return 如果此set尚未包含指定元素，则返回true。
     */
    public boolean add(E e) {
        return map.put(e, PRESENT)==null;
    }

    /**
     * 如果指定元素存在于此set中，则将其移除。
     * 更确切地讲，如果此set包含一个满足(o==null ? e==null : o.equals(e))的元素e，
     * 则将其移除。如果此set已包含该元素，则返回true
     * （或者：如果此set因调用而发生更改，则返回true）。（一旦调用返回，则此set不再包含该元素）。
     *
     * 底层实际调用HashMap的remove方法删除指定Entry。
     * @param o 如果存在于此set中则需要将其移除的对象。
     * @return 如果set包含指定元素，则返回true。
     */
    public boolean remove(Object o) {
        return map.remove(o)==PRESENT;
    }

    /**
     * 从此set中移除所有元素。此调用返回后，该set将为空。
     *
     * 底层实际调用HashMap的clear方法清空Entry中所有元素。
     */
    public void clear() {
        map.clear();
    }

    /**
     * 返回此HashSet实例的浅表副本：并没有复制这些元素本身。
     *
     * 底层实际调用HashMap的clone()方法，获取HashMap的浅表副本，并设置到HashSet中。
     */
    public Object clone() {
        try {
            HashSet<E> newSet = (HashSet<E>) super.clone();
            newSet.map = (HashMap<E, Object>) map.clone();
            return newSet;
        } catch (CloneNotSupportedException e) {
            throw new InternalError();
        }
    }
}
```

