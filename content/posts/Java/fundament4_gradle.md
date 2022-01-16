---
title: "Java Fundament 4:  Build Automation Tools：Ant, Gradle & Maven"
date: 2021-10-04T16:38:00+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Java Fundament
---

在进入*ANT*、*Maven*或*Gradle 之前*，我们必须首先了解与它们相关的一些事情。

**依赖:**一般来说，依赖是指某件事需要另一件事来自己执行。简单地说，如果 'A' 需要 'B' 才能成功执行，则 'A' 依赖于 'B'。在软件世界中，依赖项是您的应用程序成功执行所需的任何东西。它基本上是应用程序所需的任何外部支持库。例如zuul、hystrix、lombok、jdbc等。

最初，我们曾经通过以下方式管理依赖项：

- 从互联网上手动下载所需库的jar文件并将其添加到我们的项目中。
- 编写一个脚本，该脚本将通过网络从外部源自动下载库。

使用这些工具之前面临的问题：

- 通过从 Internet 上手动下载来添加依赖项是一项非常累人的任务。
- 如果外部源的 URL 通过 Internet 更改，我们的脚本可能会失败。
- 在我们的应用程序中识别和管理传递依赖是非常困难的。

**Depende Management Tools依赖管理工具:**它解决和管理应用程序所需的依赖关系。

**什么是构建工具？**

> 构建工具是从源代码自动创建可执行应用程序的程序（例如，`.apk`对于 Android 应用程序）。构建包括将代码编译、链接和打包成可用或可执行的形式。
>
> 基本上，构建自动化是编写脚本或自动化软件开发人员在日常活动中执行的各种任务的行为，例如：
>
> 1. 下载并管理依赖项。
> 2. 将源代码编译成二进制代码。
> 3. 打包那个二进制代码。
> 4. 运行测试。
> 5. 部署到生产系统。

**我们为什么要使用构建工具或构建自动化？**

> 在小型项目中，开发人员通常会手动调用构建过程。这对于大型项目来说是不切实际的，因为很难跟踪需要构建的内容、构建过程中的顺序和依赖关系。使用自动化工具可以使构建过程更加一致。

**各种可用的构建工具 ：**

> 1.  Java - Ant、Maven、Gradle。
> 2. .NET 框架 - NAnt
> 3. c# - MsBuild。

### **Apache Ant**

Ant是 Apache Tomcat 代码库的一部分，并于 2000 年作为独立项目发布. Ant 的主要好处是它的灵活性。Ant 不会对开发人员强加任何编码约定或项目结构。因此，这意味着 Ant 需要开发人员自己编写所有命令，这有时会导致构建文件很大并且难以维护。最初，Ant 没有对依赖项管理的内置支持。后来它采用了Apache Ivy，作为Apache Ant项目的一个子项目开发，用于依赖管理。**过时的构建工具。**

### **Apache Maven**

[Apache Maven](https://maven.apache.org/)是一个依赖管理和构建自动化工具，于 2004 年发布。它继续使用*XML，*但通过遵循“*约定优于配置*”的原则克服了缺点。它依赖于约定并提供预定义的命令（目标）。它的配置文件，包含构建和依赖管理指令，按照惯例称为“ *pom.xml* ”，存在于项目的根文件夹中。**Ant 升级版**。

![img](https://miro.medium.com/max/1324/1*p9j7JsTDxRLdsdks4ADlaQ.jpeg)

Maven 引擎将*pom.xml*和项目作为输入。它读取*pom.xml*文件并将其中提到的依赖项作为 jar 文件下载到本地存储库中。然后，它执行生命周期、构建阶段和插件。最后，生成一个打包和测试的工件。

**pom.xml 示例：**

```java
<?xml version="1.0" encoding="UTF-8"?> 
<project xmlns=" http://maven.apache.org/POM/4.0.0 " 
xmlns:xsi=" http://www.w3 .org/2001/XMLSchema-instance "   
xsi:schemaLocation=" http://maven.apache.org/POM/4.0.0  
 https://maven.apache.org/xsd/maven-4.0.0.xsd "> 
       <modelVersion>4.0.0</modelVersion> 
       <parent>    
               <groupId>org.springframework.boot</groupId> 
               <artifactId>spring-boot-starter-parent</artifactId> 
               <version>2.2.5.RELEASE</version >   
               <relativePath/> 
       </parent>
       <groupId>com.example</groupId>  
       <artifactId>demo</artifactId>   
       <version>0.0.1-SNAPSHOT</version>   
       <name>demo</name>   
       <description>Spring Boot 的演示项目</description>    
       <properties>   
                  <java.version>1.8< /java.version> 
       </properties>    
       <dependencies> 
                    <dependency>    
                               <groupId>org.projectlombok</groupId> 
                               <artifactId>lombok</artifactId>    
                               <optional>true</optional> 
                    </dependency> 
       </dependencies>   
</项目>
```

pom.xml 文件中的一些重要标签：

- **groupId:**代表项目所属的组织。
- **artifactId:**它是项目的名称。
- **version:**它代表项目的版本。
- **包装:**它代表了项目构建的最终形式。

**在maven中添加依赖：**

```java
<dependency> 
    <groupId>org.projectlombok</groupId> 
    <artifactId>lombok</artifactId> 
    <version>1.18.10</version> 
</dependency>
```

Maven 规定了严格的项目结构，而 Ant 也提供了灵活性。严格的约定伴随着比 Ant 灵活得多的代价——目标定制非常困难。

**maven的缺点：**

1. 依赖管理不能很好地处理同一个库的不同版本之间的冲突。
2. 目标的定制很难。

### **Gradle**

Grade 是一个开源的依赖管理和构建自动化工具，于 2012 年发布。它结合了 Apache Ant 和 Apache Maven 的优点，并在它们之上构建，并使用域特定语言（基于 Groovy）而不是 XML。它采用了 Ant 的灵活性和 Maven 的生命周期。它还遵循“*约定优于配置*”的原则。它支持用于检索依赖项的 Maven 和 Ivy 存储库。它的配置文件通常称为“ *build.gradle* ”，位于项目的根文件夹中。Gradle 将其构建步骤命名为“任务”，而不是 Ant 的“目标”或 Maven 的“阶段”。Google 采用 Gradle 作为 Android 操作系统的默认构建工具。

Gradle 不使用 XML。相反，它有它自己**d** omain**小号**pecific**大号**基于Groovy的（JVM语言之一）anguage。因此，与为 Ant 或 Maven 编写的脚本相比，Gradle 构建脚本往往更短、更清晰。Gradle 的样板代码量要小得多。

**Gradle 配置**

- **实现:**它用于声明我们不想暴露给消费者编译时的依赖项。
- **api:**它用于声明作为我们 API 一部分的*依赖项，即我们明确希望向消费者公开的依赖项。*
- **compileOnly:**它 允许我们声明只应在编译时可用但在运行时不需要的依赖项。此配置的一个示例用例是像[Lombok](https://projectlombok.org/)这样的注释处理器，它在编译时修改字节码。编译后不再需要它，因此该依赖项在运行时不可用。
- **runtimeOnly:**它允许我们声明在编译时不需要但在运行时可用的依赖项。一个例子是[SLF4J](https://www.slf4j.org/)，我们`slf4j-api`将其包含到`implementation`配置中，并将该 API（如`slf4j-log4j12`或`logback-classic`）的实现包含在`runtimeOnly`配置中。
- **testImplementation:**类似于`implementation`，但声明的依赖项`testImplementation`仅在测试的编译和运行时可用。我们可以使用它来声明对测试框架（如[JUnit](https://junit.org/junit5/)或[Mockito）的](https://site.mockito.org/)依赖[项](https://site.mockito.org/)，我们只在测试中需要，而在生产代码中不应该提供这些依赖项。
- **testCompileOnly:**类似于`compileOnly`，但声明的依赖项`testCompileOnly`仅在测试编译期间可用，在运行时不可用。
- **testRuntimeOnly:**与 类似`runtimeOnly`，但声明为 的依赖项`testRuntimeOnly`仅在测试运行时可用，而在编译时不可用。

**Gradle 中的项目和任务**

每个 Gradle 构建都包含一个或多个项目。每个项目由一组任务组成。每个任务代表构建执行的单个工作，例如生成 JavaDoc，将一些档案发布到存储库等。

**build.gradle 示例**

```java
plugins {
 id 'org.springframework.boot' version '2.2.5.RELEASE'
 id 'io.spring.dependency-management' version '1.0.9.RELEASE'
 id 'java'
}
group = 'com.example'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '1.8'
repositories {
 mavenCentral()
}
dependencies {
 implementation 'org.springframework.boot:spring-boot-starter'
 }
}
```

示例：在我们的项目中添加中央 Maven 存储库，将以下代码片段添加到我们的**build.gradle**文件中：

```java
repositories {
    mavenCentral()
}
```

**在 Gradle 中添加依赖项：**

```java
compile group: 'org.hibernate', name: 'hibernate-core', version: '3.6.7.Final'
```

**好处：**

1. 它可以很好地处理传递依赖。如果项目中存在冲突的传递依赖项，那么为了解决它，它选择依赖项的最新版本。例如，依赖“A”在内部需要依赖“C”和版本 2.0，依赖“B”在内部需要依赖“C”和版本 3.0。然后 Gradle 将使用最新版本的依赖项“C”。
2. Gradle 的配置文件更小，更干净，因为它使用领域特定语言，基于 Groovy 而不是 XML。
3. 摇篮采用增量构建理念和跟踪任务的输入和输出，并只在运行什么是必要的，只有处理避免了工作，改变在可能的情况，因此尔斯，执行比Maven的更快。

