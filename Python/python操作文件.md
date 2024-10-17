## 基础操作
### 创建文件
```python
f = open("my_cat.txt",mode="w")  # 若⽂件已存在，则覆盖
f.write("name\n") # 写操作
f.write("cat\n")
f.close()  #保存并关闭
```

### 只读模式
```python
f = open("my_cat.txt",mode="r")
print(f.readline())  # 读⼀⾏
print(f.readlines())  # 读取所有行,并返回列表
print('--------------')
data = f.read() # 读所有，剩下的所有
print(data)
f.close()

# 报错编码问题修改为如下格式 
# Windows默认编码是 gbk，如果文件是 utf-8 编码，就会报这个错误
# open(filename, 'r', encoding='utf-8')
```

### 写入模式
```python
f = open("my_cat.txt",mode="a")
f.write("团子 猫")  # 会追加到⽂件尾部
f.close()


# 指定字节类型写入
f.write("cat".encode("gbk"))
```

### 读取文件
```python
f = open("模特联系⽅式.txt",mode="r",encoding='utf-8')
for i in f:
    print(i,end="") # 使用end结尾取消默认打印的空行
```

### 处理图片视频文件
```python
# rb 2进制只读模式
# wb 2进制创建模式，若⽂件已存在，则覆盖旧⽂件
# ab 2进制追加模式，新数据会写到⽂件末尾

# 二进制打开图片
f = open("xiamu.jpg","rb")
for i in f:
    print(i)


# 二进制写入数据
f = open("my_cat.txt","wb")
s = '团子'
print(s.encode("gbk"))
print(s.encode("utf-8"))
f.write(s.encode("utf-8"))

>> b'\xcd\xc5\xd7\xd3'
>> b'\xe5\x9b\xa2\xe5\xad\x90'
```

