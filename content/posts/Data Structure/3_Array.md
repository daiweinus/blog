---
title: "Java Data Structure 3: Array"
date: 2022-01-03T14:59:11+08:00
draft: true
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Data Structure

---

```java
Module java.base
Package java.lang.reflect
  
Class Array
  
java.lang.Object
    java.lang.reflect.Array
  
public final class Array extends Object
```

**The `Array` class provides static methods to dynamically create and access Java arrays. ** Array class 是定义在Java.lang的基础语言包里，提供了一个静态方法可以动态创建和访问数组。

```java
Module java.base
Package java.util
  
Class Arrays
  
java.lang.Object
    java.util.Arrays
  
public class Arrays extends Object
```

**This class contains various methods for manipulating arrays (such as sorting and searching). ** Arrays class是一个工具类，为操作array数据提供额外方法。是 Array to ArrayList 的桥梁。

例如下面代码里的`Arrays.toString()`帮助把array转换成string方便打印：

```java
public static void main(String[] args){
        int[] array1 = {1,2,3};
        System.out.println(Arrays.toString(array1)); // Arrays.toString() method
    }
```



---



**Array数组是将相同类型的元素存储于连续内存空间的数据结构，其长度需要提前声明且不可变。**

Array 存储在  **Heap** 。

Array 主要分为两类：**one-dimensional array 一元数组 & Multidimensional arrays 多元数组**

![数组 - Java 数组 - edureka](https://www.edureka.co/blog/wp-content/uploads/2018/01/7-2.png)

在Java里，Array属于Object, 而所有的Object都属于 Class， 因此我们可以用 **`new`** keyword 来创建新的Array 对象。构建数组需要在初始化时给定长度，并对数组每个索引元素赋值，创建 Arrays 的方法如下：

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201051530909.png)

```java
// method 1, declare a new array1 then initialize it
int[] array1 = new int[3]; 
array1[0] = 1; 
array1[1] = 2;
array1[2] = 3;

// method 2, initialized array2 when declared it
int[] array2 = new int[]{1,2,3}; 

// method 3, declare with values given (variable/field initialization):
int[] array3 = {1,2,3};

// Matrix Array method 1
int[][] matrix1 = new int[2][3];
matrix1[0][0] = 1;
matrix1[0][1] = 2;
matrix1[0][2] = 3;
matrix1[1][0] = 4;
matrix1[1][1] = 5;
matrix1[1][2] = 6;

// Martix Array method 2
int[][] matrix2 = {
  {1,2,3},
  {4,5,6}
};

System.out.println(Arrays.toString(array3)); // [1, 2, 3]
System.out.println(Arrays.deepToString(matrix2)); //[[1, 2, 3], [4, 5, 6]]
System.out.println(matrix1.length); // Prints the First Dimension size in the array 2
System.out.println(matrix1[0].length);//Prints the Second Dimension size in the array 3
```

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201051536994.png)



3D Matrix Array:

```java
// method 1
int[ ][ ][ ] scores = new int[3][3][3]; 

// method 2
int[ ][ ][ ] scores = {
                        {{75, 87, 69}, {90, 87, 85},{56, 67, 76}},
                        {{78, 67, 75}, {87, 98, 76}, {67, 56, 66}},
                        {{72, 63, 72}, {82, 91, 71}, {64, 56, 66}}
                       };
```



---

### Array copy in Java

```
array2 = array1;
```

此处，不会将array1 引用（即指向）的数组元素复制到array2。它只是将引用地址从 array1 复制到 array2。

由于array1 和array2 引用同一个数组，因此不再引用array2 指向的前一个数组，现在它变成了垃圾，JVM的垃圾回收器会自动收集。

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201051647254.png)



---

### length vs length() vs size()

* `length` -- **arrays** (`int[]`, `double[]`, `String[]`) -- to know the length of the arrays

* `length()` -- **String related Object** (`String`, `StringBuilder`, etc) -- to know the length of the String

* `size()` -- **Collection Object** (`ArrayList`, `Set`, etc) -- to know the size of the Collection

array 在Java 中有一些特殊，类似Java的原始类，array的长度length是需要在使用前申明的，更像是一个constant，因此由于历史原因，早期的Java designer 更愿意把 array length 当做 一个私有field 才处理，而不是伪装method。

string 的长度是可变的 dynamic，所以需要call method 去计算长度。

---

### [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++) {
            int n = target - nums[i];
            if(map.containsKey(n)) return new int[]{map.get(n), i};
            map.put(nums[i],i);
        }
        return new int[]{}; 
      //当你需要return一个新的array时，你需要 return new int[]{1,2,3},不可以直接 return {1,2,3}
    }
}
```

#### [704. 二分查找](https://leetcode-cn.com/problems/binary-search/)

