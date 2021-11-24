---
title: "Java Architecture: JVM, JRE & JDK"
date: 2021-10-11T17:11:25+08:00
draft: true
images:
  - "/images/totoro.jpeg"
Tags:
  - Java
---

Java之所以能过成为当今最流行的编程语言之一, 离不开**Java Virtual Machine (JVM), Java Runtime Environment (JRE) and Java Development Kit (JDK) **的支持。

![JVM - Java Architecture - Edureka](https://www.edureka.co/blog/wp-content/uploads/2019/07/q.png)

![img](https://www.oracle.com/ocom/groups/public/@otn/documents/digitalasset/2167990.jpg)

---

### **[Java Virtual Machine](https://www.oracle.com/java/technologies/javase/javase-core-technologies-apis.html)** JVM

Java virtual machine is a platform-independent abstract machine that provides a runtime environment in which loads, verifies and executes Java bytecode. WORA (Write once Run Anywhere).

Java虚拟机是一个独立于平台的抽象机器，它提供了一个运行环境，在其中加载、验证和执行Java字节代码。它被称为解释器或 Java 编程语言的核心，因为它执行 Java 编程。引入Java语言虚拟机后，Java语言在不同平台上运行时不需要重新编译. 

#### Java Virtual Machine Architecture

Java Virtual Machine Architecture 虚拟机架构非常简单，它有一个内存区memory area、一个类加载器class loader 和一个执行引擎Execution Engine 以及其他组件。

![JVM First Bounce--Class Loading Subsystem](https://www.fatalerrors.org/images/blog/a2b8bfe83deb28ffd841280abede11d9.jpg)

![img](http://2.bp.blogspot.com/-ILs_L_UHzNM/U4mBNvpfB8I/AAAAAAAAAeU/EdBcJ36qfAI/s1600/JVM+Architecture+block+diagram.png)

##### ClassLoader 类加载器

It is a subsystem that is used to load class files. Whenever we run a program in java, it is first loaded by the ClassLoader. the major function includes initialization, linking and loading.  

##### JVM Memory 内存区

1. Method Area – It stores the structures for each class like the code, field data, runtime constant pool, method data, etc.  all **static variables, ** are created in this area.

   方法区 - 它存储每个类的结构，如代码、字段数据、运行时常量池、方法数据等。所有静态变量都在此运行区中创建。

2. Heap Area – Objects are allocated at the runtime in the heap. It is the main memory of JVM. All *objects* of classes – *non-static variables memory* are created in this runtime area. It may increase or decrease in size while the application runs.

   堆区 - 它是JVM的主存。类的所有*对象*-*非静态变量内存*都在此运行时区域中创建. 它是JVM的主存。类的所有*对象*-*非静态变量内存*都在此运行时区域中创建

3. Stacks Area – It stores local variables and results. In this runtime area all Java methods are executed.

   In this runtime JVM by default creates two threads, they are Main thread. Garbage collector thread.

- - - *Main thread* is responsible to execute Java methods stats with main method, also responsible to create objects in heap area if it finds “new” keyword in any method logic.
    - *Garbage collector thread* is responsible to destroy all unused objects from heap area.

Java 栈 - 所有的本地变量和运行结果都存储在这里并执行所有 Java 方法。在这个运行时 JVM 默认创建两个线程，主线程 和垃圾收集器线程。

- *主线程*负责用main方法执行Java方法stats，如果在任何方法逻辑中发现“new”关键字，也负责在堆区域创建对象。
- *垃圾收集器线程*负责销毁堆区域中所有未使用的对象。

4. PC Registers – It has the address or location of the JVMinstruction that is being executed. a separate program counter register is created for every thread for tracking that thread execution by storing its instruction address.

   程序计数器 - 它有正在执行的JVM指令的地址或位置，为每个线程创建一个单独的程序计数器寄存器，用于通过存储其指令地址来跟踪该线程的执行。

5. Native Method Stacks – All the native methods used in the applications are present in the native method stacks.

   本地方法栈 - 应用程序中使用的所有本地方法都存在于本地方法栈中。

##### Execution Engine 

 **–** An execution engine contains a Grabage collector, an interpreter and a [JIT](https://www.edureka.co/blog/just-in-time-compiler/) compiler.

**–** 一个执行引擎包含一个垃圾回收器Grabage collector、一个解释器interpreter 和一个JIT编译器。

##### Native Method [Interface](https://www.edureka.co/blog/java-interface/)

– It is a [framework](https://www.edureka.co/blog/java-frameworks/) that provides. 提供框架。

##### Native Method Library – 本地方法库

---

### **[Java Runtime Environment (JRE)](https://docs.oracle.com/javase/8/docs/technotes/guides/index.html#jre-jdk)**

The Java Runtime Environment (JRE) provides the libraries, the Java Virtual Machine, and other components to run applets and applications written in the Java programming language. In addition, two key deployment technologies are part of the JRE: [Java Plug-in](https://www.oracle.com/java/technologies/plugin.html), which enables applets to run in popular browsers; and Java Web Start, which deploys standalone applications over a network. It is also the foundation for the technologies in the Java 2 Platform, Enterprise Edition (J2EE) for enterprise software development and deployment. The JRE does not contain tools and utilities such as compilers or debuggers for developing applets and applications.

Java 运行时环境 (JRE) 提供库、Java 虚拟机和其他组件来运行用 Java 编程语言编写的小程序和应用程序。此外，JRE 还包含两项关键部署技术：[Java Plug-in](https://www.oracle.com/java/technologies/plugin.html)，它使小应用程序能够在流行的浏览器中运行；和 Java Web Start，它通过网络部署独立的应用程序。它也是 Java 2 Platform, Enterprise Edition (J2EE) 中用于企业软件开发和部署的技术的基础。JRE 不包含用于开发小程序和应用程序的工具和实用程序，例如编译器或调试器。

---

### **[Java Development Kit (JDK)](https://docs.oracle.com/javase/8/docs/technotes/guides/index.html#jre-jdk)**

The JDK is a superset of the JRE, and contains everything that is in the JRE, plus tools such as the compilers and debuggers necessary for developing applets and applications.

JDK 是 JRE 的超集，包含 JRE 中的所有内容，以及开发小程序和应用程序所需的编译器和调试器等工具。

### **Difference Between JDK, JRE, And JVM**

1. JDK is the development platform, while JRE is for execution. JDK 开发工具包，JRE 运行环境。

2. JVM is the foundation, or the heart of Java programming language, and ensures the program’s Java source code will be platform-agnostic. JVM是java基础和核心，它确保了Java可以在任何平台运行。

3. JVM is included in both JDK and JRE – Java programs won’t run without it.  **jdk & jre都包含jvm.**

   ![What is JDK, JRE and JVM?](https://s3.shunyafoundation.com/s3/1578452c3f66d8fd0d04d5d195328ae1359d8caa/jdk-jvm.png)

---

### 互补技术

有许多互补技术可用于增强 JVM、JRE 或 JDK。以下技术是最常用的技术：

- **Just-in-time Compiler (JIT)** 即时编译器 是 JVM 的一部分，用于优化字节码到机器码的转换。它选择相似的字节码同时编译，减少字节码到机器码编译的整体持续时间。
- **Javac**是另一个补充工具，它是一个编译器，可以读取 Java 定义并将其转换为可以在 JVM 上运行的字节码。
- **Javadoc**将 API 文档从 Java 源代码转换为 HTML。这在以 HTML 格式创建标准文档时很有用。

---

### Java SE, Java EE, Java ME & JavaFx

There are four platforms of the Java programming language:

- Java Platform, Standard Edition (Java SE)
- Java Platform, Enterprise Edition (Java EE)
- Java Platform, Micro Edition (Java ME)
- JavaFX 

所有 Java 平台都由 Java 虚拟机 (VM) 和应用程序编程接口 (API) 组成。Java 虚拟机是一个用于特定硬件和软件平台的程序，它运行 Java 技术应用程序。API 是一组软件组件，可用于创建其他软件组件或应用程序。每个 Java 平台都提供了一个虚拟机和一个 API，这使得为该平台编写的应用程序可以在具有 Java 编程语言所有优点的任何兼容系统上运行：平台独立性、功能强大、稳定性、易于开发和安全。

##### Java SE
当大多数人想到 Java 编程语言时，他们会想到 Java SE API。Java SE 的 API 提供了 Java 编程语言的核心功能。它定义了从 Java 编程语言的基本类型和对象到用于网络、安全、数据库访问、图形用户界面 (GUI) 开发和 XML 解析的高级类的所有内容。

除了核心 API 之外，Java SE 平台还包括虚拟机、开发工具、部署技术以及 Java 技术应用程序中常用的其他类库和工具包。

##### Java EE
Java EE 平台构建在 Java SE 平台之上。Java EE 平台为开发和运行大规模、多层、可扩展、可靠和安全的网络应用程序提供了 API 和运行时环境。

##### Java ME
Java ME 平台提供了一个 API 和一个小型虚拟机，用于在手机等小型设备上运行 Java 编程语言应用程序。该 API 是 Java SE API 的一个子集，以及对小型设备应用程序开发有用的特殊类库。Java ME 应用程序通常是 Java EE 平台服务的客户端。

##### JavaFX
JavaFX 是一个使用轻量级用户界面 API 创建富 Internet 应用程序的平台。JavaFX 应用程序使用硬件加速的图形和媒体引擎来利用更高性能的客户端和现代外观以及用于连接到网络数据源的高级 API。JavaFX 应用程序可能是 Java EE 平台服务的客户端。

![Oracle Java Strategy Lg V3](https://image.slidesharecdn.com/javastrategylgv3-100319054817-phpapp02/95/oracle-java-strategy-lg-v3-7-728.jpg?cb=1353400249)

---

### How is Java platform indeeddent?

![JIT workflow in Java - Java Architecture- Edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2019/06/Jit-Compiler.png)

***sample.java → javac (sample. class) → JVM(sample.obj) → final output***

First source code is used by java compiler and is converted in .class file. The class file code is in byte code form and that class file is used by JVM to convert into an object file. After that, you can see the final output on your screen. Java 编译器使用第一个源代码并转换为 .class 文件。类文件代码采用字节码形式，JVM 使用该类文件转换为目标文件。之后，您可以在屏幕上看到最终输出。

![Java Just-In-Time (JIT) Compiler: What is it, how does it work, where does  it fit into JVM architecture (JIT vs Interpreter)? |](http://upload.wikimedia.org/wikipedia/commons/3/3a/Java_virtual_machine_architecture.svg)



