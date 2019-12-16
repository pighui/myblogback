---
title: DataFrame的运算
comments: true
tags:
  - Python
  - 数据分析
categories:
  - 数据分析
date: 2019-04-29 14:47:09
---


```python
import numpy as np
import pandas as pd
from pandas import Series, DataFrame
```

<!--more-->

### DataFrame运算

- add()
- sub()
- mul() * 乘法
- div() / 除法
- floordiv() // 整除
- mod() % 取余
- pow() ^ 次方(幂)

使用运算的函数，可以与处理NaN值

```python
# 14天的四种蔬菜的价格表
datas = np.random.randint(1, 10, size=(14, 4))
columns = ('白萝卜', '西红柿', '黄瓜', '白菜')
days = np.arange(1, 15, step=1)

df = DataFrame(datas,days,columns)
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
      <th>白萝卜</th>
      <th>西红柿</th>
      <th>黄瓜</th>
      <th>白菜</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>9</td>
      <td>7</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>6</td>
      <td>5</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>7</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8</td>
      <td>4</td>
      <td>7</td>
      <td>9</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>3</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>9</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>6</td>
      <td>6</td>
      <td>3</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>8</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3</td>
      <td>7</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2</td>
      <td>5</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>3</td>
      <td>7</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>9</td>
      <td>4</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>8</td>
      <td>3</td>
      <td>7</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
    </div>



```python
# 将所有蔬菜的价格全部上调1.5倍
df *= 2.5
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
      <th>白萝卜</th>
      <th>西红柿</th>
      <th>黄瓜</th>
      <th>白菜</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>12.5</td>
      <td>22.5</td>
      <td>17.5</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5.0</td>
      <td>15.0</td>
      <td>12.5</td>
      <td>17.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10.0</td>
      <td>17.5</td>
      <td>12.5</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20.0</td>
      <td>10.0</td>
      <td>17.5</td>
      <td>22.5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5.0</td>
      <td>7.5</td>
      <td>5.0</td>
      <td>7.5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>15.0</td>
      <td>22.5</td>
      <td>12.5</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>5.0</td>
      <td>15.0</td>
      <td>15.0</td>
      <td>7.5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>20.0</td>
      <td>20.0</td>
      <td>5.0</td>
      <td>7.5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7.5</td>
      <td>17.5</td>
      <td>12.5</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>5.0</td>
      <td>12.5</td>
      <td>10.0</td>
      <td>12.5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7.5</td>
      <td>17.5</td>
      <td>7.5</td>
      <td>12.5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>22.5</td>
      <td>10.0</td>
      <td>2.5</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>5.0</td>
      <td>7.5</td>
      <td>10.0</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>14</th>
      <td>20.0</td>
      <td>7.5</td>
      <td>17.5</td>
      <td>17.5</td>
    </tr>
  </tbody>
</table>
    </div>



```python
# 将前五天的所有的蔬菜价格打8.8折
df[:5] *= 0.88
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
      <th>白萝卜</th>
      <th>西红柿</th>
      <th>黄瓜</th>
      <th>白菜</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>11.0</td>
      <td>19.8</td>
      <td>15.4</td>
      <td>17.6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.4</td>
      <td>13.2</td>
      <td>11.0</td>
      <td>15.4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8.8</td>
      <td>15.4</td>
      <td>11.0</td>
      <td>2.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.6</td>
      <td>8.8</td>
      <td>15.4</td>
      <td>19.8</td>
    </tr>
    <tr>
      <th>5</th>
      <td>4.4</td>
      <td>6.6</td>
      <td>4.4</td>
      <td>6.6</td>
    </tr>
    <tr>
      <th>6</th>
      <td>15.0</td>
      <td>22.5</td>
      <td>12.5</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>5.0</td>
      <td>15.0</td>
      <td>15.0</td>
      <td>7.5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>20.0</td>
      <td>20.0</td>
      <td>5.0</td>
      <td>7.5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7.5</td>
      <td>17.5</td>
      <td>12.5</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>5.0</td>
      <td>12.5</td>
      <td>10.0</td>
      <td>12.5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7.5</td>
      <td>17.5</td>
      <td>7.5</td>
      <td>12.5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>22.5</td>
      <td>10.0</td>
      <td>2.5</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>5.0</td>
      <td>7.5</td>
      <td>10.0</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>14</th>
      <td>20.0</td>
      <td>7.5</td>
      <td>17.5</td>
      <td>17.5</td>
    </tr>
  </tbody>
</table>
    </div>



```python
# 将第7、9/11天的白萝卜价格降半价且减1元
df.loc[7:12:2,'白萝卜'] = df.loc[7:12:2,'白萝卜']/2-1
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
      <th>白萝卜</th>
      <th>西红柿</th>
      <th>黄瓜</th>
      <th>白菜</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>11.00</td>
      <td>19.8</td>
      <td>15.4</td>
      <td>17.6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.40</td>
      <td>13.2</td>
      <td>11.0</td>
      <td>15.4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8.80</td>
      <td>15.4</td>
      <td>11.0</td>
      <td>2.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.60</td>
      <td>8.8</td>
      <td>15.4</td>
      <td>19.8</td>
    </tr>
    <tr>
      <th>5</th>
      <td>4.40</td>
      <td>6.6</td>
      <td>4.4</td>
      <td>6.6</td>
    </tr>
    <tr>
      <th>6</th>
      <td>15.00</td>
      <td>22.5</td>
      <td>12.5</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1.50</td>
      <td>15.0</td>
      <td>15.0</td>
      <td>7.5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>20.00</td>
      <td>20.0</td>
      <td>5.0</td>
      <td>7.5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2.75</td>
      <td>17.5</td>
      <td>12.5</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>5.00</td>
      <td>12.5</td>
      <td>10.0</td>
      <td>12.5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2.75</td>
      <td>17.5</td>
      <td>7.5</td>
      <td>12.5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>22.50</td>
      <td>10.0</td>
      <td>2.5</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>5.00</td>
      <td>7.5</td>
      <td>10.0</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>14</th>
      <td>20.00</td>
      <td>7.5</td>
      <td>17.5</td>
      <td>17.5</td>
    </tr>
  </tbody>
</table>
    </div>

```python

df.iloc[[1,5,8],[0,3]]=np.nan
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
      <th>白萝卜</th>
      <th>西红柿</th>
      <th>黄瓜</th>
      <th>白菜</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>11.00</td>
      <td>19.8</td>
      <td>15.4</td>
      <td>17.6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>13.2</td>
      <td>11.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8.80</td>
      <td>15.4</td>
      <td>11.0</td>
      <td>2.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.60</td>
      <td>8.8</td>
      <td>15.4</td>
      <td>19.8</td>
    </tr>
    <tr>
      <th>5</th>
      <td>4.40</td>
      <td>6.6</td>
      <td>4.4</td>
      <td>6.6</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>22.5</td>
      <td>12.5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1.50</td>
      <td>15.0</td>
      <td>15.0</td>
      <td>7.5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>20.00</td>
      <td>20.0</td>
      <td>5.0</td>
      <td>7.5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>17.5</td>
      <td>12.5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>5.00</td>
      <td>12.5</td>
      <td>10.0</td>
      <td>12.5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2.75</td>
      <td>17.5</td>
      <td>7.5</td>
      <td>12.5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>22.50</td>
      <td>10.0</td>
      <td>2.5</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>5.00</td>
      <td>7.5</td>
      <td>10.0</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>14</th>
      <td>20.00</td>
      <td>7.5</td>
      <td>17.5</td>
      <td>17.5</td>
    </tr>
  </tbody>
</table>
    </div>


```

```

```python
df.add(1, fill_value=0)
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
      <th>白萝卜</th>
      <th>西红柿</th>
      <th>黄瓜</th>
      <th>白菜</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>12.00</td>
      <td>20.8</td>
      <td>16.4</td>
      <td>18.6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.00</td>
      <td>14.2</td>
      <td>12.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9.80</td>
      <td>16.4</td>
      <td>12.0</td>
      <td>3.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>18.60</td>
      <td>9.8</td>
      <td>16.4</td>
      <td>20.8</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5.40</td>
      <td>7.6</td>
      <td>5.4</td>
      <td>7.6</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1.00</td>
      <td>23.5</td>
      <td>13.5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2.50</td>
      <td>16.0</td>
      <td>16.0</td>
      <td>8.5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>21.00</td>
      <td>21.0</td>
      <td>6.0</td>
      <td>8.5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1.00</td>
      <td>18.5</td>
      <td>13.5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>6.00</td>
      <td>13.5</td>
      <td>11.0</td>
      <td>13.5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>3.75</td>
      <td>18.5</td>
      <td>8.5</td>
      <td>13.5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>23.50</td>
      <td>11.0</td>
      <td>3.5</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>6.00</td>
      <td>8.5</td>
      <td>11.0</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>14</th>
      <td>21.00</td>
      <td>8.5</td>
      <td>18.5</td>
      <td>18.5</td>
    </tr>
  </tbody>
</table>
    </div>

```python

df2 = DataFrame({
    'A':[1,2,3],
    'B':[5,6,7],
    'C':[8,9,10]
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>6</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>7</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
    </div>

```python

# axis='columns' -> axis=1
df2.add([1,2,3], axis='columns') # 按列相加，每行的数值按列的顺序相加
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>7</td>
      <td>11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>8</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
      <td>9</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
    </div>



```python
# axis='index' -> axis=0
df2.add(Series([10,11,12]),axis='index') # 按行相加，每列按行的顺序相加
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>11</td>
      <td>15</td>
      <td>18</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13</td>
      <td>17</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15</td>
      <td>19</td>
      <td>22</td>
    </tr>
  </tbody>
</table>
    </div>

```python

# 增加第四列，折扣列(8.8-5.5)
rate=np.round(Series(np.random.uniform(0.55,0.89,size=3)),2)
rate
```



```
0    0.74
1    0.75
2    0.58
dtype: float64
```



```python
# 新增一列
df2['rate'] = rate
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>5</td>
      <td>8</td>
      <td>0.74</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>6</td>
      <td>9</td>
      <td>0.75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>7</td>
      <td>10</td>
      <td>0.58</td>
    </tr>
  </tbody>
</table>
    </div>



```python
# 将 B 列的数值和rate列的数值相乘，并将结果生成result列
df2['result'] = df2['B'].mul(df2['rate']) # 两个Series按照航索引进行乘法运算
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>rate</th>
      <th>result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>5</td>
      <td>8</td>
      <td>0.74</td>
      <td>3.70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>6</td>
      <td>9</td>
      <td>0.75</td>
      <td>4.50</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>7</td>
      <td>10</td>
      <td>0.58</td>
      <td>4.06</td>
    </tr>
  </tbody>
</table>
    </div>



### 练习

- 假设ddd是期中考试成绩，ddd2是期末考试成绩，请自由创建ddd2，并将其与ddd相加，求期中期末平均值。
- 假设张三期中考试数学被发现作弊，要记为0分，如何实现？
- 李四因为举报张三作弊立功，期中考试所有科目加100分，如何实现？
- 后来老师发现有一道题出错了，为了安抚学生情绪，给每位学生每个科目都加10分，如何实现？

```python
names = ['张三', '李四', '王五', '赵六']
course = ['语文', '数学', '英语']

# 期中考试
ddd = DataFrame(np.random.randint(50,100, size=(4, 3)), names, course)
ddd
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
      <th>张三</th>
      <td>71</td>
      <td>99</td>
      <td>67</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>57</td>
      <td>70</td>
      <td>55</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>80</td>
      <td>90</td>
      <td>87</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>96</td>
      <td>81</td>
      <td>68</td>
    </tr>
  </tbody>
</table>
    </div>



```python
# 期末考试
ddd2 = DataFrame(np.random.randint(60,100, size=(4, 3)), names, course)
ddd2
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
      <th>张三</th>
      <td>89</td>
      <td>96</td>
      <td>83</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>94</td>
      <td>62</td>
      <td>60</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>90</td>
      <td>82</td>
      <td>70</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>78</td>
      <td>76</td>
      <td>62</td>
    </tr>
  </tbody>
</table>
    </div>



```python
# 平均成绩
(ddd + ddd2)/2

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
      <th>张三</th>
      <td>80.0</td>
      <td>97.5</td>
      <td>75.0</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>75.5</td>
      <td>66.0</td>
      <td>57.5</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>85.0</td>
      <td>86.0</td>
      <td>78.5</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>87.0</td>
      <td>78.5</td>
      <td>65.0</td>
    </tr>
  </tbody>
</table>
    </div>



```python
# 平均成绩
ddd.add(ddd2).div(2)
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
      <th>张三</th>
      <td>80.0</td>
      <td>97.5</td>
      <td>75.0</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>75.5</td>
      <td>66.0</td>
      <td>57.5</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>85.0</td>
      <td>86.0</td>
      <td>78.5</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>87.0</td>
      <td>78.5</td>
      <td>65.0</td>
    </tr>
  </tbody>
</table>
    </div>




```python
ddd.loc['张三',['数学']] = 0
ddd
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
      <th>张三</th>
      <td>71</td>
      <td>0</td>
      <td>67</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>57</td>
      <td>70</td>
      <td>55</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>80</td>
      <td>90</td>
      <td>87</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>96</td>
      <td>81</td>
      <td>68</td>
    </tr>
  </tbody>
</table>
    </div>


```python
ddd.loc['李四'] += 100
ddd
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
      <th>张三</th>
      <td>71</td>
      <td>0</td>
      <td>67</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>157</td>
      <td>170</td>
      <td>155</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>80</td>
      <td>90</td>
      <td>87</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>96</td>
      <td>81</td>
      <td>68</td>
    </tr>
  </tbody>
</table>
    </div>



```python
ddd.add(10)
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
      <th>张三</th>
      <td>81</td>
      <td>10</td>
      <td>77</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>167</td>
      <td>180</td>
      <td>165</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>90</td>
      <td>100</td>
      <td>97</td>
    </tr>
    <tr>
      <th>赵六</th>
      <td>106</td>
      <td>91</td>
      <td>78</td>
    </tr>
  </tbody>
</table>
    </div>
