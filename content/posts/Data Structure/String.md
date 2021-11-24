---
title: "String"
date: 2021-10-06T16:00:35+08:00
draft: true
toc: false
images:
  - "/images/totoro.jpeg"
tags: 
  - Java
---

## Class String

- [java.lang.Object](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Object.html)
  * java.lang.String

```JAVA
public final class String
extends Object
implements Serializable, Comparable<String>, CharSequence
```

String在Java属于`java.lang.Object` package, The `String` class represents character strings. 

Java 程序中的所有字符串文字，例如`"abc"`，都作为此类的实例实现。

Strings 是常量 constant；它们的值在创建后无法更改，不可变的。

有两种方法可以创建 String 对象:

```java
String s1 = "apple"; // 通过字符串文字
String s2 = "apple";
String s3 = new String("apple"); // 通过 new 关键字
String s4 = new String("apple");
char[] s5 = {'a','p','p','l','e'}; 
```

方法1会新建一个字符串`"Hello World!"`到Java String Pool, 如果遇到同样的字符串，可以指向同一个对象直接引用。所以 s1 == s2 ? true.

方法2会新建一个String Object in Java Heap, 然后variable s 会heap里的对象。s3 == s4 ? False.

** 我们应该避免使用 方法2 去构建新的字符串。**

> [`String(String original)`](http://java.sun.com/javase/6/docs/api/java/lang/String.html#String(java.lang.String)) : Initializes a *newly created* `String` object so that it represents the same sequence of characters as the argument; in other words, the newly created string is a copy of the argument string. Unless an explicit copy of original is needed, use of this constructor is unnecessary since strings are immutable. **除非需要原始的显式副本，否则不需要使用此构造函数**

![String-pool - Edureka](https://www.edureka.co/blog/wp-content/uploads/2017/05/String-pool-1.png)

因为，Java String 是不可变的和 final 的，所以每当我们进行 String 操作时都会创建一个新的 String。由于字符串操作消耗资源，Java 提供了两个实用程序类：*StringBuffer*和*StringBuilder*。
让我们了解这两个实用程序类之间的区别：

- StringBuffer 和 StringBuilder 是可变类。StringBuffer 操作是线程安全和同步的，而 StringBuilder 操作不是线程安全的。
- 当多个线程在单线程环境中处理相同的 String 和 StringBuilder 时，将使用 StringBuffer。

**正常情况下我们应该避免使用 _StringBuffer_. **因为与 StringBuffer 相比，StringBuilder 的性能更快，因为没有同步的开销。

#### [剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

Java 等语言中，字符串都被设计成「不可变」的类型，即无法直接修改字符串的某一位字符，需要新建一个字符串 用`StringBuilder` 来实现。

```java
class Solution {
    public String replaceSpace(String s) {
      // using StringBuilder to build new String
        StringBuilder res = new StringBuilder(); 
      // toCharArray method can convert String to a Char Array, then we use for-each
        for(Character c : s.toCharArray()) 
        {
            if(c == ' ') res.append("%20");
            else res.append(c);
        }
        return res.toString();
    }
}
```

