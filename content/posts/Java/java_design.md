---
title: "Java Design Principles"
date: 2021-11-09T12:11:11+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - java
---

### Design Principles

1. **SOILD**

   1. Single Responsibility Principle (SRP) 单一职责原则

      Each class should have a single purpose.

   2. Open/Closed Principle (OCP) 开闭原则 

      software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. 

   3. Liscov Substitution Principle (LSP) 替换原则 

      functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.

   4. Interface Segregation Principle (ISP) 接口隔离原则 

      Clients should not be forced to depend upon interfaces that they don’t use. the number of members in the interface that is visible to the dependent class should be minimized.接口中对依赖类可见的成员数量应该最小化。

   5. Dependency Inversion Principle (DIP) 依赖倒置原则 

      High level modules should not depend upon low level modules. Both should depend upon abstractions.Abstractions should not depend upon details. Details should depend upon abstractions.

2. **DRY** (Don’t Repeat Yourself)

3. **KISS** (Keep it simple, Stupid!)

4. **YAGNI (You ain't gonna need it)**This principle states that always implement things when you actually need them never implement things before you need them.

### Design Pattern

In software engineering, a software design pattern is a general, reusable solution to a commonly occurring problem within a given context in software design. It is a description or template for how to solve a problem that can be used in many different situations.

* **Abstract Factory**Provide an interface for creating families of related or dependent objects without specifying their concrete classes.

* **Adapter**Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn’t otherwise because of incompatibility interfaces.

* **Command**Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.**Factory Method**Define an interface for creating an object, but let the subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

* **Observer**Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

* **Visitor**Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.

