### flag包
`<font style="color:rgb(52,73,94);">flag.Args()</font>`<font style="color:rgb(52,73,94);"> //返回命令行参数后的其他参数，以[]string类型 </font>

`<font style="color:rgb(52,73,94);">flag.NArg()</font>`<font style="color:rgb(52,73,94);"> //返回命令行参数后的其他参数个数 </font>

`<font style="color:rgb(52,73,94);">flag.NFlag()</font>`<font style="color:rgb(52,73,94);"> //返回使用的命令行参数个数</font>

```go
package main

import (
	"flag"
	"fmt"
)

/*
// 1、查看帮助
go run main.go --help

// 2、非flag 命令行传参
>go run main.go zs
[zs]

// 3、flag命令行传参
>go run main.go -name "zs" 1 2
zs
[1 2]
*/
func main() {
	var name string
	/* go run main.go --help
	-name string
	      姓名 (default "zhangsan")
	*/
	flag.StringVar(&name, "name", "zhangsan", "姓名")
	/*
		&name : 传递是变量的指针类型，传入的数据赋值给他了
		"name"：run main.go -name "zs" 命令行里的名字
		"zhangsan" ： 默认值，不传递就是他
		"姓名"   --help中的提示信息
	*/
	flag.Parse()
	// 1、获取指定参数
	fmt.Println(name)

	// 2、flag.Args()：获取其他参数
	fmt.Println(flag.Args())
}


>>> 输出
go run .\main.go -name "cuijian" aaa
cuijian
[aaa]

```



### ntp-http
#### 服务端
```go
package main

import (
	"encoding/json"
	"fmt"
	"io/ioutil"
	"net/http"
)

func main() {
	http.HandleFunc("/req/get", dealGetHandler)
	http.HandleFunc("/req/post", dealPostHandler)
	http.ListenAndServe(":8005", nil)
}

/*
		处理get请求
	  - 1)解析请求的数据（获取某一个商品，你需要把商品Id信息携带给后端）
	    http.Request：解析url中的数据或者post请求中body的数据
	  - 2)响应数据（把从数据库读取的数据，给返回给浏览器或者请求方）
	    http.ResponseWriter: 本质是一个interface接口，定义三个方法，进行返回数据
*/
func dealGetHandler(w http.ResponseWriter, r *http.Request) {
	query := r.URL.Query() // 返回 map[string][]string
	if len(query["name"]) > 0 {
		name := query["name"][0] // 通过字典下标取值
		fmt.Println("通过字典下标取值", name)
	}
	name2 := query.Get("name") // 使用get方式，如果没有值会返回空字符串
	fmt.Println("通过get方式获取", name2)
	fmt.Println(query)

	// 响应数据，假设拿到了name=cui，从数据库取出来cui的信息
	type Info struct {
		Name     string
		Password string
		Age      int
	}
	// 假设如下是数据库中取的数据
	user := Info{
		Name:     "cui",
		Password: "123456",
		Age:      24,
	}
	json.NewEncoder(w).Encode(user) // 页面返回json数据
}

type Info struct {
	Name     string `json:"name"`
	Password string `json:"password"`
}

// 处理post请求,和get请求差不多
func dealPostHandler(w http.ResponseWriter, r *http.Request) { // 处理POST请求
	bodyContent, _ := ioutil.ReadAll(r.Body) // 请求体数据
	var d Info
	json.Unmarshal(bodyContent, &d)
	fmt.Println("获取的数据为:", d)
	w.Write([]byte("hello world Post"))
}
```

浏览器测试发送get请求

![](https://cdn.nlark.com/yuque/0/2024/png/34804726/1728721611389-a719c67c-f868-4fe2-bfa7-ee7674e58f7f.png)

#### 客户端
##### 测试发送`<font style="color:#DF2A3F;">get</font>`请求
```go
func main() {
	//// 1、直接通过url拼接处url字符串
	apiUrl := "http://127.0.0.1:8005/req/get"

	// 2、通过url进行解析
	data := url.Values{}
	data.Set("name", "zhangsan")
	u, _ := url.ParseRequestURI(apiUrl)
	u.RawQuery = data.Encode()
	fmt.Println(u.String())

	resp, err := http.Get(u.String())
	if err != nil {
		fmt.Println(err)
	}
	body, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(body))
}
```

服务端接收的数据

![](https://cdn.nlark.com/yuque/0/2024/png/34804726/1728721928351-fb9a3569-beb3-49fc-b716-4438b6123719.png)

客户端返回的数据

![](https://cdn.nlark.com/yuque/0/2024/png/34804726/1728721915220-899a6e95-b663-44a8-b660-4667395c2ec5.png)

##### 测试发送`<font style="color:#DF2A3F;">post</font>`请求
```go
func main() {
	url := "http://127.0.0.1:8005/req/post"
	// 模拟form表单提交数据 contentType := "application/x-www-form-urlencoded"
	// 传json数据： json contentType := "application/json"
	contentType := "application/json"
	data := `{
		"name": "root",
		"password": "123456"
	}`
	resp, _ := http.Post(url, contentType, strings.NewReader(data))
	b, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(b))
}
```

服务端接收的数据

![](https://cdn.nlark.com/yuque/0/2024/png/34804726/1728721702567-90389da5-17be-4054-8901-36f6b78581ec.png)

客户端返回的数据

![](https://cdn.nlark.com/yuque/0/2024/png/34804726/1728721727673-39c45cb6-7b18-491f-b6a7-b3124a072161.png)

