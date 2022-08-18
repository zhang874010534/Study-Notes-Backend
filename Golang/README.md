## 基础语法

### fmt.Printf()

占位符：

[一般]

%v 相应值的默认格式。在打印结构体时，“加号”标记（%+v）会添加字段名

%#v 相应值的 Go 语法表示

%T 相应值的类型的 Go 语法表示

%% 字面上的百分号，并非值的占位符

[布尔]

%t 单词 true 或 false。

[整数]

%b 二进制表示

%c 相应 Unicode 码点所表示的字符

%d 十进制表示

%o 八进制表示

%q 单引号围绕的字符字面值，由 Go 语法安全地转义

%x 十六进制表示，字母形式为小写 a-f

%X 十六进制表示，字母形式为大写 A-F

%U Unicode 格式：U+1234，等同于 “U+%04X”

[浮点数及其复合构成]

%b 无小数部分的，指数为二的幂的科学计数法，与 strconv.FormatFloat 的 ‘b’ 转换格式一致。例如 -123456p-78

%e 科学计数法，例如 -1234.456e+78

%E 科学计数法，例如 -1234.456E+78

%f 有小数点而无指数，例如 123.456

%g 根据情况选择 %e 或 %f 以产生更紧凑的（无末尾的 0）输出

%G 根据情况选择 %E 或 %f 以产生更紧凑的（无末尾的 0）输出

[字符串与字节切片]

%s 字符串或切片的无解译字节

%q 双引号围绕的字符串，由 Go 语法安全地转义

%x 十六进制，小写字母，每字节两个字符

%X 十六进制，大写字母，每字节两个字符

[指针]

%p 十六进制表示，前缀 0x

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

### 条件语句

```go
func main() {
   //file, err := os.ReadFile("abc.txt")
   //if err != nil {
   // fmt.Println(err)
   //} else {
   // fmt.Printf("%s\n", file)
   //}
   if file, err := os.ReadFile("abc.txt"); err != nil {
      fmt.Println(err)
   } else {
      fmt.Printf("%s\n", file)
   }
}
```

### 循环语句

```go
func grade(score int) string {
   g := ""
   switch {
   case score < 60:
      g = "F"
   case score < 70:
      g = "C"
   default:
      panic(fmt.Sprintf("wrong %d", score))
   }
   return g
} 

// 读取文件 一行一行输出 
func printFile(filename string) {
	open, err := os.Open(filename)
	if err != nil {
		return
	}
	scanner := bufio.NewScanner(open)
	for scanner.Scan() {
		fmt.Println(scanner.Text())
	}
}
```

### 函数

```go
// 普通函数
func sum(a int, b int) (sum int, err error) {
	return a + b, fmt.Errorf("error %d", a)
}
// 某一项不需要可以用_
q, _ := sum(1, 2)

i, err := sum(1, 2)
if err != nil {
    return
}

// 接收多个参数 可变参数列表
func sum2(numbers ...int) int {
	fmt.Println(numbers)
	s := 0
    // 当while来使用
	for i := range numbers {
		s += numbers[i]
	}
	return s
}
sum2(1,2,3,4)
```

### 指针

> Go语言只有一种值传递的方式

```go
func swap(a, b *int) {
   *b, *a = *a, *b
}
a, b := 3, 4
swap(&a, &b) // 4 3
```

## 内建容器

### 数组

```go
func main() {
   var arr1 [5]int
   arr2 := [3]int{1, 2, 3}
   arr3 := [...]int{2, 4, 6,0}
   var grid [4][5]int
   fmt.Println(arr1, arr2, arr3, grid)
   for i, v := range arr3 {
      fmt.Println(i, v)
   }
}


// 会进行拷贝 所以原始的值不会被修改
func printArray(arr [3]int) {
	arr[0] = 100
	for i, v := range arr {
		fmt.Println(i, v)
	}
}

func main() {
	arr1 := [3]int{1, 2, 3}
	printArray(arr1)
    // 0 100
    // 1 2
    // 2 3
	fmt.Println(arr1) // [1, 2, 3]
}
```

### 切片

> slice本身是没有数据的，是对底层array的一个view

```go
func printArray(arr []int) {
	arr[0] = 100
	for i, v := range arr {
		fmt.Println(i, v)
	}
}

func main() {
	arr1 := []int{1, 2, 3}
    printArray(arr1[:])
    // 0 100
    // 1 2
    // 2 3
	fmt.Println(arr1) // [100, 2, 3]
}
```

```go
arr := [...]int{0, 1, 2, 3}
s1 := arr[0:2] // [0 1]
s2 := s1[1:3]  // [1 2] s[i]不可以超越len[s]  可以向后扩展,不可以超越底层数组cap[s] 即使s1中不存在2 也是能拿到的 但是直接s1[2]是拿不到的
fmt.Println(s1, s2)

```

```go
make 创建slice

s1 := []int{2, 4, 6, 8}   
s2 := make([]int, 16)
//           类型,  len, cap
s3 := make([]int, 16, 32)

// 删除第4项
s2 = append(s2[:3], s2[4:]...)
```

### Map

```go
m := map[string]string{
    "name":  "zhangCe",
    "place": "demo",
}
fmt.Println(m) // map[name:zhangCe]

m2 := make(map[string]int)
fmt.Println(m2)
for k, v := range m {
    fmt.Println(k, v)
}
// 判断能否取到值
if name, ok := m["name"]; ok {
    fmt.Println(name)
}
// 删除
delete(m, "name")
fmt.Println(m)
```

### 字符串

```go
s := "Yes我爱世界!"
for i, v := range s {
   fmt.Printf("(%d %X)", i, v)
}
fmt.Println(utf8.RuneCountInString(s)) // 8
bytes := []byte(s)
for len(bytes) > 0 {
   // 一个一个解码
   ch, size := utf8.DecodeRune(bytes)
   bytes = bytes[size:]
   fmt.Printf("%c", ch)
}
fmt.Println(bytes)

// 直接转
for i, v := range []rune(s) {
   fmt.Printf("(%d %c)", i, v)
}
```

## 面向"对象"

> go语言只有封装，不支持继承和多态

### 结构体和方法

```go
type treeNode struct {
   value       int
   left, right *treeNode
}

func (node *treeNode) print() {
   fmt.Print(node.value)
}

// 接收者 使用指针作为方法的接收者 只有使用指针才可以改变结构内容
func (node *treeNode) setValue(value int) {
   node.value = value
}

func (node *treeNode) traverse() {
   if node == nil {
      return
   }
   node.left.traverse()
   node.print()
   node.right.traverse()
}


func createNode(value int) *treeNode {
   return &treeNode{value: value}
}

func main() {
   var root treeNode
   root = treeNode{value: 3}
   root.left = &treeNode{}
   root.right = &treeNode{5, nil, nil}
   root.right.left = new(treeNode)
   root.left.right = createNode(2)

   root.print() // 3
   root.right.left.setValue(4)
   root.right.left.print() // 4
   //fmt.Println(root)
   //nodes := []treeNode{
   // {value: 3},
   // {},
   // {6, nil, &root},
   //}
   //fmt.Println(nodes)
}
```
