---
title: Pandas的级联操作
comments: true
tags:
  - Python
  - 数据分析
categories:
  - 数据分析
date: 2019-04-30 14:37:18
---


### pandas.concat()级联操作

- 行级联
- 列级联

axis指定是行或列级联操作

<!--more-->

```python
import numpy as np
import pandas as pd
from pandas import Series, DataFrame
```

### 行级联

- pd.concat((a,b), axis=0)

```python
# 生成三种水果3天的价格表
fruits_1 = DataFrame({
    '苹果':[2.5, 4.5, 2.6],
    '橘子': [1.5, 2.5, 2.0],
    '猕猴桃': [3, 4, 3.5]
}, index=[1, 2, 3])
```

```python
# 生成三种水果3天的价格表
fruits_2 = DataFrame({
    '苹果':[2.0, 4.0, 3.5],
    '橙子': [2.0, 3.0, 2.0],
    '猕猴桃': [3, 5, 4]
}, index=[1, 3, 5])
```



```
fruits_1
```



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
    .dataframe tbody tr th {
    vertical-align: top;
}
.dataframe thead th {
    text-align: right;
}
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>苹果</th>
      <th>橘子</th>
      <th>猕猴桃</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2.5</td>
      <td>1.5</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.5</td>
      <td>2.5</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.6</td>
      <td>2.0</td>
      <td>3.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
fruits_2
```



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
    .dataframe tbody tr th {
    vertical-align: top;
}
.dataframe thead th {
    text-align: right;
}
    </style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>苹果</th>
      <th>橙子</th>
      <th>猕猴桃</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>2.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>3.0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3.5</td>
      <td>2.0</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 将上面的两个水果的价格表进行行级联
# 对于不存在的列，可能会出现NaN值，因为两张表根据列标签名对齐
# ignore_index 表示是否重新创建索引
pd.concat((fruits_1, fruits_2), axis=0, ignore_index=True)
```



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
    .dataframe tbody tr th {
    vertical-align: top;
}
.dataframe thead th {
    text-align: right;
}
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>橘子</th>
      <th>橙子</th>
      <th>猕猴桃</th>
      <th>苹果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.5</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.5</td>
      <td>NaN</td>
      <td>4.0</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.0</td>
      <td>NaN</td>
      <td>3.5</td>
      <td>2.6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>3.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
# join 指定连接方式 {outer, inner}
# outer 显示所有的列标签
# inner 只显示两个表中都存在的列标签
pd.concat((fruits_1, fruits_2), axis=0, join='inner', ignore_index=True)
```



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
    .dataframe tbody tr th {
    vertical-align: top;
}
.dataframe thead th {
    text-align: right;
}
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>苹果</th>
      <th>猕猴桃</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2.5</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.5</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.6</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3.5</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# keys 指定每张表数据的一级行标签
pd.concat((fruits_1, fruits_2), axis=0, keys=['1月', '2月'])
```



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
    .dataframe tbody tr th {
    vertical-align: top;
}
.dataframe thead th {
    text-align: right;
}
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>橘子</th>
      <th>橙子</th>
      <th>猕猴桃</th>
      <th>苹果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">1月</th>
      <th>1</th>
      <td>1.5</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.5</td>
      <td>NaN</td>
      <td>4.0</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.0</td>
      <td>NaN</td>
      <td>3.5</td>
      <td>2.6</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">2月</th>
      <th>1</th>
      <td>NaN</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>3.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
#　df的ａpend函数来快速实现行级联操作
fruits_1.append(fruits_2, ignore_index=True)
```



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
    .dataframe tbody tr th {
    vertical-align: top;
}
.dataframe thead th {
    text-align: right;
}
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>橘子</th>
      <th>橙子</th>
      <th>猕猴桃</th>
      <th>苹果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.5</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.5</td>
      <td>NaN</td>
      <td>4.0</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.0</td>
      <td>NaN</td>
      <td>3.5</td>
      <td>2.6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>3.5</td>
    </tr>
  </tbody>
</table>
</div>




### 列级联

- pandas.concat((a, b), axis=1)

列级联时，按行标签对应，如果某一表中不存在某一行，则会出现NaN值

```
display(fruits_1, fruits_2)
```



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
    .dataframe tbody tr th {
    vertical-align: top;
}
.dataframe thead th {
    text-align: right;
}
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>苹果</th>
      <th>橘子</th>
      <th>猕猴桃</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2.5</td>
      <td>1.5</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.5</td>
      <td>2.5</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.6</td>
      <td>2.0</td>
      <td>3.5</td>
    </tr>
  </tbody>
</table>
</div>




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
    .dataframe tbody tr th {
    vertical-align: top;
}
.dataframe thead th {
    text-align: right;
}
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>苹果</th>
      <th>橙子</th>
      <th>猕猴桃</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>2.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>3.0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3.5</td>
      <td>2.0</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 将上面两张表的数据按列级联方式合并，并指定一级列标签，分别是1月和2月
pd.concat((fruits_1, fruits_2), axis=1, keys=['1月', '2月'])
```



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
    .dataframe tbody tr th {
    vertical-align: top;
}
.dataframe thead tr th {
    text-align: left;
}
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">1月</th>
      <th colspan="3" halign="left">2月</th>
    </tr>
    <tr>
      <th></th>
      <th>苹果</th>
      <th>橘子</th>
      <th>猕猴桃</th>
      <th>苹果</th>
      <th>橙子</th>
      <th>猕猴桃</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2.5</td>
      <td>1.5</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.5</td>
      <td>2.5</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.6</td>
      <td>2.0</td>
      <td>3.5</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.5</td>
      <td>2.0</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>


