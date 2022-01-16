---
title: "SpringBoot 5: Lombok"
date: 2021-12-24T11:43:43+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Spring

---

Lombok 是一款用来通过注解自动生成辅助代码的插件，通过注释可自动生成Getter, Setter, AllArgsConstructor....

![](https://cdn.jsdelivr.net/gh/daiweinus/blog_pictures/202112081144164.png)

```java
package com.example.bootlunch.model;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;
import lombok.extern.slf4j.Slf4j;

@Data // generate set, get method
@Slf4j // generate project logger
@Builder // create object
@AllArgsConstructor // generate all args constructor
@NoArgsConstructor // generate no args constructor
public class LombokPOJO {

    private String name;

    private Integer age;
}
```

complied bytecode 编译后的字节码

```java
//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//

package com.example.bootlunch.model;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class LombokPOJO {
  // generate project logger
    private static final Logger log = LoggerFactory.getLogger(LombokPOJO.class);
    private String name;
    private Integer age;

  // create object
    public static com.example.bootlunch.model.LombokPOJO.LombokPOJOBuilder builder() {
        return new com.example.bootlunch.model.LombokPOJO.LombokPOJOBuilder();
    }

  // generate set, get method
    public String getName() {
        return this.name;
    }

    public Integer getAge() {
        return this.age;
    }

    public void setName(final String name) {
        this.name = name;
    }

    public void setAge(final Integer age) {
        this.age = age;
    }

    public boolean equals(final Object o) {
        if (o == this) {
            return true;
        } else if (!(o instanceof LombokPOJO)) {
            return false;
        } else {
            LombokPOJO other = (LombokPOJO)o;
            if (!other.canEqual(this)) {
                return false;
            } else {
                Object this$age = this.getAge();
                Object other$age = other.getAge();
                if (this$age == null) {
                    if (other$age != null) {
                        return false;
                    }
                } else if (!this$age.equals(other$age)) {
                    return false;
                }

                Object this$name = this.getName();
                Object other$name = other.getName();
                if (this$name == null) {
                    if (other$name != null) {
                        return false;
                    }
                } else if (!this$name.equals(other$name)) {
                    return false;
                }

                return true;
            }
        }
    }

    protected boolean canEqual(final Object other) {
        return other instanceof LombokPOJO;
    }

    public int hashCode() {
        int PRIME = true;
        int result = 1;
        Object $age = this.getAge();
        int result = result * 59 + ($age == null ? 43 : $age.hashCode());
        Object $name = this.getName();
        result = result * 59 + ($name == null ? 43 : $name.hashCode());
        return result;
    }

    public String toString() {
        String var10000 = this.getName();
        return "LombokPOJO(name=" + var10000 + ", age=" + this.getAge() + ")";
    }

  // generate all args constructor
    public LombokPOJO(final String name, final Integer age) {
        this.name = name;
        this.age = age;
    }

  // generate no args constructor
    public LombokPOJO() {
    }
}
```

使用Lombok可以提升开发效率，节省编写固定模式代码时间，同时使源代码更加简洁可读。

