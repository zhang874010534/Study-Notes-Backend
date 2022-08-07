## 变量的定义

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

