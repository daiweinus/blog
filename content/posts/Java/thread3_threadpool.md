---
title: "Java Threads 3: threadpool"
date: 2021-11-22T15:57:02+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Java Threads
---

提前建好多个线程放入线程池中，使用时直接获取。避免频繁创建销毁线程，实现线程重复利用。

线程池类似公交车🚌，每个人都可以按自己的需选择乘坐任何一辆公交车。

好处：

1. 建好线程创建时间，提高程序相应速度。
2. 线程可重复利用，降低系统资源消耗。
3. 便于线程管理，提高编程效率。

线程池API: 

1. ExecutorService 线程池接口，常见子类 ThreadPoolExecutor
2. Executor 工具类，线程池工厂类，用于创建并返回不同类型的线程。

```java 
package threadpool;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

/**
 * 线程创建方式4： ThreadPool
 */
public class ThreadPool {
    public static void main(String[] args) {
        ExecutorService service = Executors.newScheduledThreadPool(10);

        //设置线程池属性，先把ExecutorService 转换成 ThreadPoolExecutor
        //ThreadPoolExecutor service1 = (ThreadPoolExecutor) service;
        //service1.setCorePoolSize(5);
        //service1.setKeepAliveTime(100, TimeUnit.MILLISECONDS);

        //service.submit(Callable callable);//适合适用于Callable
        service.execute(new NumberThread1());//适合使用于Runnable
        service.execute(new NumberThread2());

        service.shutdown();//关闭线程池
    }
}

class NumberThread1 implements Runnable {

    @Override
    public void run() {
        for (int i = 1; i <= 10; i++) {
            if (i % 2 == 0) {
                System.out.println(Thread.currentThread().getName() + ": " + i);
            }
        }
    }
}

class NumberThread2 implements Runnable {

    @Override
    public void run() {
        for (int i = 1; i <= 10; i++) {
            if (i % 2 != 0) {
                System.out.println(Thread.currentThread().getName() + ": " + i);
            }
        }
    }
}
```

