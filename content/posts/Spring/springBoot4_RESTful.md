---
title: "SpringBoot 4: RESTful API"
date: 2021-12-23T11:43:43+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Spring
---

### 什么是RESTful 风格 API

API（Application Programming Interface），顾名思义：是一组编程接口规范，客户端与服务端通过请求响应进行数据通信。REST（Representational State Transfer）表述性状态传递，决定了接口的形式与规则。**RESTful是基于http方法的API设计风格，而不是一种新的技术.**

1. 看Url就知道要什么资源
2. 看http method就知道针对资源干什么
3. 看http status code就知道结果如何

### RESTful是面向资源的（名词）

REST 通过 URI 暴露资源时，会强调不要在 URI 中出现动词。比如：

| 不符合REST的接口URI      | 符合REST接口URI       | 功能           |
| :----------------------- | :-------------------- | :------------- |
| GET /api/getDogs/{id}    | GET /api/dogs/{id}    | 获取一个小狗狗 |
| GET /api/getDogs         | GET /api/dogs         | 获取所有小狗狗 |
| GET /api/addDogs         | POST /api/dogs        | 添加一个小狗狗 |
| GET /api/editDogs/{id}   | PUT /api/dogs/{id}    | 修改一个小狗狗 |
| GET /api/deleteDogs/{id} | DELETE /api/dogs/{id} | 删除一个小狗狗 |

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202112141953419.png)

### HTTP状态码

通过HTTP状态码体现动作的结果,不要自定义

```apl
200 OK 
400 Bad Request 
500 Internal Server Error
```

在 APP 与 API 的交互当中，其结果逃不出这三种状态：

- 所有事情都按预期正确执行完毕 - 成功
- APP 发生了一些错误 – 客户端错误（如：校验用户输入身份证，结果输入的是军官证，就是客户端输入错误）
- API 发生了一些错误 – 服务器端错误（各种编码bug或服务内部自己导致的异常）

这三种状态与上面的状态码是一一对应的。如果你觉得这三种状态，分类处理结果太宽泛，http-status code还有很多。建议还是要遵循KISS(Keep It Stupid and Simple)原则，上面的三种状态码完全可以覆盖99%以上的场景。

### 使用复数名词

/dogs 而不是 /dog

### 复杂资源关系的表达

GET /cars/711/drivers/ 返回 使用过编号711汽车的所有司机
GET /cars/711/drivers/4 返回 使用过编号711汽车的4号司机

### 高级用法:HATEOAS

**HATEOAS**:Hypermedia as the Engine of Application State 超媒体作为应用状态的引擎。
RESTful API最好做到HATEOAS，**即返回结果中提供链接，连向其他API方法，使得用户不查文档，也知道下一步应该做什么**。比如，当用户向api.example.com的根目录发出请求，会得到这样一个文档。

```
{"link": {
  "rel":   "collection https://www.example.com/zoos",
  "href":  "https://api.example.com/zoos",
  "title": "List of zoos",
  "type":  "application/vnd.yourformat+json"
}}
```

上面代码表示，文档中有一个link属性，用户读取这个属性就知道下一步该调用什么API或者可以调用什么API了。

### 资源**过滤、排序、选择和分页**的表述

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202112141956190.png)

###  版本化你的API

强制性增加API版本声明，不要发布无版本的API。如：/api/v1/blog

**面向扩展开放，面向修改关闭**：也就是说一个版本的接口开发完成测试上线之后，我们一般不会对接口进行修改，如果有新的需求就开发新的接口进行功能扩展。这样做的目的是：当你的新接口上线后，不会影响使用老接口的用户。如果新接口目的是替换老接口，也不要在v1版本原接口上修改，而是开发v2版本接口，并声明v1接口废弃！


本文出自：[springboot深入浅出系列](http://springboot.zimug.com/)