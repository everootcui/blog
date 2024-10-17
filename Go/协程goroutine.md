### goroutine介绍
##### 多线程编程缺点
在 java/c++ 中我们要实现并发编程的时候，我们通常需要自己维护一个线程池  
并且需要自己去包装一个又一个的任务，同时需要自己去调度线程执行任务并维护上下文切换  

##### gouroutine
goroutine的概念类似于线程，但 goroutine是由Go的运行时（runtime）调度和管理的。Go程序会智能地将 goroutine 中的任务合理地分配给每个CPU

Go语言之所以被称为现代化的编程语言，就是因为它在语言层面已经 内置了调度和上下文切换的机制 

### 启动一个协程
```go
func main() {
	// goroutine并行测试
	//test()
	// go中开启一个协程 go关键字 方法名()
	go test()
	for i := 0; i < 10; i++ {
		fmt.Println("main", i)
		time.Sleep(time.Microsecond * 100)
	}

	time.Sleep(time.Second)
	fmt.Println("over")
}

func test() {
	for i := 0; i < 10; i++ {
		fmt.Println("test", i)
		time.Sleep(time.Microsecond * 100)
	}
}
```

### WaitGroup
<font style="color:rgb(52,73,94);">主线程退出后所有的协程无论有没有执行完毕都会退出</font>

```go
/*
wg.Add(1)               // 第二步：开启一个协程计数器+1
wg.Done()               // 第三步：协程执行完毕，计数器-1
wg.Wait()               // 第四步：计数器为0时退出
*/

var wg sync.WaitGroup // 第一步：定义一个计数器

func main() {
	wg.Add(2) // 第二步：开启一个协程计数器+1
	go test()
	go test()
	// wg.Wait()发现没有goroutine在使用而我们的wg不为0，那么就会触发异常
	wg.Wait() // 第四步：计数器为0时推出
	//time.Sleep(time.Second)
	fmt.Println("main over")
}

func test() {
	for i := 0; i < 10; i++ {
		fmt.Println(i)
		time.Sleep(100 * time.Microsecond)
	}
	wg.Done() // 第三步：协程执行完毕，计数器-1
}

```

### 开启多个协程
这里的 `sync.WaitGroup` 来实现等待 `goroutine` 执行完毕

执行打印数字顺序不一样是因为 goroutine 是`<font style="color:#DF2A3F;">并发执行</font>`的，而 goroutine 的调度是随机的

```go
var wg sync.WaitGroup

func hello(i int) {
	defer wg.Done()
	fmt.Println("hello goroutine!", i)
}

func main() {
	for i := 1; i < 6; i++ {
		wg.Add(1)
		go hello(i)
	}
	wg.Wait()
}


>>> 输出
hello goroutine! 5
hello goroutine! 1
hello goroutine! 4
hello goroutine! 3
hello goroutine! 2
```

 

### Channel
##### channel类型
```go
// channel是一宗引用类型，声明管道类型格式如下
var 变量 chan 元素类型
var ch1 chan int // 声明一个传递整型的管道
var ch2 chan bool // 声明一个传递布尔型的管道
var ch3 chan []int // 声明一个传递 int 切片的管道
```

##### 创建channel
<font style="color:rgb(52,73,94);">创建 </font>**<font style="color:rgb(52,73,94);">channel </font>**<font style="color:rgb(52,73,94);">的格式如下： </font>`<font style="color:#DF2A3F;">make(chan 元素类型, 容量)</font>`

```go
// 创建一个能存储 10 个 int 类型数据的管道
ch1 := make(chan int, 10)
// 创建一个能存储 4 个 bool 类型数据的管道
ch2 := make(chan bool, 4)
// 创建一个能存储 3 个[]int 切片类型数据的管道
ch3 := make(chan []int, 3)
```

##### channel操作
```go
func main() {
	ch := make(chan int, 5)
	ch <- 6
	ch <- 66
	fmt.Println("send success", ch)
	v1 := <-ch
	fmt.Println(v1)
	v2 := <-ch
	fmt.Println(v2)
}


>>> 输出
send success 0xc000130000
6
66
```

##### 循环从channel取值
```go
func main() {
	ch := make(chan int, 2)
	ch <- 6
	ch <- 66
	close(ch)
	for i := range ch {
		fmt.Println(i)
	}
}
```

### select多路复用
<font style="color:rgb(52,73,94);">select 的使用类似于 switch 语句，它有一系列 case 分支和一个默认的分支</font>

```go
select {
case <-chan1:
// 如果chan1成功读到数据，则进行该case处理语句
case chan2 <- 1:
// 如果成功向chan2写入数据，则进行该case处理语句
default:
// 如果上面都没有成功，则进入default处理流程
}
```

##### select的使用
<font style="color:rgb(52,73,94);">使用 select 语句能提高代码的</font>`<font style="color:#DF2A3F;">可读性</font>`

<font style="color:rgb(52,73,94);">可处理一个或多个 channel 的</font>`<font style="color:#DF2A3F;">发送/接收操作</font>`

<font style="color:rgb(52,73,94);">如果多个 case 同时满足，select 会</font>`<font style="color:#DF2A3F;">随机选择一个</font>`

<font style="color:rgb(52,73,94);">对于没有 case 的 select{}会一直等待，可用于</font>`<font style="color:#DF2A3F;">阻塞 main 函数</font>`

```go
func main() {
	ch_int := make(chan int, 10)
	for i := 0; i < 10; i++ {
		ch_int <- i
	}

	ch_str := make(chan string, 10)
	for i := 0; i < 10; i++ {
		ch_str <- "ccc"
	}

	for {
		select {
		case v := <-ch_int:
			fmt.Println("ch_int数据", v)
			time.Sleep(time.Millisecond * 50)
		case v := <-ch_str:
			fmt.Println("ch_str数据", v)
		default:
			fmt.Println("数据全部取出")
			time.Sleep(time.Millisecond * 50)
			return
		}
	}
}
```

### 互斥锁
<font style="color:rgb(52,73,94);">互斥锁是一种常用的控制共享资源访问的方法，它能够保证同时只有一个</font>`<font style="color:rgb(233,105,0);">goroutine</font>`<font style="color:rgb(52,73,94);">可以访问共享资源</font>

<font style="color:rgb(52,73,94);">Go语言中使用 </font>`<font style="color:rgb(233,105,0);">sync</font>`<font style="color:rgb(233,105,0);"> </font><font style="color:rgb(52,73,94);">包的 </font>`<font style="color:rgb(233,105,0);">Mutex</font>`<font style="color:rgb(233,105,0);"> </font><font style="color:rgb(52,73,94);">类型来实现互斥锁，使用互斥锁来修复上面代码的问题</font>

```go
package main

import (
	"fmt"
	"sync"
)

var x int64
var wg sync.WaitGroup
var lock sync.Mutex

func add() {
	for i := 0; i < 500; i++ {
		lock.Lock() // 加锁
		x = x + 1
		lock.Unlock() // 解锁
	}
	wg.Done()
}
func main() {
	wg.Add(2)
	go add()
	go add()
	wg.Wait()
	fmt.Println(x)
}


>>> 输出
1000
```

