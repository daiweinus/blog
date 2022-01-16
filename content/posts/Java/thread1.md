---

title: "Java Threads 1: Introduction"
date: 2021-11-20T11:37:08+08:00
draft: true
toc: false
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Threads
---

```java
Module java.base
Package java.lang

java.lang.Object
java.lang.Thread
  
public class Thread
extends Object
implements Runnable
```

## **What are Threads in Java?**

A thread, in the context of Java, is the path followed when executing a program. All Java programs have at least one thread, known as the **main thread**, which is created by the Java Virtual Machine (JVM) at the program’s start, when the **`main()`** method is invoked with the main thread.

* **Program** 程序是指为了完成特定任务，用某一种言语编写的静态代码指令集合。例: 360安全卫士。

* **Process** 进程是指程序的一次执行的动态过程，它有自己的开始，运行，停止生命周期。系统会为每个进程分配不一样的内存区域。 例: 打开运行360安全卫士，系统就会360卫士的运行进程分配内存空间。

* **Thread** 线程是程序的最小执行单位，是程序内部的一条执行路径。在 Java 里所有program 都至少有一个 thread，比如 `main()` thread 它是 JVM 在所有程序开始时创建的。

  * 实际上一个Java.exe程序至少有三个线程：**`main()`主线程**，**`gc`垃圾回收线程** 和 **异常处理线程**。
  * 线程作为调度和执行单位，每个线程都有独立的运行stack 和 pc (程序计数器)。一个进程可以同时执行多个线. 程，就是多线程，多线程之间可以共享相同的内存单元和地址。
  * 例: 迅雷就是程序，正在运行的迅雷就是进程，下载一部电影就是单线程，同时下载多部电影就是多线程。

  **简单的说：程序是静态代码指令集合，进程是动态正在运行的程序，线程是进程的最小执行单位。**

In Java, creating a thread is accomplished by **implementing an interface **and **extending a class**. Every Java thread is created and controlled by the **`java.lang.Thread`** class.

* **并行** 多个CPU同时执行多个任务。

* **并发** 一个CPU同时（时间片）执行多个任务。

![JavaMadeSoEasy.com (JMSE): Thread states/ Thread life cycle in java](https://lh4.googleusercontent.com/oR0_liUxjMnfgFS-fSuc0x2vCCPLQ0Vdw6w2rBVGloaE_84tRNprqNJEJiyI1unMY8Vpj2CDK9GiQGy03_RmteRz-aM31iIQcZsVZhIH2cLrne_5nY9miXKDmQqEHdY60_WopC0)

### There are actually total 4 ways to create thread in java :

1. By extending **`java.lang.Thread`** class

   ```java
   class SampleThread extends Thread {
   
       //method where the thread execution will start 
       public void run(){
           //logic to execute in a thread    
       }
   
       //let’s see how to start the threads
       public static void main(String[] args){
          Thread t1 = new SampleThread();
          Thread t2 = new SampleThread();
          t1.start();  //start the first thread. This calls the run() method.
          t2.start(); //this starts the 2nd thread. This calls the run() method.  
       }
   } 
   ```

2. By implementing **`java.lang.Runnable`** interface

   ```java
   class A implements Runnable{
   
       @Override
       public void run() {
   
           // implement run method here 
       }
   
       public static void main() {
           final A obj = new A();
   
           Thread t1 = new Thread(new A());
   
           t1.start();
       }
   }
   ```

3. By implementing **`java.util.concurrent.Callable`**  interface.

   ```java
   class Counter implements Callable {
   
       private static final int THREAD_POOL_SIZE = 2;
   
       // method where the thread execution takes place
       public String call() {
           return Thread.currentThread().getName() + " executing ...";
       }
   
       public static void main(String[] args) throws InterruptedException,
               ExecutionException {
           // create a pool of 2 threads
           ExecutorService executor = Executors
                   .newFixedThreadPool(THREAD_POOL_SIZE);
   
           Future future1 = executor.submit(new Counter());
           Future future2 = executor.submit(new Counter());
   
           System.out.println(Thread.currentThread().getName() + " executing ...");
   
           //asynchronously get from the worker threads
           System.out.println(future1.get());
           System.out.println(future2.get());
   
       }
   }
   ```

   **Callable 接口支持与 Executor 框架用于线程池。**

   **Runnable 或 Callable 接口优于extends Thread class。**



### There are two ways to create a thread in Java:

```java
// Method 1: Thread creation by extending Thread class
class MultithreadingDemo extends Thread {
    @Override
    public void run(){
        System.out.println(Thread.currentThread().getName());//显示当前线程name
    }
  
    public static void main(String[] args) {
        MultithreadingDemo obj = new MultithreadingDemo();
        obj.start(); // 如果调用obj.run()不行启用新的线程，只会在main线程执行run()方法.
        System.out.println(Thread.currentThread().getName());
    }
}
```

```java
// Method 2: Thread creation by implementing Runnable Interface
class MultithreadingDemo implements Runnable { 
    @Override
    public void run(){  
        System.out.println(Thread.currentThread().getName()); //显示当前线程name
    }   
  
  public static void main(String args[]) {  
     MultithreadingDemo obj = new MultithreadingDemo();  
     Thread tobj = new Thread(obj);  
     tobj.start();  
     System.out.println(Thread.currentThread().getName());
    }  
}
```

### extends Threads vs implements Runnable

![enter image description here](https://i.stack.imgur.com/vLRdp.gif)

- Something that can run inside a Thread (Runnable). 
- Something That can start a new Thread (Thread).

**`implements Runnable`** is the preferred way, it means you can `implement Runnable` and extend from another class as well.

使用 **Runable** 接口的同时，你还可以继承其他类。但是使用**extends Threads**就无法再继承其他类了。

**Inherit less, interface more,** only use inherit when you need override some behavior.

少继承，多接口。只有在你需要重写某些行为时才使用继承。

Multi-threads Ticket system 多线程卖票案例

```java
public class WindowTest1 {
    public static void main (String[] args) {
        Window1 t1 = new Window1();
        Window1 t2 = new Window1();
        Window1 t3 = new Window1();

        t1.setName("Window_1");
        t2.setName("Window_2");
        t3.setName("Window_3");

        t1.start();
        t2.start();
        t3.start();
    }
}

class Window1 extends Thread {
  //if not use static, all 3 every threads will have their own 100 tickets.
    private static int tickets = 100; 
  
    @Override
    public void run() {
        while(true) {
            if(tickets > 0) {
                System.out.println(getName()+ " Sold ticket No: " + tickets);
                tickets--;
            } else break;
        }
    }
}
```

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
  // implenments Runnable means all 3 threads are inherit from 1 object
  // so they will share the 100 tickets, no need use modifier static
    private int tickets = 100;

    @Override
    public void run() {
        while(true) {
            if(tickets > 0) {
                System.out.println(Thread.currentThread().getName() + " has sold ticket No : " + tickets);
                tickets--;
            } else break;
        }
    }
}
```

### 为什么要调用`start()`不直接调用`run()`方法?

如果直接调用这些线程的 run() 方法，则所有线程的执行都由同一个当前线程处理，不会发生多线程. 当通过 start() 方法调用 `run()` 方法时，就会分配一个新的单独线程来执行 `run()` 方法，因此如果有多个线程调用 start() 方法，多线程就行同时运行。

**直接调用`run()`方法**

```java
public class RunMethodExample implements Runnable{
   public void run(){  
      for(int i=1;i<=3;i++){  
	try{
              Thread.sleep(1000);
	   }catch(InterruptedException ie){
		ie.printStackTrace();
	    }  
	 System.out.println(i);  
      }  
   }  
   public static void main(String args[]){  
      Thread th1 = new Thread(new RunMethodExample(), "th1");
      Thread th2 = new Thread(new RunMethodExample(), "th2"); 
      th1.run();  
      th2.run(); 
   }
}
```

output

```java
1
2
3
1
2
3
```

**调用`start()`方法**

```java
public class RunMethodExample2 {
   public void run(){  
     ...
   }  
   public static void main(String args[]){  
      Thread th1 = new Thread(new RunMethodExample(), "th1");
      Thread th2 = new Thread(new RunMethodExample(), "th2"); 
      th1.start();  
      th2.start(); 
   }
}
```

output

```java
1
1
2
2
3
3
```

### 可以在 Java 中启动一个线程两次吗？

不可以，线程一旦启动，就不能再启动。这样做会抛出一个`IllegalThreadStateException`. 

```java 
public static void main(String args[]) {  
	Thread th1 = new Thread(new ThreadTwiceExample(), "th1"); 
	th1.start();  
	th1.start();  
}
```

ouput:

```java
Exception in thread "main" th1 is executing.
java.lang.IllegalThreadStateException
```

