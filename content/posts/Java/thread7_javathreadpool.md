---
title: "Java Threads 7: threadpool"
date: 2021-11-26T11:18:55+08:00
draft: true
toc: false
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Threads
---

## **What is the Thread Pool in Java?**

As the name suggests, the thread pool in Java is actually a pool of [Threads](https://www.edureka.co/blog/java-thread/). In a simple sense, it contains a group of worker threads that are waiting for the job to be granted. They are reused in the whole process.

In a Thread Pool, a group of fixed size threads is created. Whenever a task has to be granted, one of the threads is pulled out and assigned that task by the service provider, as soon as the job is completed the thread is returned back to the thread pool. Thread pool is preferably used because active threads consume system resources, when is JVM creates too many threads at the same time, the system could run out of memory. Hence the number of threads to be created has to be limited. Therefore the concept of the thread pool is preferred!

线程池顾名思义就是一个包含很多线程的池子，这个池子里的线程都是可复用的，使用线程池是为了降低系统内存的消耗。

## **Advantages of a Thread Pool**

- Better performance

- Saves time

- No need to create a thread again and again

- Easy to access

- Real-time usage

  使用线程池的优点：不用重复创造线程，节省时间，提高性能，方便访问和使用。

## **Disadvantages of the Thread Pool**

- There is no control over the priority and state of the thread you are working with.

- There is no stable identity given to the thread, no track can be kept.

- When there is a high demand for the thread pool, the process may be deleted.

- The thread pool can not work well when two threads are working in parallel.

- There are several situations where the application code can be affected by another application code, despite robust application isolation.

  线程池的缺点：无法控制线程的优先级，无法追踪线程，无法很好的执行并行线程工作。

## **Risk in the Java Thread Pool**

There are a few risks while you are dealing with the thread pool, like;

- **Thread Leakage:** If a thread is removed from the pool to perform a task but not returned back to it when the task is completed, thread leakage occurs.

  **线程泄漏：**如果线程从池中移除去执行任务但在任务完成时没有返回到它，则发生线程泄漏。

- **Deadlock:** In thread pool is executing thread is waiting for the output from the block the thread waiting in the queue due to unavailability of thread for execution, there’s a case of a deadlock.

  **死锁：** 在线程池里

- **Resource Thrashing:** More number of threads than the optimal number required can cause starvation problems leading to resource thrashing.

  **资源抖动：**线程数超过所需的最佳数量会导致饥饿问题，从而导致资源抖动。
