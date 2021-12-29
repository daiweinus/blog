---
title: "多线程通信安全 Thread Communication synchronized"
date: 2021-11-03T13:16:20+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Java
---

```java
/**
 * 线程通信例子：两个线程交替打印 integer 1-10
 * 涉及3个方法：
 * wait(): 当前线程进入wait状态，并释放线程监视器。
 * notify(): 唤醒一个处于wait状态中优先级最高的线程。
 * notifyAll(): 唤醒所有处于wait状态的线程。
 *
 * 1. 3个方法都必须是用在同步代码块或者同步方法中。
 * 2. 3个方法的调用者必须是同步代码块或者同步方法中的同步监视器。
 * 3. 3个方法是定义在java.Lang.Object类中， 并不是 thread 类中。
 */
public class CommunicationTest {
    public static void main (String[] args) {
        NumberPrinter n = new NumberPrinter();
        Thread t1 = new Thread(n);
        Thread t2 = new Thread(n);

        t1.start();
        t2.start();
    }
}

class NumberPrinter implements Runnable {
    int i = 1;
  
    @Override
    public void run() {
        while (true) {
            synchronized (this) {
                notify(); // 必须使用同步监视器this来调用，this.notify = notify
                if(i <= 10) {
                    System.out.println(Thread.currentThread().getName() + ": " + i);
                    i++;

                    try {
                        wait(); //this.wait
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }else break;
            }
        }
    }
}
```

## `sleep()` vs `wait()`

**相同点：**都可以让线程进入block状态。

**不同点：**

1. 声明位置不同：thread类中声明`sleep()`, object类中声明`wait()`;  
2. 调用要求不同：`sleep()`可在任何地方调用，`wait()`只能在同步代码块或方法中调用；
3. `sleep()`不会释放同步监视器，`wait()`会释放同步监视器。



## 生产者-消费者问题

```java
package communicationTest;

public class ProductTest {
    public static void main (String[] args) {
        Clerk clerk = new Clerk();
        Producer p1 = new Producer(clerk);
        Consumer c1 = new Consumer(clerk);
        Consumer c2 = new Consumer(clerk);

        p1.setName("p1");
        c1.setName("c1");
        c2.setName("c2");

        p1.start();
        c1.start();
        c2.start();
    }
}

class Clerk {
    private int production = 0;

    public synchronized void produceProduct() {
        if(production < 20) {
            production++;
            System.out.println(Thread.currentThread().getName() + ": START PRODUCE" + production);
            notify();
        } else {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public synchronized void consumeProduct() {
        if(production > 0) {
            System.out.println(Thread.currentThread().getName() + ": START consume" + production);
            production--;
            notify();
        } else {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class Producer extends Thread {
    private Clerk clerk;

    public Producer (Clerk clerk) {
        this.clerk = clerk;
    }

    @Override
    public void run() {
        System.out.println(getName() + "Start produce...");

        while (true) {
            clerk.produceProduct();
        }
    }

}

class Consumer extends Thread {
    private Clerk clerk;

    public Consumer (Clerk clerk) {
        this.clerk = clerk;
    }

    @Override
    public void run() {
        System.out.println(getName() + "Start consume...");

        while (true) {
            clerk.consumeProduct();
        }
    }
}
```

### `notify()` vs `notifyAll()`

 * notify(): 唤醒 **一个** 处于wait状态中**优先级最高**的线程。
 * notifyAll(): 唤醒 **所有** 处于wait状态的线程。
