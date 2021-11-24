---
title: "Go Introduction"
date: 2021-11-24T17:04:49+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Go
---

Go语言aka Golang, 发布于2012年。是由3名Google员工：Robert Griesemer, Rob Pike, and Ken Thompson，设计开发的一门开源语言。

**Go 旨在解决我们在构建大型服务器软件时遇到的一系列软件工程问题。**

Go 是 Google 开发的一种编译的、并发的、垃圾收集的、静态类型的语言。

**Go语言特性：**

- 清除依赖
- 清晰的语法
- 清晰的语义
- 组合优于继承
- 编程模型提供的简单性（垃圾收集、并发）
- 简易工具（`go`工具, `gofmt`, `godoc`, `gofix`）

**Go vs C** 这些包括：

- 没有指针算法
- 没有隐式数字转换
- 总是检查数组边界
- 没有类型别名（在 之后`type X int`，`X`并且`int`是不同的类型而不是别名）
- `++`和`--`是陈述不表达
- 赋值不是表达式
- 获取堆栈变量的地址是合法的（甚至鼓励）
- 还有很多

**Go vs  Java **其中包括对以下方面的语言支持：

- 并发
- 垃圾收集
- 接口类型
- 反射
- 类型开关

### Hello World code in Go:

```bash
package main

import "fmt"

func main() {
  fmt.Println("Hello World")
}
```

运行程序：

```bash
$ go build main.go
$ ls
main  main.go
$ ./main
Hello World
```

### Go 命令：

```bash
// command line via a generic command:
$ go <command> [arguments]
// such as:
$ go doc fmt.println
```

```bash
// Running Files in Go
$ go run exampleFile.go
// Compile Go
$ go build test.go
// To run test, type in the command line:
$ ./test
```

### Go Value:

```go
// literal unnamed value
fmt.Println("PI = ", 3.14159)
 
// constant named value
const pi = 3.14159
 
// variable named value
var radius = 6
```

### Go Default Values

当一个变量variable没有被赋值时，这个变量会有一个默认值。

```go
Type    Zero Value
ints     0
floats   0
string   "" (empty string)
boolean  false
```

### Go Data Types

```go
string
bool
numeric types:
int8, uint8, int16, uint16, int32 , uint32, int64, uint64, int, uint, uintptr
float32, float64
complex64, complex128
```

### Go Variable

- use the  **`var`**  keyword followed by a name and its data type. This variable can be assigned later in the program. For example:

  ```go
  var fruit string
  string = "apple"
  ```

- use the   **`var`** keyword followed by a name, data type, **`=`** and value.

  ```go
  var fruit string = "apple"
  ```

- use the   **`var`**  keyword, followed by a name, **`=`** and value. Ignore the data type and let the compiler infer its type.

  ```go
  var fruit = "apple"
  ```

- skip the  **`var`** keyword, define a name followed by **`:=`** and value and let the compiler infer its type.

  ```go
  fruit := "apple"
  ```

### Go Errors

The error message is printed to the terminal and contains the following information:

- The filename
- The line that raises the error
- The number of characters from the left side that raises the error
- The type of error and reason for raising the error

For example:

```go
./Main.go:11:3: undefined: dinner
```

This particular error occurs in the file **main.go** at line **`11`**, **`3`** characters into the line, and its error type and reason is **`"undefined: dinner"`**.

### Go Fmt .Print() and .Println()

```go
fmt.Print("I", "am", "cool")
// Iamcool 没有空格 without any spacing
fmt.Println("I", "am", "cool")
// I am cool 
```

### Go Fmt .Printf() Function

- `%v` represents the named value in its default format;
- `%d` expects the named value to be an integer type;
- `%f` expects the named value to be a float type;
- `%T` represents the type for the named value.

```go
name := "Leslie"
fmt.Printf("My name is %v", name)
// My name is Leslie
 
age := 34
fmt.Printf("I am %d years old", age)
// I am 34 years old
 
fmt.Printf("%v is of type %T", name, name)
// Leslie is of type string
```

### Go Fmt .Scan() Function

```go
package main
import "fmt"
 
func main() {
  var name string
  var age int
  fmt.Println("What's your name and age?")
  fmt.Scan(&name, &age)
  fmt.Printf("You entered %v and %d.\n", name, age)
}
```

```bash
$ What's your name and age?
$ Marcia 32
$ You entered Marcia and 32.
```

### Go Short Variable Declaration

```go
if age := 55; age >= 55 {
  fmt.Println("You are retiring!")
}
switch season := "spring"; season {
  case "spring":
    fmt.Println("Plant some bulbs.")
  case "summer":
    ...
}
```

### Go Switch Statement

```go
day := "Tuesday"
switch day {
  case "Monday":
    fmt.Println("Monday is magnificent.")
  case "Tuesday":
    fmt.Println("Tuesday is terrific.")
  case "Wednesday":
    fmt.Println("Wednesday is wacky.")
  default:
    fmt.Println("We survived.")
}
```

### Go Random Number Generator

```go
number := math.rand.Intn(100)
```

### Go Pointer Dereferencing

```go
var pointerToInt *int 
// a pointer to a variable of type int

y := 3
var x *int = &y // pointer variable x assigned the address of variable y
*x = 5 // dereference x by typing *x
fmt.Println(y) // y is now 5
```



