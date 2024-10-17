### 环境设置
由于是从github下载，国内网络大概率会失败，这个时候在vscode打开一个终端，

**运行：**

设置代理 `go env -w GOPROXY=[https://goproxy.cn](https://goproxy.cn)`

清空缓存 `go clean --modcache`

```python
# 模块代理: 
export GOPROXY=https://goproxy.cn
# 初始化一个新的 Go 模块（当前项目只需执行一次）
go mod init hello  
# 执行 go mod tidy 可以确保项目依赖的干净和正确，移除未使用的依赖并获得确切的依赖版本。这有助于减少项目体积，确保项目的构建正确性，并遵循 Go 模块规范
go mod tidy
```

### 变量定义
#### 普通变量
```go
var name string = "cui"

var name = "cui"

age = 23 // 解释器会根据后面的值自动推导出数据类型

name := "cui"  // 推荐

var name,message,data string

var (
    name   = "cui"
    age    = 18
    hobby  = "skate"
    salary = 1000000
    gender string  // 只声明但不赋值，有一个默认： ""
    length int     // 只声明但不赋值，有一个默认： 0
    sb bool     // 只声明但不赋值，有一个默认： false
)
```

#### 常量
一般常量都放在开头

```go
// 定义常量放在import之后
//const age int = 98
const age = 98

// 常量因式分解
const (
    v1 = 123
    v2 = 456
    pi = 9.9
)
```

### <font style="color:rgb(31, 35, 40);">iota</font>
<font style="color:rgb(31, 35, 40);">可有可无，当做一个在声明常量时的一个计数器</font>

```go
	const (
		monday = iota + 1
		tuesday
		wednesday
		thursday
		friday
		saturday
		sunday
	)
	fmt.Println(monday, tuesday, wednesday)

>>> 1 2 3
```

### scan、scanln、scanf输入的区别
`fmt.Scan`    读取输入存储在变量中

`fmt.Scanln`  读取输入存储在变量中，`<font style="color:#DF2A3F;">等待回车就结束</font>`

`fmt.Scanf`    提取字符中的变量

```go
package main

import "fmt"

func main() {
	// 示例一：fmt.Scan
		var name string
		// fmt.println在下一行输入
		fmt.Print("请输入用户名:")
		fmt.Scan(&name) //读取输入的名字存储在name变量中
		fmt.Println(name)

	// 示例2：fmt.Scan
		var name string
		var age int

		fmt.Println("请输入用户名：")
		// 当使用Scan时，会提示用户输入
		// 用户输入完成之后，会得到两个值：count(用户输入了几个值)；err(用输入错误则是错误信息) '_'变量可以不被引用
		_, err := fmt.Scan(&name, &age)
		if err == nil {
			fmt.Println(name, age)
		} else {
			fmt.Println("用户输入数据错误", err)
		}
		// 特别说明：fmt.Scan 要求输入两个值，必须输入两个，否则他会一直等待。

	// 示例三：fmt.Scanln
	var name string
	var age int
	fmt.Print("请输入用户名：")
	count, err := fmt.Scanln(&name, &age)
	fmt.Println(count, err)
	fmt.Println(name, age)
	// 特别说明：fmt.Scanln 等待回车就结束.

}


# fmt.Scanf示例
// 有个小bug，提取变量会带上后面的字符，可用空格区分解决
package main
import "fmt"
func main() {
	var name string
	fmt.Print("请输入用户名：")
	// Scanf提取出
	_, _ = fmt.Scanf("我叫%s今年23岁", &name)
	fmt.Println(name)
}

>>> 输出:
请输入用户名：我叫sks今年23岁
sks今年23岁
```

#### 输入中有空格无法识别问题
![](https://cdn.nlark.com/yuque/0/2024/png/34804726/1722499791076-91339971-395a-4d98-9d03-7b07fe1b41be.png)

#### 解决方法
使用本地的标准输出导入

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	reader := bufio.NewReader(os.Stdin)
	// line，从stdin中读取一行的数据（字节集合 -> 转化成为字符串）
	// reader默认一次能4096个字节（4096/3)
	//    1. 一次性读完，isPrefix=false
	// 	  2. 先读一部分，isPrefix=true，再去读取isPrefix=false
	line, _, _ := reader.ReadLine()
	data := string(line)
	fmt.Println(data)
}

```

### if条件判断
```go
package main

func main() {
	// 判断输入姓名是否为cui
	var name string
	fmt.Println("请输入姓名")
	fmt.Scan(&name)
	if name == "cui" {
		fmt.Println("success")
	} else {
		fmt.Println("err")
	}

	// 判断账号密码
	var username, password string
	fmt.Print("请输入用户名：")
	fmt.Scanln(&username)
	fmt.Print("请输入密码：")
	fmt.Scanln(&password)
	if username == "cui" && password == "123" {
		fmt.Println("success")
	} else {
		fmt.Println("err")
	}
}

```

#### 多条件判断
```go
if 条件A{
    ...
}else if 条件B{
    ...
}else if 条件C{
    ...
}else{
    ...
}
```

### switch语句
类似与shell的case语句

```go
package main

import "fmt"

func main() {
	Name_()
	More_num()
	Expl_()
	Fall_switch()
	Type_()
}

// 基本语句
func Name_() {
	var name string
	fmt.Println("输入姓名")
	fmt.Scanln(&name)
	switch name {
	case "cui":
		fmt.Println("success")
	case "cat":
		fmt.Println("err")
	default:
		fmt.Println("not found")
	}
}

// 针对多个值的语句
func More_num() {
	num := 3
	switch num {
	case 1, 3, 5:
		fmt.Println("奇数")
	case 2, 4, 6:
		fmt.Println("偶数")
	}
}

// 在case中使用表达式
func Expl_() {
	score := 85
	switch {
	case score > 90:
		fmt.Println("A 等级")
	case score > 80:
		fmt.Println("B 等级")
	case score > 70:
		fmt.Println("C 等级")
	default:
		fmt.Println("D 等级")
	}
}

// 示例4: 使用fallthrough关键字
/* Go里面switch默认相当于每个case最后带有break，
   匹配成功后不会自动向下执行其他case，而是跳出整个switch,
   但是可以使用fallthrough强制执行后面的case代码。
*/
func Fall_switch() {
	number := 10
	switch {
	case number == 10:
		fmt.Println("等于10")
		fallthrough
	case number >= 10:
		fmt.Println("10 或更多")
	}
}

// 示例5: 对类型进行Switch
func Type_() {
	var x interface{}
	x = 10
	switch x.(type) {
	case int:
		fmt.Println("x 是一个整数")
	case float64:
		fmt.Println("x 是一个浮点数")
	case string:
		fmt.Println("x 是一个字符串")
	default:
		fmt.Println("未知类型")
	}
}

>>> 输出
输入姓名
cui
success
奇数
B 等级
等于10
10 或更多
x 是一个整数
```

### for循环
```go
// 死循环
for {
    ...
}

// 条件
for 1>2 {
    ...
}

// 布尔值
flag := true
for flag {
    
}
```

#### 变量&条件&变量赋值
```go
// 对于 i=i+1简写 > i++
for i:=1;i<10;i=i+1 {
    fmt.Println("钓鱼要掉刀鱼，刀鱼要到岛上钓")
}

// 简化为：
for i:=1;i<10;i++ {
    fmt.Println("钓鱼要掉刀鱼，刀鱼要到岛上钓")
}
```

#### for循环猜数字
```go
package main
import (
	"fmt"
)
func main() {
	num := 66
	flag := true
	for flag {
		var guessnum int
		fmt.Println("请输入猜的数字")
		fmt.Scanln(&guessnum)
		if guessnum > num {
			fmt.Println("猜大了")
		} else if guessnum < num {
			fmt.Println("猜小了")
		} else {
			fmt.Println("猜对了")
			flag = false
		}
	}
}

```

#### 逆序输出10-1
```go
package main

import "fmt"

func main() {
	for i := 10; i > 0; i-- {
		fmt.Println(i)
	}
}
```

#### for循环嵌套
```go
for i:=1;i<3;i++{
    // i=1
    // i=2
    for j:=1;j<5;j++{
        // j=1/2/3/4
        if j == 3{
            continue
        }
        fmt.Println(i,j)
    }
}

>>> 输出：
1 1
1 2
1 4
2 1
2 2
2 4
```

#### continue
```go
func main() {
	for i := 1; i <= 10; i++ {
		if i == 7 {
			continue
		}
		fmt.Println(i)
	}
}

// 方式二
if i != 7 {
    fmt.Println(i)
}
```

#### break
```go
for i:=1;i<3;i++{
    // i=1
    // i=2
    for j:=1;j<5;j++{
        // j=1/2/3/4
        if j == 3{
            break
        }
        fmt.Println(i,j)
    }
}

>>> 输出：
1 1
1 2
2 1
2 2
```

#### <font style="color:rgb(31, 35, 40);">对for进行打标签，然后通过break和continue就可以实现多层循环的跳出和终止</font>
```go
f1:
	for i := 1; i < 3; i++ {
		// i=1
		// i=2
		for j := 1; j < 5; j++ {
			// j=1/2/3/4
			if j == 3 {
				continue f1
			}
			fmt.Println(i, j)
		}
	}

>>> 输出：
1 1
1 2
2 1
2 2

------------------------------------------------------------------------

f1:
	for i := 1; i < 3; i++ {
		// i=1
		// i=2
		for j := 1; j < 5; j++ {
			// j=1/2/3/4
			if j == 3 {
				break f1
			}
			fmt.Println(i, j)
		}
	}

>>> 输出：
1 1
1 2
```

### <font style="color:rgb(31, 35, 40);">goto语句</font>
```go
	var name string
	fmt.Println("请输入姓名:")
	fmt.Scanln(&name)

	if name == "cuijian" {
		//svip
		goto SVIP
	} else if name == "xiaohe" {
		//vip
		goto VIP
	}
	fmt.Println("预约...")
VIP:
	fmt.Println("等号...")
SVIP:
	fmt.Println("进入...")
```

### return用法
```go
package main

import "fmt"

func printNumbers() {
	for i := 1; i <= 5; i++ {
		if i == 4 {
			return // 当i等于3时，提前结束函数的执行
		}
		fmt.Println(i)
	}
}

func main() {
	printNumbers()
}

```

### 格式化字符串
```go
	var name, address, action string
	fmt.Print("请输入姓名：")
	fmt.Scanln(&name)

	fmt.Print("请输入位置：")
	fmt.Scanln(&address)

	fmt.Print("请输入行为：")
	fmt.Scanln(&action)

	result := fmt.Sprintf("我叫%s,在%s正在%s", name, address, action)
    // 方法2：fmt.Printf("我叫%s,在%s正在%s", name, address, action)
	//result := "我叫" + name + "在" + address + "干" + action
	fmt.Println(result)
```

### fmt.Sprintf、fmt.Printf、fmt.Println区别
`fmt.Sprintf：`将格式化的字符串返回，但不输出（可以将返回的字符串赋值给一个变量，或者在其他地方使用）

`fmt.Printf：`将格式化的字符串直接输出到标准输出（通常是控制台）

`fmt.Printlb：`<font style="color:rgba(0, 0, 0, 0.9);">将参数列表中的值输出到标准输出，并在每个值之间添加空格，最后添加换行符</font>

### <font style="color:rgb(31, 35, 40);">运算符</font>
#### 算数运算符
![](https://github.com/WuPeiqi/go_course/raw/master/day03%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E5%8F%A5/%E7%AC%94%E8%AE%B0/assets/image-20200602230315027.png)

#### 关系运算符
![](https://github.com/WuPeiqi/go_course/raw/master/day03%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E5%8F%A5/%E7%AC%94%E8%AE%B0/assets/image-20200602230358895.png)

#### 逻辑运算符
![](https://github.com/WuPeiqi/go_course/raw/master/day03%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E5%8F%A5/%E7%AC%94%E8%AE%B0/assets/image-20200602230437070.png)

#### <font style="color:rgb(31, 35, 40);">位运算符</font>
在传输文件、web、socket等场景底层原理会用到

#### ![](https://github.com/WuPeiqi/go_course/raw/master/day03%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E5%8F%A5/%E7%AC%94%E8%AE%B0/assets/image-20200602230522054.png)  
 <font style="color:rgb(31, 35, 40);">位运算指的是二进制之间的运算：</font>
```python
// 1.按位进行与运算（全为1，才得1）
r1 := 5 & 99
5  -> 0000101
99 -> 1100011
0000001   -> 1

// 2.按位进行或运算（只要有1，就得1）
r2 := 5 | 99
5  -> 0000101
99 -> 1100011
1100111   -> 2**6 + 2**5 + 2**2 + 2**1 + 2**0 = 64 + 32 + 4 + 2 + 1 = 103

// 3.按位进行异或运算（上下不同，就得1）
r3 := 5 ^ 99
5  -> 0000101
99 -> 1100011
1100110   -> 2**6 + 2**5 + 2**2 + 2**1 = 64 + 32 + 4 + 2 = 102

// 4.按位向左移动
r4 := 5 << 2
5  -> 101
向左移动2位  -> 10100  -> 2**4 + 2**2 = 16 + 4 = 20

// 5.按位向右移动
r5 := 5 >> 1
5  -> 101
向右移动1位  -> 10  -> 2**1 = 2

// 6.比较清除   // 以前面的值为基准，让前面的和后面的值的二进制位进行比较，如果两个位置都是1，则讲前面的值的那个位置置0
r6 := 5 &^ 99
5  -> 0000101
99 -> 1100011
0000100     -> 2**2 = 4
```

#### <font style="color:rgb(31, 35, 40);">赋值运算符</font>
![](https://github.com/WuPeiqi/go_course/raw/master/day03%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E5%8F%A5/%E7%AC%94%E8%AE%B0/assets/image-20200602230552667.png)

```python
age := 19
age = 99

age = age + 9  // age+=9
age = age - 9  // age-=9
age = age * 9  // age*=9
```

#### 运算符的优先级
越上面的优先级越高

> Precedence    Operator
>
>     5             *  /  %  <<  >>  &  &^
>
>     4             +  -  |  ^
>
>     3             ==  !=  <  <=  >  >=
>
>     2             &&
>
>     1             ||
>



### 指针使用
Go 支持 `指针`， 允许在程序中通过 `引用传递` 来传递值和数据结构。

```go
package main

import "fmt"

func main() {
	var num int = 10
	// ptr 指向整数的指针，它存储了 num 的内存地址
	var ptr *int = &num

	fmt.Println("Value of num", num)
	fmt.Println("Address of num", &num)

	fmt.Println("Value of ptr", ptr)
	fmt.Println("Address of ptr", &ptr)

	// *ptr 表示 ptr 所指向的值，即 num 的值
	fmt.Println("New value of num:", *ptr)
}


>>> 输出
Value of num 10
Address of num 0xc000092010
Value of ptr 0xc000092010
Address of ptr 0xc000094018
New value of num: 10
```

