---
title: "SpringBoot Hello world"
date: 2021-12-07T16:17:23+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Spring Boot

---

1. 使用Spring Initializr 新建spring boot project

   ![springboot_helloworld1.png](https://github.com/daiweinus/blog_pictures/blob/master/springboot_helloworld1.png?raw=true)

2. 在application.properties文件新建服务器端口

   ![springboot_helloworld2.png](https://github.com/daiweinus/blog_pictures/blob/master/springboot_helloworld2.png?raw=true)

3. 新建HelloController class

   ![Screenshot 2021-12-07 at 18.44.45.png](https://github.com/daiweinus/blog_pictures/blob/master/Screenshot%202021-12-07%20at%2018.44.45.png?raw=true)

4. 执行BootLunchApplication main class

   ![Screenshot 2021-12-07 at 18.47.32.png](https://github.com/daiweinus/blog_pictures/blob/master/Screenshot%202021-12-07%20at%2018.47.32.png?raw=true)

   ![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202112071909939.png)

   ![Screenshot 2021-12-07 at 18.47.49.png](https://github.com/daiweinus/blog_pictures/blob/master/Screenshot%202021-12-07%20at%2018.47.49.png?raw=true)

```java
@SpringBootApplication
@RestController
public class DemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}

	@GetMapping
	public String hello() {
		return "Hello World";
	}

}
```

