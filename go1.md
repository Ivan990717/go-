![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683896005024-0e33c8f6-3aff-4a4e-b329-f8eb9a6e5b78.png)

运行命令 `go run xx.go`或者 `go build xx.go + ./xx`

```go
package main

import (
	"fmt"
)

func main() {
	fmt.Println("hello world")
}
```

​          ![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683896951350-61cf9089-bbd3-4a8c-9205-5dca9a5222cf.png)

### 基础语法

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	var a = "ivanlee"
	var b, c int = 1, 2
	var d = true
	var e float64
	f := float32(e)
	g := a + "_regina"
	fmt.Println(a, b, c, d, e, f)
	fmt.Println("g=", g)

	const s string = "constant"
	const h = 50000000
	const i = 3e20 / h
	fmt.Println(s, h, i, math.Sin(i))
}
```

1. 定义变量可分为:var+变量定义，变量 := 
2. 定义常量时没有类型限制，其可根据上下文自行进行定义

​            ![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683897560840-4118e17b-4685-4b54-9438-93e79eac055a.png)



#### if/else

```go
func main() {
	if 7%2 == 0 {
		fmt.Println("7%2==0")
	} else {
		fmt.Println("7%2!=0")
	}

	if num := 9; num < 0 {
		fmt.Println("num < 0")
	} else if num < 10 {
		fmt.Println("0<num<10")
	} else {
		fmt.Println("num>10")
	}
}
```

if 条件当中的语句不需要加括号，也可以在if当中添加变量的定义

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683897922543-06dcdbbb-bed5-4dd7-a2c0-14310d976e51.png)



#### for循环

go语言当中只有for循环，没有while循环

```go
func main() {
	var i int = 1
	for {
		fmt.Println("loop")
		i = i + 1
		if i == 3 {
			break
		}
	}
	for n := 1; n < 9; n++ {
		
		if n%2 == 0 {
			continue
		}
        fmt.Println("n=",n)
	}

	for i <= 5 {
		fmt.Println("i=", i)
		i = i + 1
	}

}
```

如果for循环当中没有条件，则相当于python里面的`while True`，内部没有break则会一直执行

也可以像C++语法中的正常三个条件值进行编写，也可以提前定义变量以后进行范围操作，这一步也类似于`while i<=5`。

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683898477264-bd2cf3b3-28d4-43e1-aa6a-7eec5104ec7b.png)



#### switch

```go
func main() {
	a := 2
	switch a {
	case 1:
		fmt.Println("a=1")
	case 2:
		fmt.Println("a=2")
	case 3, 4, 5:
		fmt.Println("a=3 or 4 or 5")
	default:
		fmt.Println("other")
	}

	t := time.Now()
	switch {
	case t.Hour() < 12:
		fmt.Println("morning")
	default:
		fmt.Println("afternoon")
	}
}
```

switch分支语句的用法中可以使用任意类型的变量，也可以在case语句当中使用，并且当case被命中之后，会直接跳出当前switch，运行后面的语句

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683898860712-b3eb162e-f3b4-46ca-a5a1-e3e4d8a1604a.png)



#### 数组

```go
var a [5]int
a[4] = 100
fmt.Println(a[4], len(a))

b := [5]int{1, 2, 3, 4, 5}
fmt.Println(b)

var c [2][3]int
for i := 0; i < 2; i++ {
    for j := 0; j < 3; j++ {
        c[i][j] = i + j
    }
}
fmt.Println("2d: ", c)
```

定义数组时，大小必须是固定的，所以数组也并不常用。所以一般使用	切片技术，这样也就更像python的数组



```go
s := make([]string, 3)
	s[0] = "a"
	s[1] = "b"

	fmt.Println(s)
	fmt.Println(len(s))

	s = append(s, "c")
	s = append(s, "d", "f")

	fmt.Println(s)

	c := make([]string, len(s))
	copy(c, s)
	fmt.Println(c)

	fmt.Println(c[2:5])
	fmt.Println(c[:5])
	fmt.Println(c[2:])

	good := []string{"g", "o", "o", "d"}
	fmt.Println(good)
```



#### map

```go
m := make(map[string]int)
m["one"] = 1
m["two"] = 2
fmt.Println(m)
fmt.Println(m["one"])
fmt.Println(m["regina"]) //没有key时会输出0
value, ok := m["regina"]
fmt.Println(value, ok)
delete(m, "two")

m2 := map[string]int{"three": 3, "four": 4}
var m3 = map[string]int{"five": 5, "six": 6}

fmt.Println(m2, m3)
```

make函数就是只用于定义，如果要赋值则直接在后面用{}进行赋值

map更像python里面的字典，可以用delete函数删除key，如果map里面没有key，则会有一个false值

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683899934060-eadb9746-31f0-4ccb-af94-4a822b1dfb7a.png)



#### range

```go
n := []int{1，2，3，4，5}
sum := 0
for i, num := range n {
    sum += num
    if num == 2 {
        fmt.Println("index:", i, " num:", num)
    }
}
m := map[string]string{"a": "A", "b": "B"}
for k, v := range m {
    fmt.Println("key:", k, " value:", v)
}
for k := range m {
    fmt.Println("key:", k)
}
```

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683900236601-9fb402c2-2a90-46b6-8996-e0e687a873b7.png)



#### 函数

```go
func add(a int, b int) int {
	return a + b
}
func add2(a, b int) int {
	return a + b
}
func exist(m map[string]string, k string) (v string, ok bool) {
	v, ok = m[k]
	return v, ok
}
func main() {
	fmt.Println(add(1, 2))
	fmt.Println(add2(2, 3))
	fmt.Println(exist(map[string]string{"a": "A", "b": "B"}, "A"))
	fmt.Println(exist(map[string]string{"a": "A", "b": "B"}, "a"))
}
```

函数定义时，参数需要类型定义，以及返回时的类型。如果有多个函数返回值，则分别说明类型

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683900571918-405bc9b3-674d-4908-966d-acb0343d789d.png)



#### 指针

```go
func add(n int) {
	n += 2
}

func add2ptr(n *int) {
	*n += 2
}
func main() {
	n := 5
	add(n)
	fmt.Println(n)
	add2ptr(&n)
	fmt.Println(&n)
	fmt.Println(n)
}
```

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683900973393-f7042845-9336-4d26-9a41-def79c488046.png)



#### 结构体

Go 语言中数组可以存储同一类型的数据，但在结构体中我们可以为不同项定义不同的数据类型。结构体是由一系列具有相同类型或不同类型的数据构成的数据集合。

```go
func checkpwd(u user, pwd string) bool {
	if u.password == pwd {
		return true
	} else {
		return false
	}

}

func checkpwd2(u *user, pwd string) bool {
	if u.password == pwd {
		return true
	} else {
		return false
	}
}

func main() {
	a := user{name: "ivanlee", password: "regina"}
	b := user{"ivanlee", "regina"}
	c := user{name: "ivanlee"}
	c.password = "regina"

	var d user
	d.name = "ivanlee"
	d.password = "password"

	fmt.Println(checkpwd(a, "zjr")) //false
	fmt.Println(checkpwd2(&b, "regina")) //true
}
```

定义一个结构体之后，实例化有abcd四种赋值方法。结构体也拥有其方法，写法要更加简洁



```go
type user struct {
	name     string
	password string
}

func (u user) checkpwd(pwd string) bool {
	return u.password == pwd

}

func (u *user) resetpwd(pwd string) {
	u.password = pwd
}

func main() {
	a := user{name: "ivanlee", password: "regina"}
	a.resetpwd("zjr")
	fmt.Println(a.checkpwd("zjr")) //true
}
func (u user) checkpwd(pwd string) bool` { 这种定义函数的方法，可以使得每一个实例化结构体的对象直接调用，把`func(a,pwd)`的写法变成了`a.func(pwd)
```



#### 字符串操作

```go
func main() {
	a := "hello"
	fmt.Println(strings.Contains(a, "ll"))//包含
	fmt.Println(strings.Count(a, "l"))
	fmt.Println(strings.HasPrefix(a, "he"))
	fmt.Println(strings.HasSuffix(a, "llo"))
	fmt.Println(strings.Index(a, "ll"))
	fmt.Println(strings.Join([]string{"hel", "lo"}, "-"))
	fmt.Println(strings.Repeat(a, 2))
	fmt.Println(strings.Split("a-b-c", "-")) //得到一个数组
	fmt.Println(strings.ToLower(a))
	fmt.Println(strings.ToUpper(a))
	fmt.Println(len(a))
}
```

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683945315072-2eaf7299-5a81-4d11-b2ed-601eee73fce0.png)



#### 字符串格式化

```go
p := point{1, 2}

fmt.Printf("%+v\n", p)
fmt.Printf("%#v\n", p)
fmt.Printf("type: %T\n", p)

fmt.Printf("int %d\n", 123)
fmt.Printf("bin %b\n", 14)
fmt.Printf("char %c\n", 33)
fmt.Printf("hex %x\n", 27)
fmt.Printf("float1 %f\n", 78.9)
fmt.Printf("float2: %e\n", 123400000.0)
fmt.Printf("float3: %E\n", 123400000.0)

fmt.Printf("str1 %s\n", "\"string\"")
fmt.Printf("str2: %q\n", "\"string\"")
fmt.Printf("str3: %x\n", "hex this")

fmt.Printf("pointer: %p\n", &p)

fmt.Printf("width1: |%6d|%6d|\n", 12, 345)
fmt.Printf("width2: |%6.2f|%6.3f|\n", 1.2, 3.45)
fmt.Printf("width3: |%-6.2f|%-6.2f|\n", 1.2, 3.45)
fmt.Printf("width4: |%6s|%6s|\n", "foo", "b")
fmt.Printf("width5: |%-6s|%-6s|\n", "foo", "b")

s := fmt.Sprintf("sprintf: a %s", "string")
fmt.Println(s)

fmt.Fprintf(os.Stderr, "io: an %s\n", "error")
```

第3行：如果值是一个结构体，`%+v `的格式化输出内容将包括结构体的字段名。

第4行：`%#v `根据 Go 语法输出值，即会产生该值的源码片段

第5行：需要打印值的类型，使用 `%T`

第7行：格式化整型数有多种方式，使用 `%d `进行标准的十进制格式化。

8-10行：分别是二进制，字符化，16进制

第11行：`%f`表示浮点数

12-13行：`%e` 和 `%E` 将浮点型格式化为（稍微有一点不同的）科学记数法表示形式。

第15行：`%s`表示输出字符串，如果遇到双引号，使用`%q`

第17行：`%x `输出使用 base-16 编码的字符串， 每个字节使用 2 个字符表示。

第19行：要输出一个指针的值，使用 `%p`

第21行：要指定整数的宽度，请在动词 “%” 之后使用数字。 默认情况下，结果会右对齐并用空格填充。

第22行：也可以指定浮点型的输出宽度，同时也可以通过 `宽度.精度 `的语法来指定输出的精度。

第23行：要左对齐，使用 - 标志

第27行：Printf通过 `os.Stdout` 输出格式化的字符串。 Sprintf 则格式化并返回一个字符串而没有任何输出

第30行：用 `Fprintf `来格式化并输出到` io.Writers` 而不是 `os.Stdout`

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683948011937-25f67122-a298-4f30-a093-4554f6fc3746.png)



#### json

对于一个已有的结构体，只要保证每个字段段第一个字母是大写，也就是公开字段，那么这个结构体就可以用`JSON.marshaler`去序列化，变成一个json字符串。序列化之后的字符串可以通过`JSON.unmarshaler`去反序列化到一个空的变量里面。

```go
package main

import (
	"encoding/json"
	"fmt"
)

type user struct {
	Name  string
	Age   int
	Hobby []string
}

func main() {
	a := user{"ivanlee", 18, []string{"basketball", "math"}}
	buf, err := json.Marshal(a)
	if err != nil {
		panic(err)
	}
	fmt.Println(buf)
	fmt.Println(string(buf))

	buf, err = json.MarshalIndent(a, "", "\t")
	if err != nil {
		panic(err)
	}
	fmt.Println(string(buf))

	var b user
	err = json.Unmarshal(buf, &b)
	if err != nil {
		panic(err)
	}
	fmt.Printf("%#v\n", b)
}
```

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683956411113-a7fb13a8-bbf1-4464-a2ef-3b3cac090a6a.png)

<details class="lake-collapse"><summary id="u7f1fd559"></summary><ul class="ne-ul" style="margin: 0; padding-left: 23px"><li id="u750320de"><span class="ne-text" style="font-size: 16px; color: rgb(77, 77, 77)">只要是可导出成员（变量首字母大写），都可以转成json。</span></li></ul></details>

#### 时间处理

- `time.Now` 得到的当前时间的时区跟电脑的当前时区一样。
- `time.Parse` 把时间字符串转换为Time，时区是UTC时区。**其中****layout****的时间必须是** **"2006-01-02 15:04:05"****这个时间**，不管格式如何，时间点一定得是这个，如："Jan 2, 2006 at 3:04pm (MST)"，"2006-Jan-02"等。如换一个时间解析出来的时间就不对了，要特别注意这一点。
- 不管Time变量存储的是什么时区，其Unix()方法返回的都是距离UTC时间：1970年1月1日0点0分0秒的秒数。
- `Unix()`返回的秒数可以是负数，如果时间小于1970-01-01 00:00:00的话。



```go
func main() {
	now := time.Now()
	fmt.Println(now)
	t1 := time.Date(2000, 1, 27, 1, 25, 36, 0, time.UTC)
	t2 := time.Date(2000, 1, 22, 1, 25, 36, 0, time.UTC)
	fmt.Println(t1)
	fmt.Println(t1.Year(), t1.Month(), t1.Day())
	fmt.Println(t1.Format("2006-01-02 15:04:05"))
	diff := t2.Sub(t1)
	fmt.Println(diff)
	t3, err := time.Parse("2006-01-02 15:04:05", "2022-02-10 01:23:45")
	if err != nil {
		panic(err)
	}
	fmt.Println(t3 == t1)
	fmt.Println(now.Unix())
}
```

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683957757186-eb134020-cd93-4b62-9737-6a5c2221ac2f.png)



#### 数字和字符转换

在go语言中，字符串和数字之间的转换都存在`"STR/conv"`包中，可以使用`parseint`或者`parseFloat`函数解析一个字符串，可以使用`Atoi`函数把一个十进制的字符串转换成数字，用`itoA`函数把数字转换成字符串。

```go
f, _ := strconv.ParseFloat("1.234", 64)
	//inputstring是一个用字符串表示的数字浮点数 bitSize是int类型的参数精度值。对于 float32 可以是 32，对于 float64 可以是 64
	//这个函数总是返回两个值。返回的float64值包含一个浮动数。如果需要，我们可以转换为float32值。如果不能将字符串转换为浮动数，则返回错误值*NumError。
	fmt.Println(f)
	n, _ := strconv.ParseInt("12345", 10, 64)
	//第二个参数代表进制
	fmt.Println(n)
	n1, _ := strconv.ParseInt("0x1000", 0, 64)
	//值为2~36，如果为0，则会根据字符串自动判断前置为"0x"的是16进制；前置为"0"的是8进制；其余的为10进制
	fmt.Println(n1)

	n2, _ := strconv.Atoi("123")
	fmt.Println(n2)
	n3, err := strconv.Atoi("AAA")
	fmt.Println(n3, err)
	n4 := strconv.Itoa(234)
	fmt.Println(n4)
```

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683959007132-6d02c64b-ff55-4f69-8406-2a0d325e863d.png)



#### 进程信息

```go
func main() {
	fmt.Println(os.Args)
	fmt.Println(os.Getenv("PATH"))
	fmt.Println(os.Setenv("AA", "BB"))
	buf, err := exec.Command("grep", "127.0.0.1", "/etc/hosts").CombinedOutput()
	//command里面的参数第一个是执行命令，后面所有全部都是参数
    if err != nil {
		panic(err)
	}
	fmt.Println(string(buf))
}
```

[更多相关os模块用法](http://c.biancheng.net/view/5572.html)

`Getenv` 函数会检索并返回名为 key 的环境变量的值。如果不存在该环境变量则会返回空字符串。

`Setenv` 函数可以设置名为 key 的环境变量，如果出错会返回该错误。

![img](https://cdn.nlark.com/yuque/0/2023/png/35902537/1683960051361-07724858-aa90-4328-8bdf-21b2629b0c51.png)