---
title: "创建线程的方式3: Callable"
date: 2021-11-03T15:39:23+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Java
---

```java
package callableTest;

import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.FutureTask;

/**
 * 创建线程方式3：实现 callable 接口。-----JDK5.0新增
 */
public class ThreadNew {
    public static void main (String[] arg) {
        NumThread num = new NumThread();

        // Future接口可以对Runnable, callable的执行结果进行取消，查询和获取。
        // FutureTask 同时实现了Runnable & Future接口，
        // 既可作为线程被Runnable执行，又可以作为Future得到Callable的返回值。
        FutureTask<Integer> futureTask = new FutureTask<>(num);

        new Thread(futureTask).start();

        try {
            //get()返回值即callable实现类override call() 返回值
            Integer sum = futureTask.get();
            System.out.println("sum: " + sum);
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }
    }
}

class NumThread implements Callable<Integer> {

    @Override
    public Integer call() throws Exception {
        int sum = 0;
        for(int i = 1; i <= 10; i++) {
            if(i % 2 == 0) {
                System.out.println(i);
                sum += i;
            }
        }
        return sum;
    }
}
```

```java 
result:
2
4
6
8
10
sum: 30
```



## `Runnable()` vs `Callable()`

1. `call()` 可以 return 有返回值。
2. `call()` 可以抛出异常。
3. `Callable()`支持泛型。

