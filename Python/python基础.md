### **<font style="color:rgb(51,51,51);">字符串常用操作</font>**
```python
a = "cuijian"
print(a.center(20,"-")) # output: ------cuijian-------
print(a.count("i"))      # output: 2
print(a.endswith("n"))    # True(判断结尾)
print(a.startswith("C"))   # False(判断开头)
print(a.find("i"))   # 字符查找,未找到返回-1,找到了返回字符索引
print("22".isdigit())  # 判断是否为整数 Ture

name = ["tuan","cat","dog","mao"]
print("-".join(name))  # 拼接字符串 output: tuan-cat-dog-mao

print(a.replace("i","6",1))  # 替换字符串一次 output: cu6jian
```

### 字符串
```python
>>> s = "Hello, my name is Alex,golden king."
>>> s[3:6]  # 顾头不顾尾
'lo,'
>>> s[0:5] 
'Hello'
```

### 列表的增删改查
在不知道⼀个元素在列表哪个位置 的情况 下，如何修改：

1. 先判断 在不在列表⾥， item in list

2. 取索引，item_index = names.index("eva")

3. 去修改， names[item_index] = “铁蛋”

```python
# 增加
>>> names = ['alex', 'jack'] 
>>> names.append("cat")

# 插入
>>> names.insert(2,"tuanzi") 
>>> names
['alex', 'jack', 'tuanzi', 'cat']

# 合并
>>> n2 = ["狗蛋","绿⽑","鸡头"]
>>> names.extend(n2)
>>> names
['alex', 'jack', 'tuanzi', 'cat', '狗蛋', '绿⽑', '鸡头']

# 删除
>>> names
['alex', 'jack', 'tuanzi', 'cat', '狗蛋', '绿⽑', '鸡头']
>>> del names[6] # 删除第六个值


>>> names.pop()  # pop默认删除最后⼀个元素并返回被删除的值
'绿⽑'

>>> names.remove("cat") # remove删除第⼀个找到的eva值

# clear清空列表
>>> n2    
['狗蛋', '绿⽑', '鸡头']
>>> n2.clear()
>>> n2
[]

# 修改
>>> names[0] = "路飞" 
>>> names[-1] = "索隆" 
>>> names
['路飞', 'jack', '索隆']

# 查询
>>> names.index("路飞")  #返回从左开始匹配到的第⼀个路飞的索引
0
>>>
>>> names.count("路飞")  #返回路飞的个数
1


# 切片
>>> a = "hsl>25"
>>> num = a.split('>')[:2]  # 使用切片获取前两个元素
>>> ['hsl', '25']

# 步长
names[start:end:step] #step 默认是1
>>> a
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> a[0:7:2] # 设置步⻓为2
[0, 2, 4, 6]

# 排序&反转
>>> a = [83,4,2,4,6,19,33,21]
>>> a.sort()
>>> a
[2, 4, 4, 6, 19, 21, 33,  83]

>>> a.reverse() # 反转
[83, 33, 21, 19, 6, 4, 4, 2]

```

### 字典增删改查
```python
dic.keys() #返回⼀个包含字典所有KEY的列表；
dic.values() #返回⼀个包含字典所有value的列表；
dic.items() #返回⼀个包含所有（键，值）元组的列表；


# k,v 2个变量 
>>> for k,v in dic.items():
... print(k,v)
...
Alex [23, 'CEO', 66000]
⿊姑娘 [24, '⾏政', 4000]
佩奇 [26, '讲师', 40000]

for k in info:
 print(k,info[k])


# 效率最快的循环取值方法
dic = {
    "Alex":[23,"CEO",66000],
    "⿊姑娘":[24,"⾏政",4000],
    "佩奇":[26,"讲师",40000]
}
for i in dic:
    print(i,dic[i])
```



