---
title: DataFrame的NaN处理
comments: true
tags:
 - Python
 - 数据分析
categories:
 - 数据分析
date: 2019-04-29 18:47:28
---

```python
import numpy as np
import pandas as pd
from pandas import Series, DataFrame
```

<!--more-->

### isnull()/notnull()

```python
df = DataFrame({
    'sex': np.random.choice(['男', '女'], size=5),
    'height': np.random.randint(155, 180, size=5),
    'weight': np.random.randint(50, 120, size=5),
    'age':    np.random.randint(18, 30, size=5)
})
df
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159</td>
      <td>103</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>女</td>
      <td>161</td>
      <td>114</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>179</td>
      <td>116</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>179</td>
      <td>101</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161</td>
      <td>84</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
    </div>



```python
# 将第二行的height改为None
# 将第三行的weight改为NaN
df.loc[1, 'height'] = None
df.loc[2, 'weight'] = np.NaN
df
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>女</td>
      <td>NaN</td>
      <td>114.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>179.0</td>
      <td>NaN</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>179.0</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
    </div>



### 使用dropna()将带有nan的值的行或列删除

```python
df.dropna() # 默认：删除行数据，当行中存在任意一个NaN值时，则删除该行
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>179.0</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
    </div>



```python
df.dropna(axis=1, how='all') # 按列删除，当某一列所有值都为NaN时，则删除该列
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>女</td>
      <td>NaN</td>
      <td>114.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>179.0</td>
      <td>NaN</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>179.0</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
</div>

```

df_2 = df.copy()
df_2
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>女</td>
      <td>NaN</td>
      <td>114.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>179.0</td>
      <td>NaN</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>179.0</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
</div>



```python
# inplace为True表示会更新原有的数据，且函数返回None
df_2.dropna(axis='index', how='any', inplace=True)
df_2
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>179.0</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
    </div>



### fillna() 填充NaN值

```python
df.fillna(100) # 为NaN值填充100
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>女</td>
      <td>100.0</td>
      <td>114.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>179.0</td>
      <td>100.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>179.0</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
    </div>



```python
# method = {pad, ffill, bfill}
# ffill -> forward fill_value  之前的值填充NaN
# bfill -> back fill_value 之后的值填充NaN
# axis 指定行或者列的方向
df.fillna(method='ffill', axis=0) # 按列的前置填充
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>女</td>
      <td>159.0</td>
      <td>114.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>179.0</td>
      <td>114.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>179.0</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
    </div>



```python
df.fillna(method='bfill', axis=0) # 按列的后置填充
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>女</td>
      <td>179.0</td>
      <td>114.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>179.0</td>
      <td>101.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>179.0</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
    </div>



```python
df.loc[2, 'height'] = None
df
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>女</td>
      <td>NaN</td>
      <td>114.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>NaN</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
    </div>



```python
# limit 作用：在连续出现的NaN填充过程中，限制填充次数
df.fillna(method='ffill', axis=0, limit=1)
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>女</td>
      <td>159.0</td>
      <td>114.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>NaN</td>
      <td>114.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>NaN</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
    </div>



### isnull()和notnull()在DataFrame中的应用

```python
df.isnull().any(axis=0) # 查看哪些列存在NaN值
```



```
sex       False
height     True
weight     True
age       False
dtype: bool
```



```python
# 查看存在NaN值的列数据
df.loc[:, df.isnull().any(axis=0)]
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
      <th>height</th>
      <th>weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>159.0</td>
      <td>103.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>114.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>101.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>161.0</td>
      <td>84.0</td>
    </tr>
  </tbody>
</table>
    </div>



```python
df.isnull().any(axis=1) # 查看哪些行存在NaN值
```



```
0    False
1     True
2     True
3     True
4    False
dtype: bool
```



```python
# 查看存在NaN值的行数据
df[df.isnull().any(axis=1)]
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>女</td>
      <td>NaN</td>
      <td>114.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>NaN</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 删除重复行
df.loc[1] = df.loc[0]
df
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>NaN</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
</div>



```python
# keep = {'last', 'first'} default first
# first 保留重复数据的第一行
# last 保留重复数据的最后一行
df.drop_duplicates(keep='first')
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>NaN</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
</div>



```python
df.drop_duplicates(keep='last')
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
      <th>sex</th>
      <th>height</th>
      <th>weight</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>男</td>
      <td>159.0</td>
      <td>103.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>2</th>
      <td>女</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>女</td>
      <td>NaN</td>
      <td>101.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>161.0</td>
      <td>84.0</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
</div>

