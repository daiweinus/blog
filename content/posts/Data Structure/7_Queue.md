---
title: "Java Data Structure 7: Collection_Queue"
date: 2022-01-07T16:00:11+08:00
draft: true
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Data Structure

---

**Module** [java.base](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/module-summary.html)

**Package** [java.util](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/package-summary.html)

## Interface Queue<E>

- All Superinterfaces:

  `Collection<E>`, `Iterable<E>`

- All Known Subinterfaces:

  `BlockingDeque<E>`, `BlockingQueue<E>`, `Deque<E>`, `TransferQueue<E>`

- All Known Implementing Classes:

  `AbstractQueue`, `ArrayBlockingQueue`, `ArrayDeque`, `ConcurrentLinkedDeque`, `ConcurrentLinkedQueue`, `DelayQueue`, `LinkedBlockingDeque`, `LinkedBlockingQueue`, `LinkedList`, `LinkedTransferQueue`, `PriorityBlockingQueue`, `PriorityQueue`, `SynchronousQueue`

------

```java
public interface Queue<E>
```

A collection designed for holding elements prior to processing. Besides basic [`Collection`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Collection.html) operations, queues provide additional insertion, extraction, and inspection operations. Each of these methods exists in two forms: one throws an exception if the operation fails, the other returns a special value (either `null` or `false`, depending on the operation). The latter form of the insert operation is designed specifically for use with capacity-restricted `Queue` implementations; in most implementations, insert operations cannot fail.

|         | Throws exception                                             | Returns special value                                        |
| ------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Insert  | [`add(e)`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Queue.html#add(E)) | [`offer(e)`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Queue.html#offer(E)) |
| Remove  | [`remove()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Queue.html#remove()) | [`poll()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Queue.html#poll()) |
| Examine | [`element()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Queue.html#element()) | [`peek()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Queue.html#peek()) |

Queues typically, but do not necessarily, order elements in a **FIFO (first-in-first-out)** manner. Among the exceptions are priority queues, which order elements according to a supplied comparator, or the elements' natural ordering, and LIFO queues (or stacks) which order the elements LIFO (last-in-first-out). Whatever the ordering used, the *head* of the queue is that element which would be removed by a call to [`remove()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Queue.html#remove()) or [`poll()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Queue.html#poll()). In a FIFO queue, all new elements are inserted at the *tail* of the queue. Other kinds of queues may use different placement rules. Every `Queue` implementation must specify its ordering properties.

This interface is a member of the [Java Collections Framework](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/package-summary.html#CollectionsFramework).

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201121521758.png)



```java
Queue<Integer> queue = new PriorityQueue<>();
Deque<Integer> deque1 = new LinkedList<>();
Deque<Integer> deque2 = new ArrayDeque<>();
```

**Note:**

\1. The `poll()` and `remove()` methods are similar, except that `poll()` returns **null** object if the queue is empty, whereas remove() throws an exception named NoSuchElementException.

\2. The `peek()` and `element()` methods are similar, except that `peek()` returns **null** object if the queue is empty, whereas element() throws an exception named NoSuchElementException.

\3. The `offer()` method is used to insert an element to the queue. This method is similar to the `add()` method inherited from the Collection interface, but the offer() method is more preferred for queues.

---

## PriorityQueue

```java
public class PriorityQueue<E> // 底层实现 priority heap (binary heap)
extends AbstractQueue<E>
implements Serializable, Queue<E> // 可现实 Queue
```

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201121543458.png)

A **PriorityQueue in Java** is a queue or collection of elements in which elements are stored in order of their priority. 底层实现是 priority heap。

An ordinary queue is a first-in-first-out (FIFO) data structure

In Java PriorityQueue, elements are stored in order of their priority. When accessing elements, the element with the highest priority is removed first before the element with lower priority.

Element at the head of priority queue is **least element**.

Element at the tail of priority queue is **greatest element**.

enqueue 和 dequeue 的速度是 `Olog(n)`.

线程不安全，多线程下使用 `PriorityBlockingQueue` .

```java
Queue<Integer> pq = new PriorityQueue<>();

pq.offer(5); // add element in head of queue
pq.offer(4);
pq.offer(3);
pq.offer(1);
pq.offer(2);
System.out.println(pq); // [1, 2, 4, 5, 3] 遍历打印的时候并不会按顺序

while(pq.peek() != null) {
    System.out.println(pq.peek());  // 1 2 3 4 5 但是使用peek方法的时候就会按从小到大的顺序
    pq.poll(); // remove head element
}
```



---

## Dequeue

```java
public interface Deque<E>
extends Queue<E>
  
// All Superinterfaces:
Collection<E>, Iterable<E>, Queue<E>
// All Known Subinterfaces:
BlockingDeque<E>
// All Known Implementing Classes:
ArrayDeque, ConcurrentLinkedDeque, LinkedBlockingDeque, LinkedList 
  
Deque<Integer> dl = new LinkedList<>();
Deque<Integer> da = new ArrayDeque<>();
```

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201121648746.png)

The most important features of Deque are push and pop. The `push()` and `pop()` methods are commonly used to enable a Deque to function as a stack.

The name *deque* is short for "**double ended queue**" and is usually pronounced "deck".

---



**Summary of Deque methods**

|                  | First Element (Head)                                         | Last Element (Tail)                                          |                                                              |                                                              |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Throws exception | Special value                                                | Throws exception                                             | Special value                                                |                                                              |
| Insert           | [`addFirst(e)`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#addFirst(E)) | [`offerFirst(e)`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#offerFirst(E)) | [`addLast(e)`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#addLast(E)) | [`offerLast(e)`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#offerLast(E)) |
| Remove           | [`removeFirst()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#removeFirst()) | [`pollFirst()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#pollFirst()) | [`removeLast()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#removeLast()) | [`pollLast()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#pollLast()) |
| Examine          | [`getFirst()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#getFirst()) | [`peekFirst()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#peekFirst()) | [`getLast()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#getLast()) | [`peekLast()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#peekLast()) |

**Comparison of *Queue and Deque* methods**

| `Queue` Method                                               | Equivalent `Deque` Method                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`add(e)`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#add(E)) | [`addLast(e)`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#addLast(E)) |
| [`offer(e)`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#offer(E)) | [`offerLast(e)`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#offerLast(E)) |
| [`remove()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#remove()) | [`removeFirst()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#removeFirst()) |
| [`poll()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#poll()) | [`pollFirst()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#pollFirst()) |
| [`element()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#element()) | [`getFirst()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#getFirst()) |
| [`peek()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#peek()) | [`peekFirst()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#peekFirst()) |

**Comparison of *Stack and Deque* methods**

| Stack Method                                                 | Equivalent `Deque` Method                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`push(e)`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#push(E)) | [`addFirst(e)`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#addFirst(E)) |
| [`pop()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#pop()) | [`removeFirst()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#removeFirst()) |
| [`peek()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#peek()) | [`getFirst()`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html#getFirst()) |



---

### AarryDeque

```java
public class ArrayDeque<E>
extends AbstractCollection<E>
implements Deque<E>, Cloneable, Serializable
```

Resizable-array implementation of the [`Deque`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Deque.html) interface. Array deques have **no capacity restrictions**; they grow as necessary to support usage. They are **not thread-safe**; in the absence of external synchronization, they do not support concurrent access by multiple threads. **Null elements are prohibited**. **This class is likely to be faster than [`Stack`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Stack.html) when used as a stack, and faster than [`LinkedList`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/LinkedList.html) when used as a queue.** 

**ArrayDeque 用作 stack 的时候比 Stack 快，用作 queue 队列的时候比 LinkedList 快。**

```java
Deque<Integer> da = new ArrayDeque()<>;

da.offer(3); // [3]
da.offer(2); // [3,2]
da.addFirst(4); // [4,3,2]
da.addLast(1); // [4,3,2,1]

System.out.println(da); // [4, 3, 2, 1]
System.out.println(da.pollFirst()); // [4]
System.out.println(da.pollLast()); // [1]
System.out.println(da); // [3,2]
System.out.println(da.peekFirst()); // [3]
System.out.println(da.peekLast()); // [2]
```



---

### ArrayDeque vs LinkedList

Key differences:

1. The *ArrayDeque* class is the resizable array implementation of the *Deque* interface and *LinkedList* class is the list implementation
2. **NULL** elements can be added to ***LinkedList*** but not in *ArrayDeque*
3. *ArrayDeque* is more efficient than the *LinkedList* for add and remove operation at both ends and LinkedList implementation is efficient for removing the current element during the iteration
4. The ***LinkedList*** implementation consumes **more memory** than the *ArrayDeque*



在java中，Queue被定义成单端队列使用，Deque被定义成双端队列使用。
而由于双端队列的定义，Deque可以作为栈或者队列使用，而Queue只能作为队列或者依赖于子类的实现作为堆使用。