## 基础语法

### 变量的定义

```go
package main

import "fmt"

// 包内变量
var w = 1
var (
	r = 2
	t = 3
)

func variableZeroValue() {
	// go生命的变量但是没赋值的时候有一个默认的zeroValue
	var a int
	var s string
	// %d 整型 %q 单引号
	fmt.Printf("%d %q\n", a, s)
}
func variableInitialValue() {
	var a, b int = 3, 4
	var s string = "abc"
	fmt.Println(a, b, s)
}

func variableTypeDeduction() {
	// 隐式推断
	var a, c = 1, "qqq"
	fmt.Println(a, c)
}

func variableShorter() {
	a, c := 3, 4
	c = 5
	fmt.Println(a, c)
}

func main() {
	fmt.Printf("h11eelo")
	variableZeroValue()
	variableInitialValue()
	variableTypeDeduction()
	variableShorter()
	fmt.Println(w, r, t)
}

```

### 变量类型

```go
bool, string
(u)init,(u)init8,(u)init16,(u)init32,(u)init64,uintptr(指针长度) 
byte, rune(字符)
float32,float64,complex64,complex128
```

### 常量

```go
// 常量
func consts() {
   const filename = "abc.txt"
   const a, b = 3, 4
   var c int
   c = int(math.Sqrt(a * a + b * b))
   fmt.Println(filename, c)
}
```

### 枚举

```go

func enums() {
   //const (
   //  cpp = 0
   //  java = 1
   //  golang = 2
   //)
   const (
      cpp = iota
      java
      golang
   )

   const (
      b = 1 << (10 * iota)
      kb
      mb
      gb
      tb
      pb
   )

   fmt.Println(cpp, java, golang)
   fmt.Println(b, kb, mb, gb, tb , pb)
}
```

