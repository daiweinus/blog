---
title: "i++ vs ++i"
date: 2021-10-20T10:20:00+08:00
draft: true
toc: false
images:
  - "/images/totoro.jpeg"
tags: 
  - Java
---

```java
public class Main {
    public static void main (String[] args) {
        int a = 0, b = 0;
        for (int i = 0; i < 1; i++) {
            System.out.println(a += i); // a = 0
            System.out.println(i++); // i++ = 0
            System.out.println(i); // i = 1
        }

        for (int i = 0; i < 1; ++i) {
            System.out.println(b += i); // b = 0
            System.out.println(++i); // ++i = 1
            System.out.println(i); // i = 1
        }
    }
}
```

From the above example we can clear see that, after 1 loop cycle i++ = 0 & ++i = 1，but its not affected the for loop compute, the variables a & b value still equal to 0.

i++ & ++i 只会影响本身单独计算结果 (i++是先print i 的value 再 做加法； ++i 是先做加法再print i 的value），

但不管是 i++ 还是 ++i 都不会影响 for loop 循环的计算结果。
