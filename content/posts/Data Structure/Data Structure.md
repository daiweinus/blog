---
title: "Data Structure"
date: 2022-01-01T10:57:11+08:00
draft: true
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Data Structure

---

![img](https://img-blog.csdnimg.cn/img_convert/5253e82f78c3e235799fe38bfab6f097.png)

![](https://pica.zhimg.com/v2-5dd21bea8b50af177e31351ed0a2ea8d_r.jpg?source=172ae18b)

![img](https://miro.medium.com/max/2000/1*RyCRTcbKIxHiPe5AObrvqQ.png)

![](https://img-blog.csdnimg.cn/20190227211326757.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NhcnRvb25f,size_16,color_FFFFFF,t_70)

![](https://static.javatpoint.com/ds/images/ds-introduction.png)

![Hierarchy of Java Collection framework](https://static.javatpoint.com/images/java-collection-hierarchy.png)

## Array

![img](https://java2blog.com/wp-content/uploads/2017/09/Array.png)

数组是将相同类型的元素存储于连续内存空间的数据结构，其长度不可变。

构建数组需要在初始化时给定长度，并对数组每个索引元素赋值，代码如下：

```java
int[] array = new array[3]; // 初始化一个长度为 3 的数组 array
array[0] = 1; // 元素赋值
array[1] = 2;
array[2] = 3;
```

或者可以使用直接赋值的初始化方式，代码如下：

```java
int[] array = {1,2,3}; //直接赋值
```

## List

**List—是一个有序的集合，可以包含重复的元素，提供了按索引访问的方式，它继承Collection。**

**List有两个重要的实现类：ArrayList和LinkedList**

线性表在数据结构中是一种**最基本、最简单、最常用**的数据结构。它将数据一个接一个的排成一条线（可能逻辑上），也因此线性表上的每个数据只有前后两个方向，而在数据结构中，**数组、链表、栈、队列**都是线性表。**二叉树**和**图**就是典型的非线性结构了

## ArrayList

{{< figure src="https://java2blog.com/wp-content/webpc-passthru.php?src=https://java2blog.com/wp-content/uploads/2016/05/ArrayList.jpg&nocache=1 S" alt="image" caption="ArrayList" class="right">}}

下面两种ArrayList初始化方式都是正确的，List is an **`interface`** and ArrayList is a **`class`**. 

```java
List<Integer> list1 = new ArrayList<Integer>(); //generally preferred
ArrayList<Integer> list2 = (ArrayList<Integer>) list; // type-cast
```

* initialize as **`List<E>`** 更加灵活flexible, preferable，可以随后选择 LinkedList or ArrayList.

* initialize as **`ArrayList<E>`** 可以访问使用所有的ArrayList class method, such as such as _`ArrayList#ensureCapacity`_ or _`ArrayList#trimToSize`_.

```java
List<String> list = new ArrayList<>();// 初始化可变数组
list.add("one"); // list["one"]
list.add("two"); // list["one","two"]
list.remove(0); //list["two"]
list.add(1,4); //list["two",4]
boolean a = list.contains(2); //true
```

ArrayList的 **toArray** 方法返回一个数组, ArrayList的 **asList** 方法返回一个列表.

## LinkedList

{{< figure src="https://img-blog.csdnimg.cn/img_convert/81117006f63098c29cceb5938fdc3199.png" alt="image" caption="LinkedList" class="right">}}

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

## ArrayList vs LinkedList

{{< figure src="https://static.studytonight.com/data-structures/images/array-vs-linked-list.png" caption="ArrayList vs LinkedList" class="right">}}

> * ArrayList **底层是数组,内存地址连续可随机访问元素，查询快O(1),**
>
> * ArrayList **动态扩容和元素拷贝 增删慢, 实现了List 接口;**
>
> * LinkedList **底层是链表,内存地址不连续必须按顺序访问元素，查询慢O(N),**
>
> * LinkedList **只需要修改节点指针指向 增删快O(1), 实现List & Deque 接口。**  

## Stack

{{< figure src="https://java2blog.com/wp-content/webpc-passthru.php?src=https://java2blog.com/wp-content/uploads/2017/09/Stack.png&nocache=1 Z" caption="Stack" class="right">}}"

栈是一种具有 「先入后出 FILO」 特点的抽象数据结构，可使用数组或链表实现。

通过常用操作「入栈 `push()`」,「出栈 `pop()`」，展示了栈的先入后出特性

```java
Stack<Integer> stack = new Stack<>();
stack.push(1); // push = 1 ,stack = [1]
stack.push(2); // push = 2, stack = [1,2]
stack.peek(); // peek = 2
stack.pop(); // pop = 2, stack[1],
stack.pop(); // pop = 1, stack[],
```

## Queue

{{<figure src="https://java2blog.com/wp-content/webpc-passthru.php?src=https://java2blog.com/wp-content/uploads/2017/09/Queue.png&nocache=1 S" style="zoom:80%" class="right" caption="Queue">}}

队列是一种具有 「先入先出 FIFO」 特点的抽象数据结构，可使用链表实现.

通过常用操作「入队 `offer()`」,「出队 `poll()`」，展示了队列的先入先出特性。

```java
Queue<Integer> queue = new LinkedList<>();
queue.offer(1); // queue = [1]
queue.offer(2); // queue = [1,2]
queue.peek(); // peek = 1
queue.poll();   // poll = 1; queue = [2]
queue.poll();   // poll = 2; queue = []
```

## Tree

{{<figure src="https://img-blog.csdnimg.cn/img_convert/03f6d9e00726a132eac1b662a4e8a5ef.png" style="zoom:50%;" caption="Tree" class="right">}}

树是一种非线性数据结构，根据子节点数量可分为 「二叉树」 和 「多叉树」，最顶层的节点称为「根节点 root」。以二叉树为例，每个节点包含三个成员变量：「值 val」、「左子节点 left」、「右子节点 right」 。

```java
class TreeNode {
    int val;        // 节点值
    TreeNode left;  // 左子节点
    TreeNode right; // 右子节点
    TreeNode(int x) { val = x; }
}
```

建立此二叉树需要实例化每个节点，并构建各节点的引用指向。

```java
// 初始化节点
TreeNode n1 = new TreeNode(3); // 根节点 root
TreeNode n2 = new TreeNode(4);
TreeNode n3 = new TreeNode(5);
TreeNode n4 = new TreeNode(1);
TreeNode n5 = new TreeNode(2);

// 构建引用指向
n1.left = n2;
n1.right = n3;
n2.left = n4;
n2.right = n5;
```

## Graph

{{<figure src="https://img-blog.csdnimg.cn/img_convert/8bb2cee2e9db758ff3de1ace8a5fc848.png" class="right" caption="Graph">}}

图是一种非线性数据结构，由「节点（顶点）vertex」和「边 edge」组成，每条边连接一对顶点。根据边的方向有无，图可分为「有向图」和「无向图」。本文 以无向图为例 开展介绍。

如下图所示，此无向图的 顶点 和 边 集合分别为：

顶点集合： vertices = {1, 2, 3, 4, 5}
边集合： edges = {(1, 2), (1, 3), (1, 4), (1, 5), (2, 4), (3, 5), (4, 5)

```java
int[] vertices = {1, 2, 3, 4, 5};
int[][] edges = {{0, 1, 1, 1, 1},
                 {1, 0, 0, 1, 0},
                 {1, 0, 0, 0, 1},
                 {1, 1, 0, 0, 1},
                 {1, 0, 1, 1, 0}}
```

## Hashing

{{<figure src="https://img-blog.csdnimg.cn/img_convert/f2adf1e5cc3f127acd432dc34b7b2fbe.png" class="right" caption="Hashing">}}

散列表是一种非线性数据结构，通过利用 Hash 函数将指定的「键 `key`」映射至对应的「值 `value`」，以实现高效的元素查找.

> 设想一个简单场景：小力、小特、小扣的学号分别为 10001, 10002, 10003 。
> 现需求从「姓名」查找「学号」。

则可通过建立姓名为 key ，学号为 value 的散列表实现此需求，代码如下：

```java
// 初始化散列表
Map<String, Integer> dic = new HashMap<>();

// 添加 key -> value 键值对
dic.put("小力", 10001);
dic.put("小特", 10002);
dic.put("小扣", 10003);

// 从姓名查找学号
dic.get("小力"); // -> 10001
dic.get("小特"); // -> 10002
dic.get("小扣"); // -> 10003
```

## Heap

{{<figure src="https://img-blog.csdnimg.cn/img_convert/a803f4a953df9c1e5a243883c1ae7c94.png" class="right" caption="Heap">}}

堆是一种基于「完全二叉树」的数据结构，可使用数组实现。以堆为原理的排序算法称为「堆排序」，基于堆实现的数据结构为「优先队列」。堆分为「大顶堆」和「小顶堆」，大（小）顶堆：任意节点的值不大于（小于）其父节点的值。

> 完全二叉树定义： 设二叉树深度为 kk ，若二叉树除第 kk 层外的其它各层（第 11 至 k-1k−1 层）的节点达到最大个数，且处于第 kk 层的节点都连续集中在最左边，则称此二叉树为完全二叉树。

如下图所示，为包含 1, 4, 2, 6, 8 元素的小顶堆。将堆（完全二叉树）中的结点按层编号，即可映射到右边的数组存储形式。

```java
// 初始化小顶堆
Queue<Integer> heap = new PriorityQueue<>();

// 元素入堆
heap.add(1);
heap.add(4);
heap.add(2);
heap.add(6);
heap.add(8);

// 元素出堆（从小到大）
heap.poll(); // -> 1
heap.poll(); // -> 2
heap.poll(); // -> 4
heap.poll(); // -> 6
heap.poll(); // -> 8
```

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202112291814955.png)
