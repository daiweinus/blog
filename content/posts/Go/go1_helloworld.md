---
title: "Go 1: Helloworld"
date: 2021-10-20T17:54:17+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Go
---

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

### Multiple Return Values

```go
package main
import "fmt"

func GPA(midtermGrade float32, finalGrade float32) (string, float32) {
  averageGrade := (midtermGrade + finalGrade) / 2
  var gradeLetter string
  if averageGrade > 90 {
    gradeLetter = "A"
  } else if averageGrade > 80 {
    gradeLetter = "B"
  } else if averageGrade > 70 {
    gradeLetter = "C"
  } else {
    gradeLetter = "F"
  }
 
  return gradeLetter, averageGrade 
}

func main() {
  var myMidterm, myFinal float32
  myMidterm = 89.4
  myFinal = 74.9
  var myAverage float32
  var myGrade string
  myGrade, myAverage = GPA(myMidterm, myFinal)
  fmt.Println(myAverage, myGrade) // Prints 82.12 B
}
```

### defer 关键字，告诉程序在function结尾执行defer call的程序

```go
package main
import "fmt"

func queryDatabase(query string) string {
  var result string
  connectDatabase()
  // defer keyword tells Go to run a function at the end of the current function.
  defer disconnectDatabase()
  
  if query == "SELECT * FROM coolTable;" {
    result = "NAME|DOB\nVincent Van Gogh|March 30, 1853"
  }  
  fmt.Println(result)
  return result
}

func connectDatabase() {
  fmt.Println("Connecting to the database.")
}

func disconnectDatabase() {
  fmt.Println("Disconnecting from the database.")
}

func main() {
  queryDatabase("SELECT * FROM coolTable;")
}
```

```bash
Connecting to the database.
NAME|DOB
Vincent Van Gogh|March 30, 1853
Disconnecting from the database.
```
