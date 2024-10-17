**<font style="color:rgb(51,51,51);">random</font>**

```python
random.choice("abcdefg")  # 选择 "abcdefg" 中的一个字符
random.choices(my_list, k=3) # 随机选择多个元素 默认k为1
random.sample("a", 1)  # 从 "abcdefg" 中随机抽取 1 个字符，返回一个列表
random.randint(1, 10)  # 生成 1 到 10 之间的随机整数
random.randrange(1,10) #返回1-10之间的⼀个随机数，不包括10
random.random() #返回⼀个随机浮点数
```

### **<font style="color:rgb(51,51,51);"> string</font>**
```python
string.ascii_lowercase # 包含所有小写字母的字符串
string.ascii_uppercase # 包含所有大写字母的字符串
string.ascii_letters # 包含所有字母（大写和小写）的字符串
string.digits # 包含所有数字字符的字符串
string.punctuation # 打印特殊字符

# 示例用法
random.choice(string.ascii_lowercase)  # 选择小写字母中的一个字符

random.sample(string.ascii_uppercase, 1)  # 从大写字母中随机抽取 1 个字符，返回一个列表
```

### join
```python
a = ["a","b","c","d"]  # 需要为字符串
b = "".join(a)
print(a,b)
>>>> ['a', 'b', 'c', 'd'] abcd
```

### strip
```python
a = " 我可以去掉空格和斜杠 \n  "
b = a.strip()
print(b)
>>>> 我可以去掉空格和斜杠
```

### split
```python
print(a.split("i",2)) # 以i来分割字符串2次 output: ['cu', 'j', 'an']
var.split("市")[0] + "市" # 以'市'来分割字符,取出分割后的列表中的第一个元素，加上'市'
```

###  len
```python
# 解释器⾃带函数,求长度
info = ['3','55']
print(len(info))

>>> 2
```

### re 模糊查询
```python
# re.compile使用正则构建模糊查询
# re.IGNORECASE 忽略大小写
pattern = re.compile(f".*{query}.*", re.IGNORECASE)

# 匹配字符串。如果开头没有匹配项,则返回None
if pattern.match(stock_name)

# 搜索字符串。如果没有找到匹配项，则返回 None
match = pattern.search('abc123def')
```

### index
```python
# 根据索引以切片的方式分割字符为 'xx' '>' 'xx'
s = "apple>banana"
index = s.index('>')
name=s[0:index]
date=s[index+1:]

>>> apple > banana


# 删除最后一个字符
l = [ "hello", "world"]
index = 0
a = l[index]
b = l[index][0:-1]
print(a,b)
>>> hello hell
```

### try
```python
# 使用try语句尝试将字符串"not a number"转换为整数
# 由于这个字符串不是一个有效的数字，所以int()函数会引发一个ValueError异常
# 这个异常被except语句捕获，将result设置为"conversion failed"
try:
    result = int("not a number")
except ValueError:
    result = "conversion failed"
print(result)

>>> conversion failed
```

### isdigit
<font style="color:rgba(0, 0, 0, 0.9);">用于检查字符串是否只包含数字字符</font>

```python
thing = "inputfds123"
if thing.isdigit():
    print("只包含数字")
else:
    print("有其他字符")

>>> 有其他字符
```

### os
<font style="color:rgb(51,51,51);">提供了很多允许你的程序与操作系统直接交互的功能 </font>

```python
import os

得到当前⼯作⽬录，即当前Python脚本⼯作的⽬录路径: os.getcwd()
返回指定⽬录下的所有⽂件和⽬录名: os.listdir()
函数⽤来删除⼀个⽂件: os.remove()
删除多个⽬录：os.removedirs（r"c:\python"）
检验给出的路径是否是⼀个⽂件：os.path.isfile()
检验给出的路径是否是⼀个⽬录：os.path.isdir()
判断是否是绝对路径：os.path.isabs()
检验给出的路径是否真地存:os.path.exists()
返回⼀个路径的⽬录名和⽂件名:os.path.split() 
# e.g 
os.path.split('/home/swaroop/byte/code/poem.txt') 结果：
('/home/swaroop/byte/code', 'poem.txt')

分离扩展名：os.path.splitext() e.g os.path.splitext('/usr/local/test.py')
 结果：('/usr/local/test', '.py')
获取路径名：os.path.dirname()
获得绝对路径: os.path.abspath() 
获取⽂件名：os.path.basename()
运⾏shell命令: os.system()
读取操作系统环境变量HOME的值:os.getenv("HOME")
返回操作系统所有的环境变量： os.environ
设置系统环境变量，仅程序运⾏时有效：os.environ.setdefault('HOME','/home/alex')
给出当前平台使⽤的⾏终⽌符:os.linesep Windows使⽤'\r\n'，Linux and MAC使⽤'\n'
指示你正在使⽤的平台：os.name 对于Windows，它是'nt'，⽽对于Linux/Unix⽤户，它
是'posix'
重命名：os.rename(old,new)
创建多级⽬录：os.makedirs（r"c：\python\test"）
创建单个⽬录：os.mkdir（"test"）
获取⽂件属性：os.stat（file）
修改⽂件权限与时间戳：os.chmod（file）
获取⽂件⼤⼩：os.path.getsize（filename）
结合⽬录名与⽂件名：os.path.join(dir,filename)
改变⼯作⽬录到dirname: os.chdir(dirname)
获取当前终端的⼤⼩: os.get_terminal_size()
杀死进程: os.kill(10884,signal.SIGKILL)
```

### **<font style="color:rgb(51,51,51);">time</font>**
```python
time.localtime([secs]) ：将⼀个时间戳转换为当前时区的struct_time。若secs参数未提供，
则以当前时间为准。

time.gmtime([secs]) ：和localtime()⽅法类似，gmtime()⽅法是将⼀个时间戳转换为UTC时区
(0时区)的struct_time。

time.time() ：返回当前时间的时间戳。

time.mktime(t) ：将⼀个struct_time转化为时间戳。

time.sleep(secs) ：线程推迟指定的时间运⾏,单位为秒。
索引（Index） 属性（Attribute） 值（Values）
0 tm_year（年） ⽐如2011
1 tm_mon（⽉） 1 - 12
2 tm_mday（⽇） 1 - 31
3 tm_hour（时） 0 - 23
4 tm_min（分） 0 - 59
5 tm_sec（秒） 0 - 61
6 tm_wday（weekday） 0 - 6（0表示周⼀）
7 tm_yday（⼀年中的第⼏天） 1 - 366
8 tm_isdst（是否是夏令时） 默认为-1

time.strftime(format[, t]) ：把⼀个代表时间的元组或者struct_time（如由time.localtime()
和time.gmtime()返回）转化为格式化的时间字符串。如果t未指定，将传⼊
time.localtime()
举例： time.strftime("%Y-%m-%d %X", time.localtime())
# 输出 2024-07-22 17:19:39

time.strptime(string[,format]) ：把⼀个格式化时间字符串转化为struct_time
实际上它和strftime()是相反的操作
举例： time.strptime(‘2017-10-3 17:54’,”%Y-%m-%d %H:%M”) 
#输出
time.struct_time(tm_year=2017, tm_mon=10, tm_mday=3, tm_hour=17, tm_min=54,
tm_sec=0, tm_wday=1, tm_yday=276, tm_isdst=-1)
```

<font style="color:rgb(51,51,51);">为了容易记住转换关系，看下图</font>

![](https://cdn.nlark.com/yuque/0/2024/png/34804726/1721640374532-9a6ba345-4bad-4b2e-a32c-3ba3854f03fd.png)

### datetime
```python
datetime.date：表示⽇期的类。常⽤的属性有year, month, day；
datetime.time：表示时间的类。常⽤的属性有hour, minute, second, microsecond；
datetime.datetime：表示⽇期时间。
datetime.timedelta：表示时间间隔，即两个时间点之间的⻓度。
datetime.tzinfo：与时区有关的相关信息。（这⾥不详细充分讨论该类，感兴趣的童鞋可以参考
python⼿册）


# 时间运算 当前时间的前五天，加5小时
d = datetime.datetime.now()
print(d)
print(d + datetime.timedelta(-5,hours=5)) 
print(d.replace(year=2124,month=9))

>>> 2024-07-23 10:36:16.381404
>>> 2024-07-18 15:36:16.381404
>>> 2124-09-23 10:38:05.522174
```

### smtplib
```python
import smtplib
from email.mime.text import MIMEText # 邮件正⽂
from email.header import Header # 邮件头
# 登录邮件服务器
smtp_obj = smtplib.SMTP_SSL("smtp.exmail.qq.com", 465) 
smtp_obj.login("nami@luffycity.com", "xxxx-sd#gf") # 括号中对应的是发件⼈邮箱账号、邮箱密码
#smtp_obj.set_debuglevel(1) # 显示调试信息

# 设置邮件头信息
msg = MIMEText("Hello, ⼩哥哥，约么？800上⻔，新到学⽣妹...", "plain", "utf-8")
msg["From"] = Header("来⾃娜美的问候","utf-8") # 发送者
msg["To"] = Header("有缘⼈","utf-8") # 接收者
msg["Subject"] = Header("娜美的信","utf-8") # 主题
# 发送
smtp_obj.sendmail("nami@luffycity.com", ["alex@luffycity.com",
"317822232@qq.com"], msg.as_string())
```



