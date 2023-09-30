0.参考网站

> 1. [Go语言中文网](https://studygolang.com/): 该网站提供了一些学习Go语言的文章、教程和标准库的详细用法。http://c.biancheng.net/golang/
> 2. [Go Playground](https://play.golang.org/): 这是Go官方提供的在线代码平台，可以方便地运行程序，对于学习语言和进行实验很有帮助。
> 3. [Go官方教程](https://tour.golang.org/welcome/1): 这是官方提供的一个交互式教程，旁边配有在线代码平台，非常适合初学者入门。
> 4. [Go by Example](https://gobyexample-cn.github.io/): 这个网站以简洁优美的界面和清晰的代码示例，快速帮助你入门Go语言。
> 5. [Go Walker](https://gowalker.org/): 这是一个可以在线生成和浏览Go项目API文档的网站，支持GitHub等代码托管平台。
> 6. 地鼠文档**网站链接：** https://www.topgoer.cn/
> 7. [API](https://golang.google.cn/doc/)
> 8. [学习路线](https://blog.csdn.net/zyx6a/article/details/122816207?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522169416003416800192212530%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=169416003416800192212530&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-122816207-null-null.142^v93^chatgptT3_2&utm_term=go%E5%AD%A6%E4%B9%A0&spm=1018.2226.3001.4187)
> 9. https://tour.go-zh.org/flowcontrol/10 (彩蛋：为什么 Go Playground 中 time.Now() 是 2009-11-10---->Golang 诞生的日子)
>

练手项目

[wechat-go]( https://github.com/songtianyi/wechat-go)

> https://blog.csdn.net/xiaojin21cen/article/details/124610464)



1.引入

Go 语言最主要的特性：

- 自动垃圾回收
- 更丰富的内置类型
- 函数多返回值
- 错误处理
- 匿名函数和闭包
- 类型和接口
- 并发编程
- 反射
- 语言交互性



9.8

### Ruby vs Go

> Ruby和Go是两种不同的编程语言，它们有一些相似之处，但也有很多不同之处。以下是它们之间的一些主要区别：
>
> 1. **性能**：Go是一种编译型语言，因此它的执行速度比Ruby快得多。这使得Go非常适合处理大量数据和高并发的情况。Ruby是一种解释型语言，因此它的执行速度比Go慢得多。但是，Ruby在处理小型Web应用程序和原型时非常有用。
> 2. **语法**：Go的语法非常简单，易于学习和使用。它的代码结构非常清晰，易于阅读和维护。Ruby的语法比较复杂，但也更灵活。它允许开发人员使用各种编程范例，例如面向对象编程、函数式编程等。
> 3. **生态系统**：Go拥有一个庞大而活跃的社区，提供了许多有用的库和工具。这使得开发人员可以更快地构建应用程序，并且可以轻松地找到解决问题的方法。Ruby也有一个庞大而活跃的社区，但它没有像Go那样广泛的库和工具。
> 4. **适用场景**：由于其出色的性能和并发处理能力，Go非常适合构建高性能Web应用程序、网络服务器、分布式系统等。Ruby则更适合构建小型Web应用程序、原型、脚本等。
>
>  

### Go 用途

Go 语言被设计成一门应用于搭载 Web 服务器，存储集群或类似用途的巨型中央服务器的系统编程语言。

对于高性能分布式系统领域而言，Go 语言无疑比大多数其它语言有着更高的开发效率。它提供了海量并行的支持，这对于游戏服务端的开发而言是再好不过了。

==**注意事项**==

如果你导入了一个包却没有使用它，则会在构建程序时引发错误，如 `imported and not used: os`，这正是遵循了 ==Go 的格言：“没有不必要的代码！”。==





### 日常学习

### *-9.8-*

##### ch1

（？？）在github上找到项目如何自己实现？具体步骤还不知道awa



>#坑  go: go.mod file not found in current directory or any parent directory; see 'go help modules'
>
> **解决**
>
> [go mod没有初始化](



###### **导出名**

在 Go 中，如果一个名字以大写字母开头，那么它就是已导出的。例如，`Pizza` 就是个已导出名，`Pi` 也同样，它导出自 `math` 包。

在导入一个包时，你只能引用其中已导出的名字。任何“未导出”的名字在该包外均无法访问。

###### 函数

当连续两个或多个函数的已命名形参类型相同时，除最后一个类型以外，其它都可以省略。

```go
package main

import "fmt"

func add(x, y int) int {
	return x + y
}

func main() {
	fmt.Println(add(42, 13))
}
```

###### 多值返回

函数可以返回任意数量的返回值。

```go
...
func swap(x, y string) (string, string) {
	return y, x
}

func main() {
	a, b := swap("hello", "world")
	fmt.Println(a, b)
}
```

###### 命名返回值

Go 的返回值可被命名，它们会被视作定义在函数顶部的变量。

返回值的名称应当具有一定的意义，它可以==作为文档使用== 。

没有参数的 `return` 语句返回已命名的返回值。也就是 `直接` 返回。

直接返回语句应当仅用在下面这样的短函数中。在长的函数中它们会影响代码的可读性。

```go
...
func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}

func main() {
	fmt.Println(split(17))
}
```

###### 变量

`var` 语句用于声明一个变量列表，跟函数的参数列表一样，类型在最后。

就像在这个例子中看到的一样，`var` 语句可以出现在包或函数级别。

```go
...
var c, python, java bool

func main() {
	var i int
	fmt.Println(i, c, python, java)
}
```

###### 变量的初始化

变量声明可以包含初始值，每个变量对应一个。

如果初始化值已存在，则可以省略类型；变量会从初始值中获得类型。

```go
...
var i, j int = 1, 2

func main() {
	var c, python, java = true, false, "no!"
	fmt.Println(i, j, c, python, java)
}
```

###### 短变量声明

在函数中，简洁赋值语句 `:=` 可在类型明确的地方代替 `var` 声明。

函数外的每个语句都必须以关键字开始（`var`, `func` 等等），因此 `:=` 结构不能在函数外使用。

```go
...
func main() {
	var i, j int = 1, 2
	k := 3
	c, python, java := true, false, "no!"

	fmt.Println(i, j, k, c, python, java)
}

```

###### 基本类型

Go 的基本类型有

> 这些是 Go 语言中的整数、无符号整数、浮点数和复数类型的数据定义：
>
> - `int` 表示有符号整数类型，其大小和机器相关（在大多数平台上是32位或64位）。
> - `int8` 是一个有符号的8位整数，其值范围为-128 到 127。
> - `int16` 是一个有符号的16位整数，其值范围为-32768 到 32767。
> - `int32` 是一个有符号的32位整数，其值范围为-2147483648 到 2147483647。
> - `int64` 是一个有符号的64位整数，其值范围为-9223372036854775808 到 9223372036854775807。
>
> - `uint` 表示无符号整数类型，其大小和机器相关（在大多数平台上是32位或64位）。
> - `uint8` 是一个无符号的8位整数，其值范围为0 到 255。
> - `uint16` 是一个无符号的16位整数，其值范围为0 到 65535。
> - `uint32` 是一个无符号的32位整数，其值范围为0 到 4294967295。
> - `uint64` 是一个无符号的64位整数，其值范围为0 到 18446744073709551615。
>
> - **`uintptr` 是一个无符号整数类型，足以容纳指针的位模式。它用于存储指针值的底层二进制表示。**
>
> - `byte` 是 `uint8` 的别名，用于表示字节类型。
>
> - **`rune` 是 `int32` 的别名，用于表示 Unicode 码点。它可以存储任何 Unicode 代码点的值**。
>
> - `float32` 是一个单精度浮点数，根据 IEEE-754 标准采用32位格式存储。
> - `float64` 是一个双精度浮点数，根据 IEEE-754 标准采用64位格式存储。
>
> - **`complex64` 是一个用于表示具有实部和虚部的复数的复数类型。实部和虚部都是 `float32` 类型。**
> - **`complex128` 是一个用于表示具有实部和虚部的复数的复数类型。实部和虚部都是 `float64` 类型**。

```go
...
var (
	ToBe   bool       = false
	MaxInt uint64     = 1<<64 - 1
	z      complex128 = cmplx.Sqrt(-5 + 12i)
)

func main() {
	fmt.Printf("Type: %T Value: %v\n", ToBe, ToBe)
	fmt.Printf("Type: %T Value: %v\n", MaxInt, MaxInt)
	fmt.Printf("Type: %T Value: %v\n", z, z)
}

```

###### 类型转换

表达式 `T(v)` 将值 `v` 转换为类型 `T`。

一些关于数值的转换：

```go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)
```

或者，更加简单的形式：

```go
i := 42
f := float64(i)
u := uint(f)
```

与 C 不同的是，Go 在不同类型的项之间赋值时需要显式转换。

```go
...
func main() {
	var x, y int = 3, 4
	var f float64 = math.Sqrt(float64(x*x + y*y))
	var z uint = uint(f)
	fmt.Println(x, y, z)
}
// 3 4 5
```

######  类型推导

在声明一个变量而不指定其类型时（即使用不带类型的 `:=` 语法或 `var =` 表达式语法），变量的类型由右值推导得出。

当右值声明了类型时，新变量的类型与其相同：

```
var i int
j := i // j 也是一个 int
```

不过当右边包含未指明类型的数值常量时，新变量的类型就可能是 `int`, `float64` 或 `complex128` 了，这取决于常量的精度：

```
i := 42           // int
f := 3.142        // float64
g := 0.867 + 0.5i // complex128
```

尝试修改示例代码中 `v` 的初始值，并观察它是如何影响类型的。

```go
...
func main() {
	v := 3+2i // 修改这里！
	fmt.Printf("v is of type %T\n", v)
}
//v is of type complex128
```



###### 数值常量

数值常量是高精度的 **值**。

一个未指定类型的常量由上下文来决定其类型。

再尝试一下输出 `needInt(Big)` 吧。

（`int` 类型最大可以存储一个 64 位的整数，有时会更小。）

（`int` 可以存放最大64位的整数，根据平台不同有时会更少。）

```go
...
const (
	// 将 1 左移 100 位来创建一个非常大的数字
	// 即这个数的二进制是 1 后面跟着 100 个 0
	Big = 1 << 100
	// 再往右移 99 位，即 Small = 1 << 1，或者说 Small = 2
	Small = Big >> 99
)

func needInt(x int) int { return x*10 + 1 }
func needFloat(x float64) float64 {
	return x * 0.1
}

func main() {
	fmt.Println(needInt(Small))
	fmt.Println(needFloat(Small))
	fmt.Println(needFloat(Big))
	//fmt.Println(needInt(Big)) 爆int了
}
```

##### ch2

###### for

Go 只有一种循环结构：`for` 循环。

基本的 `for` 循环由三部分组成，它们用分号隔开：

- 初始化语句：在第一次迭代前执行
- 条件表达式：在每次迭代前求值
- 后置语句：在每次迭代的结尾执行

初始化语句通常为一句短变量声明，该变量声明仅在 `for` 语句的作用域中可见。

一旦条件表达式的布尔值为 `false`，循环迭代就会终止。

**注意**：和 C、Java、JavaScript 之类的语言不同，==Go 的 for 语句后面的三个构成部分外没有小括号==， 大括号 `{ }` 则是必须的。

```go
...
func main() {
	sum := 0
	for i := 0; i < 10; i++ {
		sum += i
	}
	fmt.Println(sum)
}
```

初始化语句和后置语句是可选的。

```go
...
func main() {
	sum := 1
	for ; sum < 1000; {
		sum += sum
	}
	fmt.Println(sum)
}
```

**==for 是 Go 中的 “while”==**

此时你可以去掉分号，因为 C 的 `while` 在 Go 中叫做 `for`。

```go
...
func main() {
	sum := 1
	for sum < 1000 {
		sum += sum
	}
	fmt.Println(sum)
}
```

**无限循环**如果省略循环条件，该循环就不会结束，因此无限循环可以写得很紧凑。

```go
...
func main() {
	for {
	}
}
package main



```

###### if

Go 的 `if` 语句与 `for` 循环类似，表达式外无需小括号 `( )` ，而大括号 `{ }` 则是必须的。

```go
package main
import (
	"fmt"
	"math"
)
func sqrt(x float64) string {
	if x < 0 {
		return sqrt(-x) + "i"
	}
	return fmt.Sprint(math.Sqrt(x))
}

func main() {
	fmt.Println(sqrt(2), sqrt(-4))
}
```

==if with short statement==

Go 语言中的语法特性之一，称为 "**短变量声明**" 或 "**if with short statement**"

(如下的"v")

```go
...
func pow(x, n, lim float64) float64 {
    // 在 if 语句的条件部分，使用 := 定义并赋值了一个局部变量 v
    //它的作用域仅在 if 语句内部
	
	if v := math.Pow(x, n); v < lim {
		return v	// v 接收 math.Pow(x, n) 计算的幂次方结果，并判断是否小于 lim
	}
	return lim
}

func main() {
	fmt.Println(
		pow(3, 2, 10),
		pow(3, 3, 20),
	)
}
```

###### if 和 else

在 `if` 的简短语句中声明的变量同样可以在任何对应的 `else` 块中使用。

（在 `main` 的 `fmt.Println` 调用开始前，两次对 `pow` 的调用均已执行并返回其各自的结果。）

```go
...
func pow(x, n, lim float64) float64 {
	if v := math.Pow(x, n); v < lim {
		return v
	} else {
		fmt.Printf("%g >= %g\n", v, lim)
	}
	// 这里开始就不能使用 v 了
	return lim
}

func main() {
	fmt.Println(
		pow(3, 2, 10),
		pow(3, 3, 20),
	)
}
//27 >= 20
//9 20

```

`%g` : 

>  `%g` 是 `fmt` 包中的格式化动词之一，用于将浮点数格式化为一种紧凑但精确的表示形式。
>
> - 对于大于 1e-4 或者小于 1e20 的浮点数，`%g` 格式会像 `%f` 一样给出小数点形式，并且通过去除末尾的 0 来降低精度。
> - 对于较大或较小的数字，`%g` 会使用指数形式，基于尾数除以 10 的幂的方式来表示。
>
> 示例输出中可能显示类似于 "1.2345e+02 >= 100" 的结果，它表示 v 的值为 "1.2345e+02"（即 123.45），lim 的值为 100。
>
> 这里使用 `%g` 的目的是以一种简洁且具有可读性的方式，将浮点数的值输出到标准输出中。

**switch**

`switch` 是编写一连串 `if - else` 语句的简便方法。它运行第一个值等于条件表达式的 case 语句。

Go 的 switch 语句类似于 C、C++、Java、JavaScript 和 PHP 中的，不过 Go 只运行选定的 case，而非之后所有的 case。 实际上，Go 自动提供了在这些语言中每个 case 后面所需的 `break` 语句。 除非以 `fallthrough` 语句结束，否则分支会自动终止。 Go 的另一点重要的不同在于 switch 的 case 无需为常量，且取值不必为整数。

```go
package main

import (
	"fmt"
	"runtime" //导入 runtime 包，用于访问与运行时环境有关的函数和变量
)

func main() {
	fmt.Print("Go runs on ")
	switch os := runtime.GOOS; os {
	case "darwin":
		fmt.Println("OS X.")
	case "linux":
		fmt.Println("Linux.")
	default:
		// freebsd, openbsd,
		// plan9, windows...
		fmt.Printf("%s.\n", os)
	}
}
```

> `runtime.GOOS` 是 Go 语言中的一个常量，它表示当前运行程序的操作系统类型。
>
> `runtime` 包提供了访问与运行时环境有关的函数和变量的能力，而 `GOOS` 是其中一个常量。它的值在运行时由 Go 编译器根据不同的操作系统设定。



###### switch 

switch 的 case 语句**==从上到下顺次执行，直到匹配成功时停止==**。

（例如，

```go
switch i {
case 0:
case f():
}
```

在 `i==0` 时 `f` 不会被调用。）

*注意：* Go 练习场中的时间总是从 2009-11-10 23:00:00 UTC 开始，该值的意义留给读者去发现。

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	today := time.Now().Weekday()
	fmt.Println(today)
	fmt.Println("When's Saturday?")
	switch time.Saturday {
	case today + 0:
		fmt.Println("Today.")
	case today + 1:
		fmt.Println("Tomorrow.")
	case today + 2:
		fmt.Println("In two days.")
	case today + 3:
		fmt.Println("In three days.")
	default:
		fmt.Println("Too far away.")
	}
}
/*
Tuesday
When's Saturday?
Too far away.
*/
```

另一种方式

```go
func main() {
	today := time.Now().Weekday()
	// 根据 Go 语言的时间和日期表达方式，周日是 0，周一是 1，以此类推

	// 使用一个 map 来映射为符合你期望的格式输出
	daysOfWeek := map[time.Weekday]string{
		time.Sunday:    "Sunday",
		time.Monday:    "Monday",
		time.Tuesday:   "Tuesday",
		time.Wednesday: "Wednesday",
		time.Thursday:  "Thursday",
		time.Friday:    "Friday",
		time.Saturday:  "Saturday",
	}

	fmt.Println(daysOfWeek[today])
}
```

没有条件的 switch

没有条件的 switch 同 `switch true` 一样。

这种形式能将一长串 if-then-else 写得更加清晰。

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	t := time.Now()
	fmt.Println(t)
	switch {
	case t.Hour() < 12:
		fmt.Println("Good morning!")
	case t.Hour() < 17:
		fmt.Println("Good afternoon.")
	default:
		fmt.Println("Good evening.")
	}
}
/*
2009-11-10 23:00:00 +0000 UTC m=+0.000000001
Good evening.
*/
```

###### defer

defer 语句会将函数推迟到外层函数返回之后执行。

推迟调用的函数其参数会立即求值，但直到外层函数返回前该函数都不会被调用

```go
func main() {
	fmt.Println("Cecilia")
	fmt.Println("hello")
	defer fmt.Println("world")
}
```



在这个例子中，我们使用 `defer` 关键字将 `fmt.Println("world")` 延迟到 `main` 函数执行结束之后再执行。因此，在 `fmt.Println("world")` 被推迟执行期间，程序首先执行了 `fmt.Println("hello")` 。

###### defer 栈

​	推迟的函数调用会被压入一个栈中。当外层函数返回时，被推迟的函数会按照后进先出的顺序调用。//`defer` 关键字按照**后进先出（LIFO）**的顺序处理被延迟的函数调用。这意味着如果有多个 `defer` 函数的调用，则最后一个被推迟的函数会在函数结束前最先执行。

​	`defer` 可以用来在函数执行结束时执行一些资源清理、关闭文件、解锁资源等操作。它确保在函数返回前进行这些操作，无论函数是正常返回还是由于 panic 异常而返回。这种特性使得 `defer` 很有用，可以减少代码重复和改善代码可读性。



### *-9.12-*

##### ch3



###### 指针

Go 拥有指针。指针保存了值的内存地址。

类型 `*T` 是指向 `T` 类型值的指针。其零值为 `nil`。

```
var p *int
```

`&` 操作符会生成一个指向其操作数的指针。

```
i := 42
p = &i
```

`*` 操作符表示指针指向的底层值。

```
fmt.Println(*p) // 通过指针 p 读取 i
*p = 21         // 通过指针 p 设置 i
```

这也就是通常所说的“间接引用”或“重定向”。

与 C 不同，Go 没有指针运算。

```go
package main

import "fmt"

func main() {
	i, j := 42, 2701

	p := &i         // 指向 i
	fmt.Println(*p) // 通过指针读取 i 的值
	*p = 21         // 通过指针设置 i 的值
	fmt.Println(i)  // 查看 i 的值

	p = &j         // 指向 j
	*p = *p / 37   // 通过指针对 j 进行除法运算
	fmt.Println(j) // 查看 j 的值
}
```

###### 结构体

- 一个结构体（`struct`）就是一组字段（field）。

- 结构体字段使用点号来访问。

  结构化的类型没有真正的值，它使用 `nil` 作为默认值（在 Objective-C 中是 nil，在 Java 中是 null，在 C 和 C++ 中是 NULL 或 0）。值得注意的是，Go 语言中不存在类型继承。

```go
type Vertex struct{
    X int
    Y int
}
func main(){
    v:=Vertex{1,2}
    v.X=4;
    fmt.Println(v.X)			//4
    fmt.Println(Vertex{1,2})	//{1,2}
}
```

- 结构体字段可以通过结构体指针来访问。

  如果我们有一个指向结构体的指针 `p`，那么可以通过 `(*p).X` 来访问其字段 `X`。不过这么写太啰嗦了，所以语言也允许我们使用隐式间接引用，直接写 `p.X` 就可以。

```go
type Vertex struct{
    X int
    Y int
}
func main(){
    v := Vertex{1,2}
    p := &v
    p.X=1e9			//(*p).X = 1e9
    fmt.Println(v)	//{1000000000 2}
}
```

- 结构体文法

  结构体文法通过直接列出字段的值来新分配一个结构体。

  使用 `Name:` 语法可以仅列出部分字段。（字段名的顺序无关。）

  特殊的前缀 `&` 返回一个指向结构体的指针。

  ```go
  type Vertex struct{
      X ,Y int
  }
  var(
      v1 = Vertex{1,2}
      v2 = Vertex{X: 1}	//Y:0
      v3 = Vertex{}		//X:0 Y:0
      p = &Vertex{1,2}	// 创建一个 *Vertex 类型的结构体（指针）
  )
  ```



###### 数组

类型 `[n]T` 表示拥有 `n` 个 `T` 类型的值的数组。

表达式

```
var a [10]int
```

会将变量 `a` 声明为拥有 10 个整数的数组。

数组的长度是其类型的一部分，因此数组不能改变大小。这看起来是个限制，不过没关系，Go 提供了更加便利的方式来使用数组。

 ```go
 func main() {
 	var a [2]string
 	a[0] = "Hello"
 	a[1] = "World"
 	fmt.Println(a[0], a[1])
 	fmt.Println(a)
 
 	primes := [6]int{2, 3, 5, 7, 11, 13}
 	fmt.Println(primes)
 }
 ```

###### 切片

每个数组的大小都是固定的。而切片则为数组元素提供动态大小的、灵活的视角。在实践中，切片比数组更常用。

类型 `[]T` 表示一个元素类型为 `T` 的切片。

切片通过两个下标来界定，即一个上界和一个下界，二者以冒号分隔：

```
a[low : high]
```

它会选择一个半开区间，包括第一个元素，但排除最后一个元素。

以下表达式创建了一个切片，它包含 `a` 中下标从 1 到 3 的元素：

```
a[1:4]
```

```go
func main(){
    primes :=[6]int{2,3,5,7,11,13}
    var s[]int = primes[1:4]
    fmt.Println(s)
}
```

-  ==切片就像数组的引用==

  切片并不存储任何数据，它只是描述了底层数组中的一段。

  更改切片的元素会修改其底层数组中对应的元素。

  与它共享底层数组的切片都会观测到这些修改。

  ```go
  func main() {
  	names := [4]string{
  		"John",
  		"Paul",
  		"George",
  		"Ringo",
  	}
  	fmt.Println(names)
  
  	a := names[0:2]
  	b := names[1:3]
  	fmt.Println(a, b)
  
  	b[0] = "XXX"
  	fmt.Println(a, b)
  	fmt.Println(names)
  }/*
  [John Paul George Ringo]
  [John Paul] [Paul George]
  [John XXX] [XXX George]
  [John XXX George Ringo]
  */
  ```

- ==切片文法==

  切片文法类似于没有长度的数组文法。

  这是一个数组文法：

  ```
  [3]bool{true, true, false}
  ```

  下面这样则会创建一个和上面相同的数组，然后构建一个引用了它的切片：

  ```
  []bool{true, true, false}
  ```

```go
func main() {
	q := []int{2, 3, 5, 7, 11, 13}
	fmt.Println(q)

	r := []bool{true, false, true, true, false, true}
	fmt.Println(r)

	s := []struct {
		i int
		b bool
	}{
		{2, true},
		{3, false},
		{5, true},
		{7, true},
		{11, false},
		{13, true},
	}
	fmt.Println(s)
}
/*
[2 3 5 7 11 13]
[true false true true false true]
[{2 true} {3 false} {5 true} {7 true} {11 false} {13 true}]
*/
```

- ==切片的默认行为==

  在进行切片时，你可以利用它的默认行为来忽略上下界。

  切片下界的默认值为 `0`，上界则是该切片的长度。

  对于数组

  ```
  var a [10]int
  ```

  来说，以下切片是等价的：

  ```
  a[0:10]
  a[:10]
  a[0:]
  a[:]
  ```

-  ==切片的长度与容量==

  切片拥有 **长度** 和 **容量**。

  切片的长度就是它所包含的元素个数。

  切片的容量是从它的第一个元素开始数，到其底层数组元素末尾的个数。

  切片 `s` 的长度和容量可通过表达式 `len(s)` 和 `cap(s)` 来获取。

  你可以通过重新切片来扩展一个切片，给它提供足够的容量。试着修改示例程序中的切片操作，向外扩展它的容量，看看会发生什么。

  ```go
  func main() {
  	s := []int{2, 3, 5, 7, 11, 13}
  	printSlice(s)
  
  	// 截取切片使其长度为 0
  	s = s[:0]
  	printSlice(s)
  
  	// 拓展其长度
  	s = s[:4]
  	printSlice(s)
  
  	// 舍弃前两个值
  	s = s[2:]
  	printSlice(s)
  	
  	s = s[0:4]
  	printSlice(s)
  }
  
  func printSlice(s []int) {
  	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)
  }
  /*
  len=6 cap=6 [2 3 5 7 11 13]
  len=0 cap=6 []
  len=4 cap=6 [2 3 5 7]
  len=2 cap=4 [5 7]
  len=4 cap=4 [5 7 11 13]
  */
  ```

- nil 切片

  切片的零值是 `nil`。

  nil 切片的长度和容量为 0 且没有底层数组。

  ```go
  func main() {
  	var s []int
  	fmt.Println(s, len(s), cap(s))
  	if s == nil {
  		fmt.Println("nil!")
  	}
  }
  /*
  [] 0 0
  nil!
  */
  ```



- 用 make 创建切片

  切片可以用内建函数 `make` 来创建，这也是你创建动态数组的方式。

  `make` 函数会分配一个元素为零值的数组并返回一个引用了它的切片：

  ```
  a := make([]int, 5)  // len(a)=5
  ```

  要指定它的容量，需向 `make` 传入第三个参数：

  ```
  b := make([]int, 0, 5) // len(b)=0, cap(b)=5
  
  b = b[:cap(b)] // len(b)=5, cap(b)=5
  b = b[1:]      // len(b)=4, cap(b)=4
  ```

   	

```go
func main() {
	a := make([]int, 5)
	printSlice("a", a)

	b := make([]int, 0, 5)
	printSlice("b", b)

	c := b[:2]
	printSlice("c", c)

	d := c[2:5]
	printSlice("d", d)
}

func printSlice(s string, x []int) {
	fmt.Printf("%s len=%d cap=%d %v\n",
		s, len(x), cap(x), x)
}
/*
a len=5 cap=5 [0 0 0 0 0]
b len=0 cap=5 []
c len=2 cap=5 [0 0]
d len=3 cap=3 [0 0 0]
*/
```



- 切片的切片

  切片可包含任何类型，甚至包括其它的切片。

  

```go
...
import (
	"fmt"
	"strings"
)

func main() {
	// 创建一个井字板（经典游戏）
	board := [][]string{
		[]string{"_", "_", "_"},
		[]string{"_", "_", "_"},
		[]string{"_", "_", "_"},
	}

	// 两个玩家轮流打上 X 和 O
	board[0][0] = "X"
	board[2][2] = "O"
	board[1][2] = "X"
	board[1][0] = "O"
	board[0][2] = "X"

	for i := 0; i < len(board); i++ {
		fmt.Printf("%s\n", strings.Join(board[i], " "))
	}
}

```



- 向切片追加元素

  为切片追加新的元素是种常用的操作，为此 Go 提供了内建的 `append` 函数。内建函数的[文档](https://go-zh.org/pkg/builtin/#append)对此函数有详细的介绍。

  ```
  func append(s []T, vs ...T) []T
  ```

  `append` 的第一个参数 `s` 是一个元素类型为 `T` 的切片，其余类型为 `T` 的值将会追加到该切片的末尾。

  `append` 的结果是一个包含原切片所有元素加上新添加元素的切片。

  当 `s` 的底层数组太小，不足以容纳所有给定的值时，它就会分配一个更大的数组。返回的切片会指向这个新分配的数组。

  （要了解关于切片的更多内容，请阅读文章 [Go 切片：用法和本质](https://blog.go-zh.org/go-slices-usage-and-internals)。）

  ```go
  package main
  
  import "fmt"
  
  func main() {
  	var s []int
  	printSlice(s)
  
  	// 添加一个空切片
  	s = append(s, 0)
  	printSlice(s)
  
  	// 这个切片会按需增长
  	s = append(s, 1)
  	printSlice(s)
  
  	// 可以一次性添加多个元素
  	s = append(s, 2, 3, 4)
  	printSlice(s)
  }
  
  func printSlice(s []int) {
  	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)
  }
  /*
  len=0 cap=0 []
  len=1 cap=1 [0]
  len=2 cap=2 [0 1]
  len=5 cap=6 [0 1 2 3 4]
  */
  ```

  

###### Range

`for` 循环的 `range` 形式可遍历切片或映射。

当使用 `for` 循环遍历切片时，每次迭代都会返回两个值。第一个值为当前元素的下标，第二个值为该下标所对应元素的一份副本。

