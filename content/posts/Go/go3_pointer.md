---
title: "Go 3: Pointer"
date: 2021-10-22T17:59:37+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Go
---

### Go is a pass-by-value language.

- **addresses** 

   * An address is where a value is stored, To find an address of a variable, use the `&` operator before a variable.

  ```go
  x := "My very first address"
  fmt.Println(&x) // Prints address 0x414020
  ```

- **pointers**

  - A pointer is specific to what type of address it can store.
  - The `*` operator can be used to assign a pointer the type of the value its address holds.

  ```go
  var pointerForInt *int
  ```

- **dereferencing**

  - The `*` operator can also be used to dereference a pointer and assign a new value.

  ```go
  lyrics := "Moments so dear" 
  pointerForStr := &lyrics
   
  *pointerForStr = "Journeys to plan" 
   
  fmt.Println(lyrics) // Prints: Journeys to plan
  ```

```go
func addHundred1(num int) {
  num += 100
}

func addHundred12 (numPtr *int) {
  *numPtr += 100
}
 
func main() {
  x := 1
  addHundred1(x)
  fmt.Println(x) // Prints 1
  
  addHundred2(&x) //&x
  fmt.Println(x) // Prints 101
}
```

