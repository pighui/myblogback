---
title: DataFrame的应用
comments: true
tags:
  - Python
  - 数据分析
categories:
  - 数据分析
date: 2019-04-29 16:47:19
---


DataFrame 带有行和列的标签以及数据的二维表(二维数组)，在Pandas中提供所有函数来读取csv、excel、text以及数据库的数据，结果都是DataFrame对象。

DataFrame由多个Series组成，每个Series代表一列或一行

<!--more-->

```python
import numpy as np
import pandas as pd
from pandas import Series, DataFrame
```

```python
# 创建10位同学的Python，H5和Testing三门课程的成绩表
names = ['Disen','Jack','Rose','Mack','Jerry','Peter','Tom','Alice','Tony','Kobe']
scores = np.random.randint(100, size=(10, 3))

# index 行索引标签
# columns 列索引标签
df = DataFrame(scores, index=names, columns=['Python','H5','Testing'])
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
      <th>Python</th>
      <th>H5</th>
      <th>Testing</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Disen</th>
      <td>98</td>
      <td>72</td>
      <td>90</td>
    </tr>
    <tr>
      <th>Jack</th>
      <td>64</td>
      <td>29</td>
      <td>5</td>
    </tr>
    <tr>
      <th>Rose</th>
      <td>90</td>
      <td>18</td>
      <td>47</td>
    </tr>
    <tr>
      <th>Mack</th>
      <td>6</td>
      <td>24</td>
      <td>7</td>
    </tr>
    <tr>
      <th>Jerry</th>
      <td>51</td>
      <td>50</td>
      <td>14</td>
    </tr>
    <tr>
      <th>Peter</th>
      <td>38</td>
      <td>85</td>
      <td>37</td>
    </tr>
    <tr>
      <th>Tom</th>
      <td>83</td>
      <td>27</td>
      <td>88</td>
    </tr>
    <tr>
      <th>Alice</th>
      <td>31</td>
      <td>27</td>
      <td>37</td>
    </tr>
    <tr>
      <th>Tony</th>
      <td>59</td>
      <td>74</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Kobe</th>
      <td>25</td>
      <td>24</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
    </div>


```

```

```python
# 以字典的方式创建DataFrame，类似于Series的字典创建方式
# key表示列的名称（标签）
df2 = DataFrame({
    '语文':[100,90,20,30,55],
    '数学':[80,88,76,65,60],
    '英语':[81,77,54,92,87]
})
df2
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
      <th>语文</th>
      <th>数学</th>
      <th>英语</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100</td>
      <td>80</td>
      <td>81</td>
    </tr>
    <tr>
      <th>1</th>
      <td>90</td>
      <td>88</td>
      <td>77</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>76</td>
      <td>54</td>
    </tr>
    <tr>
      <th>3</th>
      <td>30</td>
      <td>65</td>
      <td>92</td>
    </tr>
    <tr>
      <th>4</th>
      <td>55</td>
      <td>60</td>
      <td>87</td>
    </tr>
  </tbody>
</table>
    </div>

