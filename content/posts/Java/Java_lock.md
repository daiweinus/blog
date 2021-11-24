---
title: "Java Lock"
date: 2021-11-03T10:10:07+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Java
---

```apl
Module: java.base
Package: java.util.concurrent.locks
Interface Lock
  
All Known Implementing Classes:
ReentrantLock, ReentrantReadWriteLock.ReadLock, ReentrantReadWriteLock.WriteLock
```

`Lock`实现提供了比使用`synchronized`方法和语句获得的更广泛的锁定操作。它们允许更灵活的结构，可能具有完全不同的属性，并且可能支持多个关联 [`Condition`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/concurrent/locks/Condition.html)对象。

锁是用于控制多个线程对共享资源的访问的工具。通常，锁提供对共享资源的独占访问：一次只有一个线程可以获取锁，所有对共享资源的访问都需要先获取锁。但是，某些锁可能允许并发访问共享资源，例如[`ReadWriteLock`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/concurrent/locks/ReadWriteLock.html).

`synchronized`方法或语句的使用提供对与每个对象关联的隐式监视器锁的访问，但强制所有锁的获取和释放以块结构的方式发生：当获取多个锁时，它们必须以相反的顺序释放，并且所有锁必须在获得它们的同一个词法范围内释放。

虽然`synchronized`方法和语句的作用域机制使使用监视器锁编程变得更加容易，并有助于避免许多涉及锁的常见编程错误，但在某些情况下，您需要以更灵活的方式使用锁。例如，一些遍历并发访问数据结构的算法需要使用“hand-over-hand”或“chainlocking”：你先获取节点A的锁，然后节点B，然后释放A，获取C，然后释放B并获得 D 等等。所述的实施方式中 `Lock`接口通过允许获得并在不同的范围释放的锁，并允许获得并以任何顺序释放多个锁使得能够使用这样的技术。

这种增加的灵活性带来了额外的责任。块结构锁的缺失消除了`synchronized` 方法和语句中发生的锁的自动释放。在大多数情况下，应使用以下习语：

```java
 Lock l = new Lock;
 l.lock();
 try {
   // access the resource protected by this lock
 } finally {
   l.unlock();
 }
```

当锁定和解锁发生在不同的作用域时，必须注意确保持有锁时执行的所有代码都受到 try-finally 或 try-catch 的保护，以确保在必要时释放锁。

```java
package lockTest;


import java.util.concurrent.locks.ReentrantLock;

/**
 * ConcurrentThread Safety
 * The solution 1: synchronized
 * The solution 2: lock
 */
public class LockTest {
    public static void main(String[] args) {
        Window w = new Window();

        Thread t1 = new Thread(w);
        Thread t2 = new Thread(w);
        Thread t3 = new Thread(w);

        t1.setName("Window 1");
        t2.setName("Window 2");
        t3.setName("Window 3");

        t1.start();
        t2.start();
        t3.start();
    }
}


class Window implements Runnable {
    private int tickets = 100;
    private final ReentrantLock lock = new ReentrantLock();

    @Override
    public void run() {
        while (true) {
            lock.lock();
            try {
                if (tickets > 0) {
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(Thread.currentThread().getName() + " sold ticket: " + tickets);
                    tickets--;
                } else break;
            } finally {
                lock.unlock();
            }
        }
    }
}
```

### 解决线程安全的方式有几种？

1. synchronized
   * 同步代码块 / 同步方法
2. lock

### sychronized vs lock

* sychonized 在执行完相应的同步代码块后，会自动释放同步监视器。

  lock需要手动启动和停止同步锁``lock()/unlock()``。

建议优先用lock，其实同步代码块，最后考虑同步方法。

### Exercise

```java
package exercise;

import java.util.concurrent.locks.ReentrantLock;

/**
 * 两位储户分别向同一银行账户存入3000，存3次，每次存1000并打印余额
 * 1.是否是多线程问题？是，两位储户同时操作
 * 2.是否共享数据？是，同一个银行账户
 */
public class AccountTest {
    public static void main (String[] args) {
        Account acct = new Account(0);
        Customer c1 = new Customer(acct);
        Customer c2 = new Customer(acct);

        c1.setName("Jack");
        c2.setName("Rose");

        c1.start();
        c2.start();
    }
}

class Account {
    private double balance;
   
    //extend Thread 要用static 修饰 lock
    private final static ReentrantLock l = new ReentrantLock();

    public Account (double balance) {
        this.balance = balance;
    }

    //同步方法 和 lock
    //public synchronized void deposed (double amt) {
    public void deposed (double amt) {
        if(amt > 0) {
            l.lock();
            try{
                balance+=amt;
                System.out.println(Thread.currentThread().getName() + " Deposed success, your balance: " + balance);

                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            } finally {
                l.unlock();
            }
        }
    }
}

class Customer extends Thread {
    private final Account acct;

    public Customer(Account acct){
        this.acct = acct;
    }

    @Override
    public void run(){
       for(int i = 0; i < 3; i ++)
           acct.deposed(1000);
    }
}
```

