### <font style="color:rgb(51,51,51);">模块导入&调用</font>
模块一旦被调用，就相当于执行了另外一个py文件中的源码

```python
import module_a #导⼊
from module import xx # 导⼊某个模块下的某个⽅法 or ⼦模块
from module.xx.xx import xx as rename #导⼊后⼀个⽅法后重命令
from module.xx.xx import * #导⼊⼀个模块下的所有⽅法，不建议使⽤
module_a.xxx #调⽤
```

### 模块查找路径
```python
import my_mod # 调用同级目录中的自定义模块
my_mod.sayhi() # 函数名

import sys 
print(sys.path) # 模块查找的路径
 
import os
print(__file__) # 打印当前文件路径
print(os.path.dirname(__file__))  # 打印当前文件所在目录路径
```

### **<font style="color:rgb(51,51,51);">第三方开源模块安装</font>**
```python
# python开源模块库
https://pypi.python.org/pypi 

# 下载方式
1. pip3 install 模块名
默认安装目录/your_python_install_path/3.6/lib/python3.6/site-packages
# 若安装满可以使用豆瓣源下载
pip install -i http://pypi.douban.com/simple/ xxx --trusted-host
pypi.douban.com #xxx是模块名

2. 编译源码 
python setup.py build 安装源码 
python setup.py install
```

### 不同目录下的模块调用
![](https://cdn.nlark.com/yuque/0/2024/png/34804726/1721637833021-9d499e4d-63f6-4766-b28e-4535df18165d.png)

使用a/a2/a_moudule.py文件调用b/b2/b2_mod

```python
import sys
import os

base_dir = os.path.dirname(os.path.dirname(os.path.dirname(__file__)))
print(base_dir) # 取到路径
sys.path.append(base_dir)
from b.b2 import b2_mod
```











