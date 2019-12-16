---
title: Series的应用
comments: true
tags:
  - Python
  - 数据分析
categories:
  - 数据分析
date: 2019-04-29 10:46:31
---


### Series的创建

- Series 可以认为是一维数组，但是除了数据之外，还有行索引标签
- 可以使用 list[]创建
- 可以使用ndarray 创建

<!--more-->

```python
import numpy as np
import pandas as pd
from pandas import Series, DataFrame
```

```python
# 创建6位同学的身高信息
# index不指定时，自动按索引位置来创建索引
# name 指定数据集的名称，代表某一特征名或者某一对象的名称
heights = Series([180,185,180,170,175,170],name='height(cm)')
heights
```



```
0    180
1    185
2    180
3    170
4    175
5    170
Name: height(cm), dtype: int64
```



```python
# 创建42位同学的体重的信息
weights = Series(np.random.randint(50,105,size=42), name='weight(kg)')
weights
```



```
0      71
1      67
2      54
3      95
4      94
5     100
6      67
7      90
8      99
9      67
10     60
11    100
12     52
13     84
14     90
15     91
16    101
17     59
18     60
19     59
20     59
21    100
22     56
23     78
24     64
25     61
26     63
27     67
28     83
29     76
30     51
31     65
32     63
33     63
34     60
35     70
36     71
37     63
38     98
39     95
40     73
41     98
Name: weight(kg), dtype: int64
```



```python
# 创建5位同学的Python成绩，分别是disen, jack, mack, rose, jerry
scores = Series(np.random.randint(50,100,size=5),
               index=['disen','jack','mack','rose','jerry'],
               name='Python')
scores
```



```
disen    96
jack     80
mack     94
rose     59
jerry    92
Name: Python, dtype: int64
```



```python
scores_2 = Series({
    'disen':100,
    'jack':90,
    'mack':99,
    'rose':70,
    'jerry':85
}, name='Python')
scores_2
```



```
disen    100
jack      90
mack      99
rose      70
jerry     85
Name: Python, dtype: int64
```



### Series的索引操作

- s[标签名]
- s.loc[标签名]
- s.ilock[标签名]

```python
# 查看disen的成绩
scores['disen']
```



```
96
```



```python
scores[['disen', 'jerry']] # 查看disen和jerry的考试成绩
```



```
disen    96
jerry    92
Name: Python, dtype: int64
```



```python
# 查看前三位同学的成绩
scores['disen':'mack'] # 索引名可以进行切片操作
```



```
disen    96
jack     80
mack     94
Name: Python, dtype: int64
```



```python
scores.loc['disen']
```



```
96
```



```python
scores.loc[['disen', 'jerry']]
```



```
disen    96
jerry    92
Name: Python, dtype: int64
```



```python
# 查看最后两位同学的成绩
scores.iloc[-2:]
```



```
rose     59
jerry    92
Name: Python, dtype: int64
```



### Series的属性

- dtype 数据类型
- shape 数据的形状，如(42, )
- values 数据集，ndarray类型
- index 行索引名的列表，index
- name 数据集的名称

```python
scores.dtype
scores.shape
heights.shape
scores.values
scores.index
```



```
Index(['disen', 'jack', 'mack', 'rose', 'jerry'], dtype='object')
```



```python
# 使用scores.index索引，为这位同学创建它们身高的信息
persons_heights = Series(np.random.randint(155,190, size=5),
                        index=scores.index)
persons_heights
```



```
disen    176
jack     175
mack     162
rose     178
jerry    183
dtype: int64
```



### head()和tail()

```python
weights.head() # 默认显示前5条数据
```



```
0    71
1    67
2    54
3    95
4    94
Name: weight(kg), dtype: int64
```



```python
weights.index
```



```
RangeIndex(start=0, stop=42, step=1)
```



```python
weights.head(n=10) # 显示前10条数据
```



```
0     71
1     67
2     54
3     95
4     94
5    100
6     67
7     90
8     99
9     67
Name: weight(kg), dtype: int64
```



```python
weights.tail() # 显示最后5条数据
```



```
37    63
38    98
39    95
40    73
41    98
Name: weight(kg), dtype: int64
```



```python
weights.tail(n=8) # 显示后8条数据
```



```
34    60
35    70
36    71
37    63
38    98
39    95
40    73
41    98
Name: weight(kg), dtype: int64
```



### NaN值处理

- isnull()
- notnull()

```python
scores
```



```
disen    96
jack     80
mack     94
rose     59
jerry    92
Name: Python, dtype: int64
```



```python
# np.NAN/np.NaN/np.nan
# nan -> not a number
scores['jack'] = np.nan  # scores.iloc[1]
scores
```



```
disen    96.0
jack      NaN
mack     94.0
rose     59.0
jerry    92.0
Name: Python, dtype: float64
```



```python
scores.isnull() #索引对应值变成bool值
```



```
disen    False
jack      True
mack     False
rose     False
jerry    False
Name: Python, dtype: bool
```



```python
# 查出没有成绩的人员姓名
# 根据isnull()结果，将数值为True的索引标签提取出来， 作为scores索引选择数据
scores[scores.isnull()] # == scores['jack']
```



```
jack   NaN
Name: Python, dtype: float64
```



```python
weights.iloc[[1,7,9,11,20,33,38]] = np.nan
weights
```



```
0      71.0
1       NaN
2      54.0
3      95.0
4      94.0
5     100.0
6      67.0
7       NaN
8      99.0
9       NaN
10     60.0
11      NaN
12     52.0
13     84.0
14     90.0
15     91.0
16    101.0
17     59.0
18     60.0
19     59.0
20      NaN
21    100.0
22     56.0
23     78.0
24     64.0
25     61.0
26     63.0
27     67.0
28     83.0
29     76.0
30     51.0
31     65.0
32     63.0
33      NaN
34     60.0
35     70.0
36     71.0
37     63.0
38      NaN
39     95.0
40     73.0
41     98.0
Name: weight(kg), dtype: float64
```



```python
weights[weights.isnull()] # 提取没有值的数据集
```



```
1    NaN
7    NaN
9    NaN
11   NaN
20   NaN
33   NaN
38   NaN
Name: weight(kg), dtype: float64
```



```python
weights[weights.notnull()] # 提取有数值的数据集
```



```
0      71.0
2      54.0
3      95.0
4      94.0
5     100.0
6      67.0
8      99.0
10     60.0
12     52.0
13     84.0
14     90.0
15     91.0
16    101.0
17     59.0
18     60.0
19     59.0
21    100.0
22     56.0
23     78.0
24     64.0
25     61.0
26     63.0
27     67.0
28     83.0
29     76.0
30     51.0
31     65.0
32     63.0
34     60.0
35     70.0
36     71.0
37     63.0
39     95.0
40     73.0
41     98.0
Name: weight(kg), dtype: float64
```



### Series运算

- ndarray的算术运算，完全适合于Series
- 如果对数据中存在NaN值进行预处理，则使用Series本身提供的算术运算的函数

```python
class A:
    def __init__(self, n):
        self.n = n
        
    def __add__(self, value):
        return self.n + value
    
    def __gt__(self, value):
        if isinstance(value, int):
            return self.n > value
        elif isinstance(value, A):
            return self.n > value.n
        
        return False
    
    def __gte__(self,value):
        return self.n >= value
    
    def __str__(self):
        return str(self.n)
```

```python
a = A(10)
a += 100

print(a)

if a > 100:
    print('ok')
```

```
110
ok
```



```python
a2 = A(200)
print(a2)
```

```
200
```



```python
a2 > a 
```



```
True
```



```python
scores += 100
scores
```



```
disen    196.0
jack       NaN
mack     194.0
rose     159.0
jerry    192.0
Name: Python, dtype: float64
```



```python
# add()返回运算后结果
scores_2 = scores.add(100, fill_value=0) # fill_value 指定Nan的填充值
scores_2
```



```
disen    296.0
jack     100.0
mack     294.0
rose     259.0
jerry    292.0
Name: Python, dtype: float64
```



```python
scores.sub(5, fill_value=0) # 减法
```



```
disen    191.0
jack      -5.0
mack     189.0
rose     154.0
jerry    187.0
Name: Python, dtype: float64
```



```python
scores.mul(2, fill_value=0) # 乘法
```



```
disen    392.0
jack       0.0
mack     388.0
rose     318.0
jerry    384.0
Name: Python, dtype: float64
```



```python
scores.div(2, fill_value=0) # 除法
```



```
disen    98.0
jack      0.0
mack     97.0
rose     79.5
jerry    96.0
Name: Python, dtype: float64
```



### Series和ndarray的区别

- Series是一个类似一维数组，而ndarray可以是多维数组
- Series没有广播机制， ndarray有广播机制
- Series的索引操作支持索引标签和.loc[],.iloc[]操作，而ndarray只能使用索引位置
- Series的数据集中可能存在NaN值，并提供相关的运算函数对NaN预处理，而ndarray中不能存在nan值

```python
s2  = Series({
    '政治':80,
    '历史':90,
    '地理':95
},name="文综")
s2
```



```
政治    80
历史    90
地理    95
Name: 文综, dtype: int64
```



```python
s2 += 10
s2
```



```
政治     90
历史    100
地理    105
Name: 文综, dtype: int64
```



```python
s2 = s2.sub(10)
s2
```



```
政治    80
历史    90
地理    95
Name: 文综, dtype: int64
```



```python
# 最大值，最小值，平均值，总数：
# s2.max(),s2.min(),s2.mean(),s2.size
s2.mean()
```



```
98.33333333333333
```



```python
s2.median()
```



```
100.0
```



```python
s2['语文'] = 80 #增加新的索引
s2
```



```
政治    80
历史    90
地理    95
语文    80
Name: 文综, dtype: int64
```



```python
s2.unique() # 去重
```



```
array([80, 90, 95])
```
