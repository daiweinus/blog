---
title: "Array"
date: 2021-10-11T14:49:45+08:00
draft: true
toc: false
images:
  - "/images/totoro.jpeg"
tags: 
  - Java
---

### util.Arrays class:

```java
java.lang.Object
java.util.Arrays
public class Arrays extends Object
```

This class contains various methods for manipulating arrays (such as sorting and searching). This class also contains a static factory that allows arrays to be viewed as lists. 

此类[Java Collections Framework](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/package-summary.html#CollectionsFramework)的成员, 包含用于操作数组的各种方法（例如排序和搜索）。此类还包含一个静态工厂，允许将数组视为列表。它仅由静态方法和 Object 类的方法组成。

![数组 - Java 数组 - edureka](https://www.edureka.co/blog/wp-content/uploads/2018/01/7-2.png)

有两种方法可以创建 Arrays 对象:

```java
// method 1, declare a new array1 then initialize it
int[] array1 = new int[3]; 
array1 = {1,2,3}; 

// method 2, initialized array2 when declared it
int[] array2 = new int[]{1,2,3}; 

// method 3, declare with values given (variable/field initialization):
int[] array3 = {1,2,3};

// Matrix Array
int[][] matrix1 = new int[2][3];
matrix1[0][0] = 1;
matrix1[0][1] = 2;
matrix1[0][2] = 3;
matrix1[1][0] = 4;
matrix1[1][1] = 5;
matrix1[1][2] = 6;

// Martix Array
int[][] matrix2 = {
  {1,2,3},
  {4,5,6}
};

System.out.println(Arrays.toString(array3)); // [1, 2, 3]
System.out.println(Arrays.deepToString(matrix2)); //[[1, 2, 3], [4, 5, 6]]
System.out.println(matrix1.length); // Prints the First Dimension size in the array 2
System.out.println(matrix1[0].length);//Prints the Second Dimension size in the array 3
```

3种创建方法其实是一样的，但是当你需要return一个array时，你需要`return new int[]{1,2,3}`,不可以直接`return {1,2,3}`.



---

### length vs length() vs size()

* `length` -- **arrays** (`int[]`, `double[]`, `String[]`) -- to know the length of the arrays

* `length()` -- **String related Object** (`String`, `StringBuilder`, etc) -- to know the length of the String

* `size()` -- **Collection Object** (`ArrayList`, `Set`, etc) -- to know the size of the Collection

array 在Java 中有一些特殊，类似Java的原始类，array的长度length是需要在使用前申明的，更像是一个constant，因此由于历史原因，早期的Java designer 更愿意把 array length 当做 一个私有field 才处理，而不是伪装method。

string 的长度是可变的 dynamic，所以需要call method 去计算长度。

---

#### [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

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
    }
}
```



![2D Array - Java array - edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/01/Asset-2@2x.png)

---

### reflect.Array Class:

```java
java.lang.Object
java.lang.reflect.Array
public final class Array extends Object
```

The `Array` class provides static methods to dynamically create and access Java Arrays. 

此类提供静态方法去动态创建和访问Java Arrays。它是一个 final 类，这意味着它**不能被实例化或改变**。使数组保持类型安全。

**util.Array vs reflect.Arrays:**

```java
// Java program to show Array vs Arrays  
import java.lang.reflect.Array; 
import java.util.Arrays; 
  
public class GfG { 
    public static void main(String[] args) 
    { 
        // Get the size of the array 
        int[] intArray = new int[5]; 
  
        // Add elements into the array 
        // using reflect.Array class 
        Array.setInt(intArray, 0, 10); 
  
        // Printing the Array content 
        // using util.Arrays class 
        System.out.println( 
            Arrays.toString(intArray)); 
    } 
} 
```

