---
title: "Java Data Structure 2: String"
date: 2022-01-02T14:58:11+08:00
draft: true
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Data Structure

---

```java
Module java.base
Package java.lang
  
Class String
  
java.lang.Object
    java.lang.String
  
public final class String extends Object implements Serializable, Comparable<String>, CharSequence
```

String在Java属于`java.lang.Object` package, The `String` class represents character strings. 

String class 是用来创建string对象的，它是**不可改变的**类因为它和Java的原始数据一样都是被预先定义在Java language里面的。

Java 程序中的所有字符串文字，例如`"abc"`，都作为此类的实例实现。

Strings 是常量 constant；它们的值在创建后无法更改，不可变的。



---



**基本上Java的内存可以分为2个部分：heap & stack**，String Pool 是Java在 Heap 堆中开辟出来的一个专门用来存放 String 的内存区。

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

> [`String(String original)`](http://java.sun.com/javase/6/docs/api/java/lang/String.html#String(java.lang.String)) : Initializes a *newly created* `String` object so that it represents the same sequence of characters as the argument; in other words, the newly created string is a copy of the argument string. Unless an explicit copy of original is needed, use of this constructor is unnecessary since strings are immutable. **除非需要原始的显式副本，否则不需要使用new此构造函数**

![String-pool - Edureka](https://www.edureka.co/blog/wp-content/uploads/2017/05/String-pool-1.png)

**因为，Java String 是不可变的和 final 的，所以每当我们进行 String操作时都会  *在Heap堆中创建一个新的 String对象。***



---



### StringBuffer vs StringBuilder

由于字符串操作消耗资源，Java 提供了两个实用程序类：*StringBuffer*和*StringBuilder*。
让我们了解这两个实用程序类之间的区别：

- StringBuffer 和 StringBuilder 是可变类。StringBuffer 操作是线程安全和同步的，而 StringBuilder 操作不是线程安全的。
- 当多个线程在单线程环境中处理相同的 String 和 StringBuilder 时，将使用 StringBuffer。

**正常情况下我们应该避免使用 _StringBuffer_. **因为与 StringBuffer 相比，StringBuilder 的性能更快，因为没有同步的开销。

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201051219120.jpeg)



**What is the capacity of a new StringBuffer object?**

```java
StringBuffer sb = new StringBuffer(String s);

For example:
   StringBuffer sb=new StringBuffer("Tech");
   Capacity = sb.length() + 16 = 4 + 16 = 20 // capacity 20
```



**What is the new capacity of a new StringBuffer object?**

**Ans:** The capacity of a new StringBuffer object can be calculated by using the formula below:

```java
New capacity = ( Current capacity + 1 ) * 2
Thus, New capacity = (16 + 1) * 2 = 34 // new capacity 34
```

Once the 16th character is completed, the next capacity will be 34 if we add 17th character.



---

```java
public static void main(String[] args) 
{ 
   String s = "hello"; 
   s.concat("world"); // concat() method adds string at the end. 
 
   System.out.println(s); // It will print "hello" because string is immutable object. 
 } 

// Output: hello
```

```java
public static void main(String[] args) 
{ 
   String s = "hello"; 
   s = s.concat(" world"); // concat() method adds string at the end. 
 
   System.out.println(ss); // It will print "hello" because string is immutable object. 
 } 

// Output: hello world
```

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201041927445.png)

第一个String s 指向了string pool 的“hello”， s.concat(" world")会同时在string pool创建一个新的string “world”，同时会在heap中创建一个新的string “hello world”。而此时的 s 依然是指向string pool中的 “hello”，所以print s output 依然是“hello”；

### String Compare in Java have 3 ways

> 1. By**` equals()`** method
> 2. By **`==`** operator (double equal operators)
> 3. By **`compareTo()`** method.

```java
public static void main(String[] args) {
        String s1 = "hello";
        String s2 = "hello";
        String s3 =  new String("hello");

        System.out.println(s1.equals(s2)); // true
        System.out.println(s1.equals(s3)); // true
  // equal是方法，比较的是对象的hash值是否相同。例如，名单上两个张三名字一样但身份证号不一样，equal只比较名字相同即为同一个人。

        System.out.println(s1 == s2); // true
        System.out.println(s1 == s3); // false， 
  // == 是运算符，比较的双方是否引用的同一个对象，也就是物理地址是否相同。
  // 例如，名单上两个张三名字一样但身份证号不一样，== 比较的是他们的身份证号也要一样才能算是同一个人。

        System.out.println(s1.compareTo(s2)); // 0
        System.out.println(s1.compareTo(s3)); // 0
  
        StringBuffer sb1 = new StringBuffer("Hello"); 
        StringBuffer sb2 = new StringBuffer("Hello");  
 
        System.out.println(sb1 == sb2); // fasle, == 比较是否指向同一个对象
        System.out.println(sb1.equals(sb2)); //false， 在StringBuffer中，equal也是比较是否饮用同一个对象
  
    }
```



---



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

