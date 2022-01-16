---
title: "Java Fundament 3: Java OOP"
date: 2021-10-03T11:30:25+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Java Fundament
---

Object-oriented programming (OOP) is a programming based on the concept of “objects” that contain data and methods. The primary purpose of object-oriented programming is to increase the flexibility and maintainability of programs. Object oriented programming brings together data and its behaviour(methods) in a single location(object) makes it easier to understand how a program works.

面向对象程序设计（Object Oriented Programming，OOP）是一种计算机编程架构。OOP的一条基本原则是计算机程序由单个能够起到子程序作用的单元或对象组合而成。OOP达到了软件工程的三个主要目标：重用性、灵活性和扩展性。OOP=对象+类+继承+多态+消息，其中核心概念是类和对象。

除了OOP, 还有面向过程(Procedure Oriented Programming)，是一种以过程为中心的编程思想。这些都是以什么正在发生为主要目标进行编程。函数式编程（Functional Programming），data更多的围绕operation， 所以添加新的方法很容易。

### What is an Object

什么是对象？对象就是一组数据 data 和行为 behaviour (aka method).

**Example :**
**Object**: House
**State**: Address, Color, Area
**Behavior**: Open door, close door

### Characteristics of Objects:

**Abstraction**: Abstraction is a process where you show only “relevant” data and “hide” unnecessary details of an object from the user.

**Encapsulation**: Encapsulation simply means binding object state(fields) and behaviour(methods) together. If you are creating class, you are doing encapsulation.

**Message passing**
A single object by itself may not be very useful. An application contains many objects. One object interacts with another object by invoking methods on that object. It is also referred to as **Method Invocation**. See the diagram below.

### Object Oriented Programming features

![OOPs features, Object-oriented-programming-features](https://beginnersbook.com/wp-content/uploads/2013/04/Object-oriented-programming-features.jpg)

#### Abstraction 抽象

Abstraction is a process of hiding the implementation details from the user, only the functionality will be provided to the user. In other words, the user will have the information on what the object does instead of how it does it.
In Java, abstraction is achieved using **Abstract classes** and **interfaces**.

抽象就是对用户隐藏程序的执行细节，只提供功能给用户。

#### Inhertance 继承

Inheritance can be defined as the process where one class acquires the properties (methods方法 and fields属性) of another. With the use of inheritance the information is made manageable in a hierarchical order.

The class which inherits the properties of other is known as subclass (derived class, child class) and the class whose properties are inherited is known as superclass (base class, parent class). **extends** is the keyword used to inherit the properties of a class.

继承的关键词是extends，当一个子类需要获取他的父类的方法和属性时就需要使用继承来定义。

#### Encapsolution 封装

This is the practice of keeping fields within a class private, then providing access to them via public methods. It’s a protective barrier that keeps the data and code safe within the class itself.

Declare the variables of a class as **private**.Provide **public setter and getter methods** to modify and view the variables values.

封装就是通过使用private，public， protect关键词来保护内部数据的安全。

#### Polymorphism 多态

Polymorphism is the ability of an object to take on many forms. The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object.

多态是一个对象具有多种形式的能力。OOP中最常见的多态性用法是使用父类引用来引用子类对象。



### Inhertance继承 vs Interface接口

**Inhertance继承** 使用关键字 **`extends`**实现继承，一个类只可以继承一个父类。在继承中可以定义属性方法,变量,常量等。并在子类中重写复用父类方法，可以去掉多个子类间的功能类似的重复代码，保持代码的简洁性。但是回增加代码的耦合性。

**Interface接口**使用关键字 **`interface`** 修饰，使用关键字**`implements`**实现接口。一个类可以继承多个接口。接口中只能定义全局常量,和抽象方法，不能实例化，接口中不能有构造。子类任然需要实现自己的方法，但是可以降低代码的耦合性。

接口更像是一种规范，而不是具体方法的实现。接口可以约束继承统该接口的类的方法和参数，以供调用方统一调配。

因此我们应该面向接口编程，科学编程。
