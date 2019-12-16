---
title: Pandas的透视表与交叉表
comments: true
tags:
  - Python
  - 数据分析
categories:
  - 数据分析
date: 2019-05-06 19:19:09
---


### 什么是透视表

- 透视表针对特定的列进行分组同时聚合计算，相当于groupby()与聚合函数的组合使用
- 透视表注重的是数据排列与聚合计算，默认使用平均值做聚合计算

<!--more-->

```python
import numpy as np
import pandas as pd
from pandas import Series, DataFrame
```

### 行透视表

- df.pivot_table(index=)

```python
df = DataFrame({
    'sex': np.random.choice(['男', '女'], size=10),
    'smoke': np.random.choice(['Yes', 'No'], size=10),
    'height(cm)': np.random.randint(160, 200, size=10),
    'weight(kg)': np.random.randint(55, 100, size=10),
    'size(尺)': np.random.randint(30, 40, size=10)
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
      <th>smoke</th>
      <th>height(cm)</th>
      <th>weight(kg)</th>
      <th>size(尺)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>男</td>
      <td>Yes</td>
      <td>184</td>
      <td>93</td>
      <td>35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>女</td>
      <td>No</td>
      <td>182</td>
      <td>62</td>
      <td>33</td>
    </tr>
    <tr>
      <th>2</th>
      <td>男</td>
      <td>No</td>
      <td>171</td>
      <td>55</td>
      <td>36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>男</td>
      <td>No</td>
      <td>199</td>
      <td>75</td>
      <td>39</td>
    </tr>
    <tr>
      <th>4</th>
      <td>男</td>
      <td>Yes</td>
      <td>186</td>
      <td>75</td>
      <td>36</td>
    </tr>
    <tr>
      <th>5</th>
      <td>男</td>
      <td>No</td>
      <td>180</td>
      <td>81</td>
      <td>30</td>
    </tr>
    <tr>
      <th>6</th>
      <td>女</td>
      <td>No</td>
      <td>178</td>
      <td>69</td>
      <td>31</td>
    </tr>
    <tr>
      <th>7</th>
      <td>男</td>
      <td>No</td>
      <td>186</td>
      <td>74</td>
      <td>38</td>
    </tr>
    <tr>
      <th>8</th>
      <td>女</td>
      <td>Yes</td>
      <td>194</td>
      <td>71</td>
      <td>36</td>
    </tr>
    <tr>
      <th>9</th>
      <td>男</td>
      <td>Yes</td>
      <td>182</td>
      <td>56</td>
      <td>38</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 按是否抽烟、计算平均身高、体重、腰围
df.groupby('smoke').mean()
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
      <th>height(cm)</th>
      <th>weight(kg)</th>
      <th>size(尺)</th>
    </tr>
    <tr>
      <th>smoke</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>No</th>
      <td>182.666667</td>
      <td>69.333333</td>
      <td>34.50</td>
    </tr>
    <tr>
      <th>Yes</th>
      <td>186.500000</td>
      <td>73.750000</td>
      <td>36.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_table(index='smoke')
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
      <th>height(cm)</th>
      <th>size(尺)</th>
      <th>weight(kg)</th>
    </tr>
    <tr>
      <th>smoke</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>No</th>
      <td>182.666667</td>
      <td>34.50</td>
      <td>69.333333</td>
    </tr>
    <tr>
      <th>Yes</th>
      <td>186.500000</td>
      <td>36.25</td>
      <td>73.750000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 查看是否吸烟和不同的性别的平均的身高、体重、腰围的数据
df.groupby(['smoke', 'sex']).mean()
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
      <th>height(cm)</th>
      <th>weight(kg)</th>
      <th>size(尺)</th>
    </tr>
    <tr>
      <th>smoke</th>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">No</th>
      <th>女</th>
      <td>180.0</td>
      <td>65.500000</td>
      <td>32.000000</td>
    </tr>
    <tr>
      <th>男</th>
      <td>184.0</td>
      <td>71.250000</td>
      <td>35.750000</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Yes</th>
      <th>女</th>
      <td>194.0</td>
      <td>71.000000</td>
      <td>36.000000</td>
    </tr>
    <tr>
      <th>男</th>
      <td>184.0</td>
      <td>74.666667</td>
      <td>36.333333</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_table(index=['smoke', 'sex'], aggfunc='max')
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
      <th>height(cm)</th>
      <th>size(尺)</th>
      <th>weight(kg)</th>
    </tr>
    <tr>
      <th>smoke</th>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">No</th>
      <th>女</th>
      <td>182</td>
      <td>33</td>
      <td>69</td>
    </tr>
    <tr>
      <th>男</th>
      <td>199</td>
      <td>39</td>
      <td>81</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Yes</th>
      <th>女</th>
      <td>194</td>
      <td>36</td>
      <td>71</td>
    </tr>
    <tr>
      <th>男</th>
      <td>186</td>
      <td>38</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>




### 列透视表

- df.pivot_table(columns=)

```python
df.pivot_table(columns='smoke')
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
      <th>smoke</th>
      <th>No</th>
      <th>Yes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>height(cm)</th>
      <td>182.666667</td>
      <td>186.50</td>
    </tr>
    <tr>
      <th>size(尺)</th>
      <td>34.500000</td>
      <td>36.25</td>
    </tr>
    <tr>
      <th>weight(kg)</th>
      <td>69.333333</td>
      <td>73.75</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby(['smoke']).mean().transpose()
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
      <th>smoke</th>
      <th>No</th>
      <th>Yes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>height(cm)</th>
      <td>182.666667</td>
      <td>186.50</td>
    </tr>
    <tr>
      <th>weight(kg)</th>
      <td>69.333333</td>
      <td>73.75</td>
    </tr>
    <tr>
      <th>size(尺)</th>
      <td>34.500000</td>
      <td>36.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_table(columns=['smoke', 'sex'])
```



```
            smoke  sex
height(cm)  No     女      180.000000
                   男      184.000000
            Yes    女      194.000000
                   男      184.000000
weight(kg)  No     女       65.500000
                   男       71.250000
            Yes    女       71.000000
                   男       74.666667
size(尺)     No     女       32.000000
                   男       35.750000
            Yes    女       36.000000
                   男       36.333333
dtype: float64
```



### 行列同时透视

- df.pivot_table(index, columns)

```python
df.pivot_table(index='sex', columns='smoke', aggfunc='min')  # aggfunc指定聚合函数
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
.dataframe thead tr:last-of-type th {
    text-align: right;
}
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">height(cm)</th>
      <th colspan="2" halign="left">size(尺)</th>
      <th colspan="2" halign="left">weight(kg)</th>
    </tr>
    <tr>
      <th>smoke</th>
      <th>No</th>
      <th>Yes</th>
      <th>No</th>
      <th>Yes</th>
      <th>No</th>
      <th>Yes</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>女</th>
      <td>178</td>
      <td>194</td>
      <td>31</td>
      <td>36</td>
      <td>62</td>
      <td>71</td>
    </tr>
    <tr>
      <th>男</th>
      <td>171</td>
      <td>182</td>
      <td>30</td>
      <td>35</td>
      <td>55</td>
      <td>56</td>
    </tr>
  </tbody>
</table>
</div>




### 交叉表

- pd.cross(index, columns) 通过不同表的特征数据进行交叉显示
- 是一种特殊的透视表,聚合函数只是用来统计数量

```python
pd.crosstab(df['sex'],df['smoke'])
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
      <th>smoke</th>
      <th>No</th>
      <th>Yes</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>女</th>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>男</th>
      <td>4</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# margins=True 小计
pd.crosstab(df['sex'],df['smoke'], margins=True, margins_name='小计')
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
      <th>smoke</th>
      <th>No</th>
      <th>Yes</th>
      <th>小计</th>
    </tr>
    <tr>
      <th>sex</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>女</th>
      <td>2</td>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>男</th>
      <td>4</td>
      <td>3</td>
      <td>7</td>
    </tr>
    <tr>
      <th>小计</th>
      <td>6</td>
      <td>4</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>


