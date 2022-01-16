---
title: "Java Threads 6: Lock"
date: 2021-11-25T10:10:07+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Java Threads
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



### Deadlock vs Livelock vs Starvation 死锁 VS 活锁 VS 饿死

**Deadlock** thread A waiting for thread B && thread B also waiting for thread A, the dependence is a circular they are waiting each other. 死锁就像刚在一起的小情侣打电话，男生说：女生先挂电话，女生说：男生先挂电话，最后谁都不先挂电话，无解。。。

**死锁** 是指两个或两个以上的线程在执行过程中，因争夺资源而造成的一种互相等待的现象，这些永远在互相等待的线程称为死锁。死锁就像是独木桥上的两人，互不相让，都想等对方退后，最后两个人都被困在桥上。

```java
synchronized (objRef1) {
  synchronized (objRef2) {
    //...
  }
}

synchronized (objRef2) {
  synchronized (objRef1) {
    //...
  }
}
```

**Livelock** thread are too busy to responding other threads to progress.

**活锁** 线程没有被阻塞，由于某些条件没有满足，导致一直重复尝试，失败，尝试，失败。活锁就像是要过独木桥但还没上桥的两个人，相互礼让，都想让对方先过，最后两个人都过不了桥。

**Starvation** 可运行的线程尽管可以执行，但被调度器无限期地忽视，而不能被调度执行一直处于等待状态的行为。饿死就像路人甲正要过独木桥回家吃饭，对面来了一群老大爷，路人甲让老人先过，接着又来一群小学生，路人甲有让小学生先过，最后天黑了路人甲还没能过桥饿死在桥边了。

**活锁和死锁的区别：** 活锁的状态可以改变，有可能自行解开，死锁只能是等待状态，无法自行解开。

**产生死锁的必要条件**：

1. 互斥使用（资源独占），一个资源每次只能给一个进程使用。
2. 占有且等待，进程在申请新的资源的同时，保持对原有资源的占有。
3. 不可抢占，资源申请者不能强行从资源占有者手中夺取资源，资源只能由占有者自愿释放。
4. 循环等待，P1等待P2占有的资源，P2等待P3的资源，...Pn等待P1的资源，形成一个进程等待回路。

**既然知道了出现死锁的必要条件，其实只要破坏其中一条就可避免死锁！**

其中，互斥这个条件我们没有办法破坏，因为我们用锁为的就是互斥。

对于**占用且等待**这个条件，我们可以**一次性申请所有的资源**，这样就不存在等待了。
对于**不可抢占**这个条件，占用部分资源的线程进一步申请其他资源时，如果申请不到，可以主动释放它占有的资源。
对于**循环等待**这个条件，可以按顺序申请资源来预防。所谓按序申请，是指资源是有线性顺序的，申请的时候可以先申请资源序号小的，再申请资源序号大的，这样线性化后自然就不存在循环了。

**如何解决活锁？**  为线程增加一个随机等待时间，时间到了切换状态。

**如何解决饥饿？** 

1. 增加供给，保证资源充足
2. 公平地分配资源
3. 避免持有锁的线程长时间执行

### 互斥锁
当有一个线程要访问共享资源（临界资源）之前，会对线程访问的这段代码（临界区）进行加锁。如果在加锁之后没释放锁之前其他线程要对临界资源进行访问，则这些线程会被阻塞睡眠，直到解锁，如果解锁时有一个或者多个线程阻塞，那么这些锁上的线程就会变成就绪状态，然后第一个变为就绪状态的线程就会获取资源的使用权，并且再次加锁，其他线程继续阻塞等待。

### 自旋锁

自旋锁和互斥锁很像，唯一不同的是自旋锁访问加锁资源时，会一直循环的查看是否释放锁。这样要比互斥锁效率高很多，但是仍然需要占用CPU。如果线程竞争不激烈适合使用自旋锁。但是但当线程数不断增加时，性能下降明显，因为每个线程都需要执行，会占用大量CPU时间片，就不适用自旋锁了。

### 悲观锁 (Pessimistic Lock)

- 悲观锁认为自己在获取数据的时候一定有别的线程来修改数据，在获取数据的时候会先加锁，确保数据不会被别的线程修改
- 锁实现:Java中关键字synchronized、接口Lock的实现类
- 适用场景:写操作较多，先加锁可以保证写操作时数据正确

### 乐观锁 (Optimistic Lock)

- 乐观锁认为自已在获取数据时不会有别的线程修改数据，所以不会添加锁，只是在更新数据的时候去判断之前有没有别的线程更新了这个数据
- 锁实现: CAS算法， 例如AtomicInteger 类的原子自增是同过CAS自旋实现
- 适用场景:读操作较多，不加锁的特点能够使其读操作的性能大幅提升

**乐观锁和悲观锁都是一种思想，并不是真实存在于数据库中的一种机制。**

### 读写锁

也叫做共享互斥锁，读模式共享，写模式互斥。有点像数据库负载均衡的读写分离模式。它有三种模式：读加锁状态，写加锁状态和不加锁状态。简单来说就是只有一个线程可以占有写模式的读写锁，但是可以有多个线程占用读模式的读写锁。
当写加锁的模式下，任何线程对其进行加锁操作都会被阻塞，直到解锁。
当在读加锁的模式下，任何线程都可以对其进行读加锁的操作，但所有试图进行写加锁操作的线程都会被阻塞。直到所有读线程解锁。但是当读线程太多时，写线程一直被阻塞显然是不对的，所以一个线程想要对其进行写加锁时，就会阻塞读加锁，先让写加锁线程加锁

### 公平锁(Fair Lock)

加锁前检查是否有排队等待的线程，优先排队等待的线程，先来先得。

### 非公平锁(Nonfair Lock)

加锁时不考虑排队等待问题，直接尝试获取锁，获取不到自动到队尾等待。
