---
title: ndarray的聚合操作
comments: true
tags:
  - Python
  - 数据分析
categories:
  - 数据分析
date: 2019-04-28 15:41:33
---


### 最大值、最小值和平均值

```python
import numpy as np
```

```python
# 六个城市的五种水果的价格
prices = np.round(np.random.uniform(1, 50, size=(6, 5)),1)
prices
```

<!--more-->

```
array([[17.8, 33.9, 21.6, 37.9, 29.5],
       [21. , 35.8,  1.3,  3.3, 11.1],
       [42. , 15.3, 23.2, 13. , 18.9],
       [ 2. , 10.4, 49.2,  1.9, 27.4],
       [33.4, 38.5, 37.4, 49.9,  2.7],
       [44.2,  7.9, 20.3, 10. , 47.9]])
```



#### 分别查看每个城市的水果的总价、平均、最高、最低

```python
prices.sum(axis=1)
```



```
array([140.7,  72.5, 112.4,  90.9, 161.9, 130.3])
```



```python
prices.mean(axis=1)
```



```
array([28.14, 14.5 , 22.48, 18.18, 32.38, 26.06])
```



```python
prices.min(axis=1)
```



```
array([17.8,  1.3, 13. ,  1.9,  2.7,  7.9])
```



#### 查看每种水果的最高、最低价格

```python
prices.max(axis=0)
```



```
array([44.2, 38.5, 49.2, 49.9, 47.9])
```



```python
prices.min(axis=0)
```



```
array([2. , 7.9, 1.3, 1.9, 2.7])
```



### 读取excel的文件，pandas库

```python
import pandas as pd
```

```python
heights = pd.read_excel('/home/pighui/Desktop/heights.xlsx')
heights
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
      <td>180</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>185</td>
      <td>75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>155</td>
      <td>50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>165</td>
      <td>65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>190</td>
      <td>110</td>
    </tr>
    <tr>
      <th>5</th>
      <td>186</td>
      <td>105</td>
    </tr>
  </tbody>
</table>
    </div>



```python
heights.values #ndarry
```



```
array([[180,  70],
       [185,  75],
       [155,  50],
       [165,  65],
       [190, 110],
       [186, 105]])
```



```python
heights.values.mean(axis=0)
```



```
array([176.83333333,  79.16666667])
```
