---
title: "Spring_intro"
date: 2021-12-01T16:57:23+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Spring
---

### 什么是框架 **framework**？

具有一定约束性和支撑性的半成品项目。框架+业务逻辑 = 一个完整的项目。

MVC 模式代表 Model-View-Controller（模型-视图-控制器） 模式。这种模式用于应用程序的分层开发。

> Model 负责存储系统的中心数据;
>
> View 负责存储系统的中心数据;
>
> Controller 处理用户输入的信息。负责从视图读取数据，控制用户输入，并向模型发送数据，是应用程序中处理用户交互的部分。负责管理与用户交互交互控制。

表示层框架：struts1，struts2，springMVC

业务层框架，设计型框架：spring

持久层框架：hibernate(全自动), mybatis(半自动) 

建议优先学习 Springboot 。

### Spring Boot

1. Spring Boot 简介

   >简化Spring应用开发的框架。
   >
   >整个Spring技术栈的大整合。
   >
   >J2EE开发的一站式解决方案。

2. 微服务

   2014， Martin Fowler

   微服务：架构风格（服务微化）

   一个应用应该是一组小型服务，可以通过http方式互通；

   每一个功能元素最终都是一个可独立替换可升级的软件单元；

    [microservices guide](https://martinfowler.com/microservices/)

3. Spring Boot主要特性

   - 遵循“约定优于配置”的原则，简化配置
   - 可以完全脱离XML配置文件,采用注解配置和java Config
   - 内嵌Servlet容器，应用可用jar包执行：java -jar
   - 快速完成项目搭建、整合第三方类库，方便易用
   - 提供了starter POM, 能够非常方便的进行包管理, 简化包管理配置
   - 与Spring cloud天然集成，spring boot是目前java体系内实现微服务最佳方案

4. Spring Boot集成第三方类库的步骤

   1. 通过maven引入springboot-XXXX-starter
   2. 修改ymal或properties全局统一配置文件
   3. 加入一个Java Config。这个属于个性化配置，如果使用通用配置，这一步不需要。

