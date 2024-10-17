#### 需求：需要拿到红框内的value值，并且根据出现次数进行排序
![](https://cdn.nlark.com/yuque/0/2024/png/34804726/1723454222319-88278e2b-de8d-4a13-ae19-65b0616b2d0e.png)

```python
# 处理过程：由于该文件是csv格式的，且编码也是gbk导致一系列问题，所以本次将该列复制重新创建了一个xlsx表并粘贴至第一列

from openpyxl import load_workbook
from collections import Counter
import json

wb = load_workbook("告警id.xlsx")

sheet_name = wb.sheetnames[0]
sheet = wb[sheet_name]
id = []
for row in sheet.iter_rows(min_row=2, max_row=1527, max_col=1):
    for cell in row:
        # 将单引号替换为双引号
        cell_value_str = str(cell.value).replace("'", "\"")
        data = json.loads(cell_value_str)
        values = data[0]['value']
        id.append(values)
counter = Counter(id)
sorted_counter = counter.most_common()
for id1,count in sorted_counter:
    print(f"特性id为{id1}，出现了{count}次")


>>> 输出
特性id为874683，出现了905次
特性id为11986，出现了229次
特性id为874682，出现了181次
特性id为15076，出现了101次
特性id为872877，出现了49次
特性id为1208，出现了28次
特性id为14802，出现了17次
特性id为13977，出现了12次
特性id为11985，出现了3次
特性id为987432，出现了1次
```





