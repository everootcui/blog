### openpyxl模块
会在当前目录创建一个excle，且sheet名为cuijian

```python
from openpyxl import Workbook
import datetime
wb = Workbook() # create excel file in ARM
sheet = wb.active # 获取激活的工作表
sheet.title = "cuijian"
print(sheet.title)
sheet["c6"] = "black_girl"
sheet["d6"] = "172,48"
sheet.append(["jack","175","49"]) # 追加写入
sheet['b6'] = datetime.datetime.now().strftime("%Y-%m-%d")
wb.save("test.xlsx") # 保存文件名为
```

![](https://cdn.nlark.com/yuque/0/2024/png/34804726/1721704205645-bc8861b4-7d96-4ad9-8878-312d8e60ae20.png)

打开现有文件

```python
# 打开已有文件
from openpyxl import load_workbook
wb = load_workbook("test.xlsx",data_only=True) # 为真时读取的是公式计算值

# sheet = wb.active # 直接选择第一个工作表

print(wb.sheetnames) # 获取工作簿中的所有工作表名称
sheet_name = wb.sheetnames[0] # 第一个工作表的名称

sheet = wb[sheet_name]
cell_value = sheet["B6"]
value = sheet["B6"].value # 获取单元格 B6 的值
print(f'{cell_value}\n{value}')

>>> ['cuijian']
>>> <Cell 'cuijian'.B6>
>>> 2024-07-23
```

遍历表数据

```python
# 打开已有文件
from openpyxl import load_workbook
wb = load_workbook("test.xlsx")

print(wb.sheetnames)
sheet_name = wb.sheetnames[0]
sheet = wb[sheet_name]
for row in sheet:
    for cell in row:
        print(cell.value,end=',')
    print()

>>> ['cuijian']
>>> None,None,None,None,
>>> None,None,None,None,
>>> None,None,None,None,
>>> None,None,None,None,
>>> None,None,None,None,
>>> None,2024-07-23,black_girl,172,48,
>>> jack,175,49,None,>>> 
```

按行&列遍历数据

```python
from openpyxl import load_workbook
wb = load_workbook("test.xlsx")

sheet_name = wb.sheetnames[0]
sheet = wb[sheet_name]
# 从第5行开始至第7行，每行打印3列
for row in sheet.iter_rows(min_row=5,max_row=7,max_col=3):
    for cell in row:
        print(cell.value,end=",")
    print()

>>> None,None,None,
>>> None,2024-07-23,black_girl,
>>> jack,175,49,>>> 
```

遍历指定几列的数据

```python
from openpyxl import load_workbook
wb = load_workbook("test.xlsx")

sheet_name = wb.sheetnames[0]
sheet = wb[sheet_name]
# 打印第一列到第三列的数据
for col in sheet.iter_cols(min_col=1, max_col=3):
    for i in col:
        print(i.value,end=',')
    print()
```

删除工作表

```python
# ⽅式⼀
wb.remove(sheet)

# ⽅式⼆
del wb[sheet]
```



