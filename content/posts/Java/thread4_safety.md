---
title: "Java Threads 4:Threads Safety"
date: 2021-11-23T12:08:57+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Java Threads
---

Unsafe threads in tickets system 不安全线程:

```java
public class WindowTest2 {
    public static void main (String[] args) {
        Window2 w = new Window2();

        Thread t1 = new Thread (w);
        Thread t2 = new Thread (w);
        Thread t3 = new Thread (w);

        t1.setName("Window_1");
        t2.setName("Window_2");
        t3.setName("Window_3");

        t1.start();
        t2.start();
        t3.start();
    }
}

class Window2 implements Runnable {
    private int tickets = 100;

    @Override
    public void run() {
        while(true) {
            if(tickets > 0) {
                try {
                    Thread.sleep(100); // sleep for amplified the threads bug
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
              
                System.out.println(Thread.currentThread().getName() + " has sold ticket No : " + tickets);
                tickets--;
            } else break;
        }
    }
}
```

运行结果：

```java
> Task :WindowTest2.main()
Window_3 has sold ticket No : 100 // duplicate ticket
Window_2 has sold ticket No : 100 // duplicate ticket
Window_1 has sold ticket No : 100 // duplicate ticket
Window_2 has sold ticket No : 98
Window_3 has sold ticket No : 99
Window_2 has sold ticket No : 96
  ...
Window_2 has sold ticket No : 3
Window_3 has sold ticket No : 2
Window_1 has sold ticket No : 1 // duplicate ticket
Window_2 has sold ticket No : 1 // duplicate ticket
Window_3 has sold ticket No : -1 // illegal ticket
```

* Problem: in ticket sysytem appear duplicate & illegal ticket.
* Reason: During 1 thread havn't finish job other threads access and working also.
* Solution: When 1 thread havn't finish  job other threads will be block.

Java有两种方法解决线程安全问题：

#### 同步代码块 **synchronize**(同步监视器：俗称锁🔒)

* 需要被同步的代码，操作共享数据的代码即为需要被同步的代码。

* 任何object都可以充当锁，所有线程必须使用同样的锁。

缺点： 只可以单线程执行，其他线程等待，效率低。

**extends Threads 同步代码块**

```java
class Window1 extends Threads {
  ...
    // private static Object = new Object;
    pulic void run() {
        while(true) {
          //synchronized (obj) 新建一个静态对象来充当锁
            synchronized (Window1.class) { //同步代码块监视器：Window1.class
              //类也是一种对象，直接用类来充当锁，只会加载一次。
              ....
            }
        }
  }
```

**implements Runnable 同步代码块**

```java
class Window2 implements Runnable {
    private int tickets = 100;

    @Override
    public void run() {
        while(true) {
            synchronized (this) { //同步代码块监视器：this 表示使用当前对象Window2 充当线程锁
                if (tickets > 0) {
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(Thread.currentThread().getName() + " has sold ticket No : " + tickets);
                    tickets--;
                } else break;
            }
        }
    }
}
```

Result:

```java
Window_1 has sold ticket No : 100
Window_1 has sold ticket No : 99
Window_1 has sold ticket No : 98
  ...
Window_1 has sold ticket No : 2
Window_1 has sold ticket No : 1
```

#### 同步方法 

**extends Thread 同步方法**

```java
class Window3 extends Thread {
    private static int tickets = 100;

    @Override
    public void run() {
        while(true) {
            show(); // 调用静态方法
            }
        }

    private static synchronized void show() { // 同步方法监视器：this
        if (tickets > 0) {
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName() + " has sold ticket No : " + tickets);
            tickets--;
        }
    }
}
```

**implements Runnable 同步方法**

```java
class Window4 implements Runnable {
    private int tickets = 100;

    @Override
    public void run() {
        while(true) {
            show(); // 调用方法
        }
    }

    private synchronized void show() { //同步方法监视器：Window4.class
        if (tickets > 0) {
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName() + " has sold ticket No : " + tickets);
            tickets--;
        }
    }
}
```

懒汉式线程安全

```java
package BankTest;

//懒汉式线程安全
public class BankTest1 {
}

class Bank {
    private Bank(){}

    private static Bank instance = null;

    private static synchronized Bank getInstance() {
      //先判断instance 是否等于 null，可以减少多线程重复判断问题，提升效率
        if(instance == null) { 
            synchronized (Bank.class) {
                if(instance == null) instance = new Bank();
            }
        }
        return instance;
    }
}
```

### Deadlock 死锁

```java
package BankTest;

public class ThreadTest {
    public static void main (String[] args) {
        StringBuffer s1 = new StringBuffer();
        StringBuffer s2 = new StringBuffer();

      // thread1先拿锁s1然后sleep 0.1s，然后换锁s2 
        new Thread() {
            @Override
            public void run() {
                synchronized (s1) {
                    s1.append("a");
                    s2.append("1");

                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }

                    synchronized (s2) {
                        s1.append("b");
                        s2.append("2");

                        System.out.println(s1);
                        System.out.println(s2);
                    }
                }
            }
        }.start();
      // thread2 先拿锁s2 然后sleep 0.1s 然后换锁s1
      // 等两个线程苏醒后，都拿不到彼此想要的锁，就变成了死锁
        new Thread(new Runnable() {
            @Override
            public void run() {
                synchronized (s2) {
                    s1.append("c");
                    s2.append("3");

                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }

                    synchronized (s1) {
                        s1.append("d");
                        s2.append("4");

                        System.out.println(s1);
                        System.out.println(s2);
                    }
                }
            }
        }).start();
    }
}

```









