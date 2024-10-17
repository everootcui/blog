```python
# 不参数的函数
def sayhi():
    print("hello world")

# 带参数的函数
def calc(x,y):
    res = x*y
    print(res)

sayhi()
calc(2,4)

>>> hello world
>>> 8
```

### 非固定参数
```python
def stu_register(name,age,*args,**kwargs): # *args 会把多传⼊的参数变成⼀个元组形式
    print(name,age,args,kwargs)

stu_register("cui",22,"M","974361381",province="湖北",base="武汉")
```

### 关键参数
```python
def stu_register(name, age, course='PY' ,country='CN'):
    print("----注册学⽣信息------")
    print("姓名:", name)
    print("age:", age)
    print("国籍:", country)
    print("课程:", course)


stu_register("王⼭炮",22,course='PY',country='JP')

# 关键参数必须放在位置参数之后
# stu_register("王⼭炮",course='PY',22,country='JP') 错误用法
```

### **<font style="color:rgb(51,51,51);">返回值return</font>**
```python
#  函数在执行过程中只要遇到return语句，就会停止执行并返回结果
def stu_register(name,age,course,country="CN"):
    print("----注册学⽣信息------")
    print("姓名:",name)
    print("age:",age)
    print("国籍:",country)
    print("课程:",course)
    if age > 22:
        return False
    else:
        return True,age,name
    
registriation_status = stu_register("王⼭炮",21,"python_devops")
print(registriation_status)
if registriation_status:
    print("注册成功")
else:
    print("too old to be a student")

>>> ----注册学⽣信息------
>>> 姓名: 王⼭炮
>>> age: 21
>>> 国籍: CN
>>> 课程: python_devops
>>> (True, 21, '王⼭炮')
>>> 注册成功
```

### **<font style="color:rgb(51,51,51);">传递列表、字典</font>**
```python
d = {"name":"cui","age":23,"hobbie":"skate"}
l = ["Rebeeca","Katrina","Rachel"]
def change_data(info,girls):
 info["hobbie"] = "学习"
 girls.append("XiaoYun")
 
change_data(d,l)
print(f"{d}\n{l}")

>>> {'name': 'cui', 'age': 23, 'hobbie': '学习'}
>>> ['Rebeeca', 'Katrina', 'Rachel', 'XiaoYun']
```



:::info
#python中查看内存地址

<font style="color:rgb(51,51,51);">如图程序只是把d这个字典的内存地址传给了change_data函数，字典里的值(k,v)可以修改，但是字典本身不可以修改(这样设计的目的是为了减少内存浪费，避免copy一份新的dict)</font>

>>> id(d)

4312622856

:::

![](https://cdn.nlark.com/yuque/0/2024/png/34804726/1721273875789-781deb2b-424d-4d4b-978e-fb4fb7bda458.png)

### 内置函数
```python
abs # 求绝对值
all # 返回布尔值，如果有一个值为False则直接返回False
any # 与all相反，只有有一个为True则直接返回True
ascii # 打印ascii码
ord # 打印ascii对应的十进制数字
bin #返回整数的2进制格式
bool # 判断⼀个数据结构是True or False, bool({}) 返回就是False, 因为是空dict
bytearray # 把byte变成 bytearray, 可修改的数组
bytes # bytes("中国","gbk")
callable # 判断⼀个对象是否可调⽤
chr # 返回⼀个数字对应的ascii字符 ， ⽐如chr(90)返回ascii⾥的'Z'
classmethod # ⾯向对象时⽤，现在忽略
compile # py解释器⾃⼰⽤的东⻄，忽略
complex # 求复数，⼀般⼈⽤不到
copyright # 没⽤
credits # 没⽤
delattr # ⾯向对象时⽤，现在忽略
dict # ⽣成⼀个空dict
dir # 返回对象的可调⽤属性
locals # 打印当前程序作用域的所有变量名&变量值
max # 打印列表中的最大值
min # 取最小值
sum # 求和a=[1, 4, 9, 1849, 2025, 25, 36],sum(a) 得3949

```

##### map
```python
l = list(range(5))
print(l)
def calc(x): # 只能定义一个参数
    return x**2
print(calc) # 此时只会打印函数在内存中的地址

m = map(calc,l) # 并没有执行，在循环中才会开始执行
for i in m: # 每循环一次，就把列表的每一个元素扔给calc函数执行
    print(i)

>>> [0, 1, 2, 3, 4]
>>> <function calc at 0x000001C7E3EFE200>
>>> <map object at 0x000001C7E4110D30>
```

##### max
判断字典时以key来判断

```python
numbers = [1, 5, 3, 8, 2]
my_dict = {'a': 1, 'd': 4, 'c': 5} 

max_num = max(numbers)
max_dict = max(my_dict) 
print(max_num,max_dict)

>>> 8 f
```

##### enumerate
枚举打印索引和值

```python
for k,v in enumerate(['cui','jack','tom']):
    print(k,v) 
>>> 0 cui
>>> 1 jack
>>> 2 tom
```

##### round
输出保留小数个数

```python
print(round(3.1415,2)) 

>>> 3.14
```

##### zip
<font style="color:rgb(51,51,51);">把2个或多个列表拼成⼀个</font>

```python
a = [1,2,3]
b = ['a','b']
for i in zip(a,b):
    print(i)

>>> (1, 'a')
>>> (2, 'b')
```

##### filter
把列表的每一个元素交给第一个参数运行，若结果为真则保留这个值

```python
l = list(range(8))
def compare(x):
    if x > 5:
        return x
print(l)
for i in filter(compare,l):
    print(i)

>>> [0, 1, 2, 3, 4, 5, 6, 7]
>>> 6
>>> 7
```















