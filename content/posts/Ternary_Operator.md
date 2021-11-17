---
title: "Ternary Operator 三元运算符"
date: 2021-10-12T13:28:50+08:00
draft: true
toc: false
images:
  - "/images/totoro.jpeg"
tags: 
  - Java
---

**Syntax:**

```java
Variablename = (Condition) ? the value assigned if 'true' is returned: t
```

example：

```java
if (BooleanValue) {
   Greetings = "Hello!";
}
else {
   Greetings = "Bye!";
}
```

using ternary operator the above expression involves 1 line:

```java
Greeetings = (BooleanValue) ? "Hello!" : "Bye!";
```

**Chained Operations**

```java
public class Ternaryy {
   public static void main(String[] args) {
 
       String coffeeOrder = "Piccolo Latte";
       if (coffeeOrder == "Espresso" ) {
           System.out.println("would you like whipped cream on the top");
       } else if (coffeeOrder == "Piccolo Latte") {
           System.out.println("25ml or 30ml");
       } else if (coffeeOrder == "Macchiato") {
           System.out.println("Short or long");
       } else {
           System.out.println("Hello, we were unable to process your order");
 
       }
   }
}
```

use the ternary operator:

```java
public class Ternaryy {
   public static void main(String[] args) {
       String coffeeOrder = "Piccolo Latte";
       String FinalOrder = (coffeeOrder == "Espresso") ? 
         " would you like whipped cream on the top" : (coffeeOrder == "Piccolo Latte") ?
           "25ml or 30ml" : (coffeeOrder == "Macchiato") ? 
             "Short or long" : "Hello, we were unable to process your order";
       System.out.println(FinalOrder);
   }
}
```

