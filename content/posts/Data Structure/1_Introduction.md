---
title: "Java Data Structure 1: Introduction"
date: 2022-01-01T14:00:11+08:00
draft: true
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Data Structure

---

程序简而言之就是数据+算法，根据数据的属性 **Java data structure** 可以分为两大类：**primitive data types & non-primitive data types**.

> Primitive data types: **byte, short, int, long, float, double, char, boolean.** 
>
> Non-primitive data types: **String, Array, Class, Interface, Object**.

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201041727487.png)

---

### Primitive Data Types (also called built-in types)

下面以 **Integer ** 为例：

```java
Module java.base
Package java.lang
   
Class Integer
  
java.lang.Object
    java.lang.Number // Number包里还包含：BigDecimal,Byte, Double,Float, Integer, Long,Short 等子包
        java.lang.Integer
  
public final class Integer extends Number implements Comparable<Integer>
```

The **Integer class** wraps a value of the **primitive type  int** in an object. An object of type Integer contains a **single field** whose type is int.     Integer类 把原始数据类型 int 的封装为一个对象。



![DataTypes - Data types in Java - Edureka](https://www.edureka.co/blog/wp-content/uploads/2017/04/Primitive_Data_Type.png)



* **byte, short, int, long, float, double, char, boolean.** 

* 1 bit; 1 byte = 8 bits; 1kilobyte = 1024 bytes; 1 Megabyte = 1024 KBs .....因为1970年代的计算机CPU一次最多只能处理**8bits**的数据，所以就有了**byte**, byte is **the basic addressable unit**, below which computer architecture cannot address. 

* **`char` in Java** is **UTF-16 encoded**, which requires a minimum of **16-bits (2bytes)** of storage for each character.

  **`char` in C** programming is **ASCII encoded** which only covers the english language character set, and the range is 127, which requries a minimum of **8-bits (1byte)** of storage for each character.

  |   Type    | Size (bits)  |                         Minimum                         |  Maximum   |    Default Value    |
  | :-------: | ------------ | :-----------------------------------------------------: | :--------: | :-----------------: |
  |  *byte*   | 8 / 1byte    |                         $-2^7$                          |  $2^7-1$   |    *byte b = 0;*    |
  |  *short*  | 16 / 2bytes  |                        $-2^{15}$                        |  $2^15-1$  |   *short s = 0;*    |
  |   *int*   | 32 / 4 bytes |                        $-2^{31}$                        | $2^{31}-1$ |    *int i = 0;*     |
  |  *long*   | 64 / 8 bytes |                        $-2^{63}$                        | $2^{63}-1$ |    *long l = 0*     |
  |  *float*  | 32 / 4 bytes | 1 sign bit, 8 bits of exponent, 23 bits of significand  |            |  *float f = 0.0f*   |
  | *double*  | 64 / 8 bytes | 1 sign bit, 11 bits of exponent, 52 bits of significand |            |  *double d = 0.0d*  |
  |  *char*   | 16 / 2 bytes |                            0                            | $2^{16}-1$ | *char c =  ‘u0000’* |
  | *boolean* | 1 / 1 bytes  |                            –                            |     –      | *boolean b = false* |

> **在《Effective  Java》这本书中提到这个原则，float和double只能用来做科学计算或者是工程计算，在商业计算中我们要用java.math.BigDecimal。使用BigDecimal并且一定要用String来够造。**

```java
public static double add(double v1,double v2){    
    BigDecimal b1 = new BigDecimal(Double.toString(v1));    
    BigDecimal b2 = new BigDecimal(Double.toString(v2));    
    return b1.add(b2).doubleValue();    // v1 + v2
}  
```

> A primitive data type is pre-defined by the programming language. The size and type of variable values are specified, and it has no additional methods.  
>
> 原始数据的大小和类型都是提前规定好的，并且不提供额外的方法，这就是为什么我们需要非原始数据，例如 Array, List, Set & Map 来帮助我们更高效的完成数据操作。
>
> 所有的原始数据都是小写，并且有一个默认值。
>
> 所有原始类型数据变量都存储在**stack栈**。

---

### Non-primitive Data Types (also called reference data type)

非原始数据类型是Java程序员为了更加方便的存储和操控数据而在后期创造的，也被称为高级数据类型。

> 非原始数据类型的首字母都是**大写**；
>
> 非原始数据类型的默认值都是**null**；
>
> 非原始数据类型存储在**Heap堆**，**stack堆**上只是保存了一个指向heap的对象的指针；
>
> 将非原始数据类型的值传递给方法是指实际传递存储数据的对象的地址。

Non-primitive data types: **String, Array, Class, Interface, Object**

1. **class & object：**每个类都是数据类型，也被认为是用户定义的数据类型。
2. **interface：**接口的声明方式与类类似，但唯一的区别是它只包含最终变量和方法声明。
3. **string & array**: 常用的非原始数据类型，string也是一个class。

![Java Collections](https://beginnersbook.com/wp-content/uploads/2013/12/Java-collection-framework-hierarchy.png)





---

### Primitive Data Types VS Non-Primitive Data Types

The main difference between **primitive** and **non-primitive** data types are:

- Primitive types are predefined (already defined) in Java. Non-primitive types are created by the programmer and is not defined by Java (except for `String`). 

  原始数据类型都是被Java language 提前定义好的，非原始数据除了**String**, 其他都是后期定义的。

  

  [java.lang](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/package-summary.html): 

  * [Byte](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Byte.html), [Short](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Short.html), [Integer](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Integer.html), [Long](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Long.html), [Float](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Float.html), [Double](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Double.html), [Character](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Character.html), [Boolean](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Boolean.html).

  * [String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html).

    

- Non-primitive types can be used to call methods to perform certain operations, while primitive types cannot. 

  非原始数据类型可以使用方法操作数据，非原始数据类型没有定义额外方法。

- A primitive type has always a value, while non-primitive types can be `null`.

  原始数据类型都有一个值或者不能为null的默认值。而所有的非原始数据默认值是**null**。

- A primitive type starts with a lowercase letter, while non-primitive types starts with an uppercase letter. 

  原始数据类型小写开头，非原始数据大写开头。

- The size of a primitive type depends on the data type, while non-primitive types have all the same size.

  原始数据类型大小是固定的存储在**stack栈**，非原始数据类型大小都是动态的存储在**heap堆**。

- 原始数据类型是pass by value（copy值），原始数据不会被method改变。

  非原始数据类型是pass by reference（copy物理地址）, 原始数据可以被method改变。

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201041845283.png)

![](https://pica.zhimg.com/v2-5dd21bea8b50af177e31351ed0a2ea8d_r.jpg?source=172ae18b)

![](https://static.javatpoint.com/ds/images/ds-introduction.png)

![img](https://img-blog.csdnimg.cn/img_convert/5253e82f78c3e235799fe38bfab6f097.png)

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201111624931.png)