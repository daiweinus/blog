---
title: "Java Operator 1: Bitwise Operator"
date: 2021-11-01T13:13:13+08:00
draft: true
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Operator

---

An operator that acts on individual bits (0 or 1) of the operands is called **bitwise operator in java**.

It acts only integer data types such as byte, short, int, and long. Bitwise operators **in java cannot be applied to float and double** data types. 

操作 bit 单位 0 和 1 成为 位操作， 在Java 位操作只可以使用在整数，不可以在小数上使用。

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201061246513.png)

### Bitwise Operator Table:

| Operator |         Meaning          |
| :------: | :----------------------: |
|   1. &   |       bitwise AND        |
|  2. \|   |        bitwise OR        |
|   3. ^   |   bitwise exclusive OR   |
|   4. ~   | one’s complement (unary) |
|  5. <<   |        shift left        |
|  6. >>   |       shift right        |
|  7. >>>  |   unsigned right shift   |



---

### AND, OR, XOR & NOT

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201061221620.jpeg)

```java
public class BitwiseOperatorTest {
    public static void main(String[] args) {

        // |: 或 OR, 0|0 = 0; 1|0 1|1 = 1
        System.out.println(6 | 3); // 110 | 011 -> 111 = 7

        // &: 与 AND, 1&1 0&0 = 1; 0&1 = 0
        System.out.println(6 & 3); // 110 & 011 -> 010 = 2

        // ~: 非 NOT, 0 -> 1; 1 -> 0 一元操作符 one’s complement (unary)
        // 110 -> 0000 0110 ~运算后得到 -> 1111 1001 为负数，需转换为十进制
        // 1111 1001 -> 0000 0110 + 1 -> 0000 0111 = 7, 加上负号 -7
        System.out.println(~6); // -7
        System.out.println(-6); // 5

        // ^: 异或 XOR, 0^0 1^1 = 0; 0^1 = 1
        System.out.println(6 ^ 3); // 110 ^ 011 -> 101 = 5

        // >>：带符号右移。正数右移高位补0，负数右移高位补1。
        System.out.println( 8 >> 1); // 0000 1000 -> 0100 = 4
        System.out.println(-8 >> 1); // 1111 1000 -> 1111 1100 = -4

        // <<：带符号左移。无论是正负，都是低位补0。
        System.out.println( 8 << 1); // 0000 1000 -> 0001 0000 = 16
        System.out.println(-8 << 1); // 1111 1000 -> 1111 0000 = -16

        // >>>：无符号右移。无论是正负，都是高位补0。
        System.out.println( 8 >>> 1); // 1000 -> 0100 =4
        System.out.println(-8 >>> 1); 
        // 11111111 11111111 11111111 1111 1000 -> 00111111 11111111 11111111 1111 1100 = 2147483644

        // 没有 <<< 无符号左移
    }
}
```

```java
> Task :BitwiseOperatorTest.main()
6 | 3 = 7
6 & 3 = 2
~6 = -7
~(-6) = 5
6 ^ 3 = 5
8 >> 1 = 4
-8 >> 1 = -4
8 << 1 = 16
-8 << 1 = -16
8 >>> 1 = 4
-8 >>> 1 = 2147483644
```

---

### <<  Left Shift Operator in Java 带符号左移。无论是正负，都是低位补0。

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201061259363.png)

**Key point:** Shifting a value to the left, n bits, is equivalent to multiplying that value by 2^n.

For example: In the above expression, n = 3. So, 20 * 2^3 = 20 * 8 = 160.

**20 左移 3位 等于 20 x $2^3$ = 20 x 8 = 160**

---

### >> Right Shift Operator in Java 带符号右移。正数右移高位补0，负数右移高位补1。

***1) 10 >> 3***

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201061306429.png)

**Key point:** Shifting a value to the right is equivalent to dividing the number by 2^n.

**10 右移 3位 等于 10 / $2^3$ = 10 / 8 = 1**



***2)  -10 >> 2***

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201061326254.png)

> 1. 10  = `0000 1010`
> 2. 1's complement form  反码 `1111 0101`
> 3. 2‘s complement form  补码 `1111 0101` + 1 = `1111 0110` = -10
> 4. 10 >> 2 = `1111 1101 10 ` 舍掉最后2位 = `1111 1101` 
> 5. 1111 1101 为负数，需转换成10进制Decimal 得到正整数位，再添加负号
> 6. 2‘s complement form 反补码  `1111 1101` - 1 = `1111 1100`
> 7. 1's complement form  反码` 0000 0011` = 3
> 8. -10 >> 2 = `1111 1101` = -3

---

### >>> Unsigned Right Shift Operator  无符号右移。无论是正负，都是高位补0。

`>>>`, read as triple greater than.

**>>  vs  >>>** 两者都是向右位移，但是`>>>`没有正负之分，如果是负数>>>右移结果会变成正数。

>-10 >>> 2
>
>1. -10 =  `1111 32位制 1111 0110` >>> 2 = `0011 1111 1111 1111 1111 1111 1111 1101 10` 
>2. 舍弃最末2位 = `0011 1111 1111 1111 1111 1111 1111 1101`
>3. `11 1111 1111 1111 1111 1111 1111 1101`转换成十进制Decimal  = 1073741821

---

### Why need use bitwise operator?

1. The average `1` and `2147483647` (`Integer.MAX_VALUE`).

2. ```java
   (1 + 2147483647) / 2 = 2147483648 / 2 = 1073741824  // in math
   ```

3.  `(1 + 2147483647) / 2` code execute in computer 

    ```java
              1: 00000000 00000000 00000000 00000001
    +2147483647: 01111111 11111111 11111111 11111111
    ================================================
    -2147483648: 10000000 00000000 00000000 00000000  // Overflow, MSB is 1 menas nagetive '-'
    /2
    ================================================
    -1073741824: 11000000 00000000 00000000 00000000  // Signed divide, same as >> 1.
    ```

4. `(1 + 2147483647) >>> 1` code execute in computer

   ```java
             1: 00000000 00000000 00000000 00000001
   +2147483647: 01111111 11111111 11111111 11111111
   ================================================
   -2147483648: 10000000 00000000 00000000 00000000  // Overflow
   >>> 1
   ================================================
   +1073741824: 01000000 00000000 00000000 00000000  // Unsigned shift right >>> 1 got correct result
   ```

Sample code as below:

```java
int res1 = (1 + Integer.MAX_VALUE) / 2;
int res2 = (1 + Integer.MAX_VALUE) >> 1;
int res3 = (1 + Integer.MAX_VALUE) >>> 1;

System.out.println(res1);
System.out.println(res2);
System.out.println(res3);
```

```
res1 = -1073741824
res2 = -1073741824
res3 = 1073741824
```



---

#### [36. 只出现一次的数字](https://leetcode-cn.com/problems/single-number/)

示例：

```java
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。
输入: [4,1,2,1,2]
输出: 4
  
// 所有元素都出现2次，只有一个只出现1次。 
// 如果两个数字一样，用 XOR 的特性可以把所有重复出现的元素消除，只留下唯一的元素

  4 ： 100
^ 1 ： 001
^ 2 ： 010
^ 1 ： 001
^ 2 ： 010
==========
  4 : 100   
```

```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for(int num : nums) res ^= num; 
        return res;
    }
}
```

#### [704. 二分查找](https://leetcode-cn.com/problems/binary-search/)

```java
public class BinarySearch {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("Please enter the Integer Arrays: ");
        String input = sc.nextLine(); // receive array input

        String[] newInput = input.split("\\s+"); // split string into string array
        System.out.println(newInput.length);

        int[] array = new int[newInput.length];

        for(int i = 0; i < array.length; i++) {
            array[i] = Integer.parseInt(newInput[i]); // parse string array element to int array element
        }

        System.out.println("Please enter the target number you want search: ");
        int target = sc.nextInt(); // receive target input

        int res = binarySearch(array,target);
        System.out.println(res);
    }

    public static int binarySearch(int[] array, int target) {
        int low = 0; 
        int high = array.length - 1;

        while (low <= high) {
            int mid = (low + high) >>> 1; // bitwise >>> operator to avoid stack overflow
            // int mid = low + (high -low) / 2;
            
            int midNum = array[mid];
            if (target > array[mid]) low = mid + 1;
            else if (target < array[mid]) high = mid - 1;
            else return mid;
        }
        return -1;
    }

}
```



---

### **Appendix**

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202201061433458.png)