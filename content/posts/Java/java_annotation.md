---
title: "Java Annotation注解"
date: 2021-10-20T17:26:19+08:00
draft: true
toc: false
images:
  - "/images/totoro.jpeg"
tags: 
  - Java
---

The predefined [annotation](https://docs.oracle.com/javase/tutorial/java/annotations/index.html) types defined in `java.lang` are **`@Deprecated`, `@Override`, and `@SuppressWarnings`**.

[`@Deprecated`](https://docs.oracle.com/javase/8/docs/api/java/lang/Deprecated.html)注释表示被标记的元素已被*弃用*，不应再使用。每当程序使用带有`@Deprecated`注释的方法、类或字段时，编译器都会生成警告

[`@Override`](https://docs.oracle.com/javase/8/docs/api/java/lang/Override.html)注释通知编译器该元素旨在覆盖超类中声明的元素。覆盖方法将在[接口和继承中](https://docs.oracle.com/javase/tutorial/java/IandI/index.html)讨论 。虽然在覆盖方法时不需要使用此注释，但它有助于防止错误。如果标记为 的方法`@Override`未能正确覆盖其超类之一中的方法，则编译器会生成错误

[`@SuppressWarnings`](https://docs.oracle.com/javase/8/docs/api/java/lang/SuppressWarnings.html)注释告诉编译器抑制它会生成的特定警告。

使用 annotation 注释并不是必须的，没有使用 annotation 并不会影响程序的任何功能。

但是如果你使用`@Override`注释一个方法但你没有覆盖任何东西，编译器会提示bug, 这是一个低成本高效率增加代码可维护性的方法，非常推荐使用。

从 Java SE 8 版本开始，注释也可以应用于任何*类型的 use*。这意味着可以在使用类型的任何地方使用注释。使用类型的一些示例是类实例创建表达式 ( `new`)、强制转换、`implements`子句和`throws`子句。创建类型注释是为了支持改进的 Java 程序分析方法，以确保更强大的类型检查。

```java
@Entity

@Override
void mySuperMethod() { ... }

@Author(
   name = "Benjamin Franklin",
   date = "3/27/2003"
)
class MyClass { ... }

//If only one element named value, then the name can be omitted
@SuppressWarnings(value = "unchecked")
void myMethod() { ... }

//multiple annotations on the same declarati
@Author(name = "Jane Doe")
@EBook
class MyClass { ... }

//Type cast
myString = (@NonNull String) str;

//implements clause:
class UnmodifiableList<T> implements
    @Readonly List<@Readonly T> { ... }

//Thrown exception declaration:
void monitorTemperature() throws
    @Critical TemperatureException { ... }

```

