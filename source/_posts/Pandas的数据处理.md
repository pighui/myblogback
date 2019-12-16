---
title: Pandas的数据处理
comments: true
tags:
  - Python
  - 数据分析
categories:
  - 数据分析
date: 2019-05-05 14:06:29
---

```python
import numpy as np
import pandas as pd
from pandas import Series, DataFrame
```

<!--more-->

### 删除重复行数据

```python
# 创建日志表
# 列： 日志编号、日志等级、日志名称、日志的消息
# 行： 日志的日期, 2018-10-10
logs = DataFrame({
    'ID': np.arange(1, 11, step=1),
    'LevelName': np.random.choice(['INFO','ERROR', 'WARNNING', 'CRITICAL'],
                                 size=10),
    'Name': np.random.choice(['django', 'flask', 'scrapy'], size=10),
    'Message': np.random.choice(['登录', '下订单', '支付', '积分',
                                 '秒杀', '验证码'], size=10)
},index=[ '2019-04-%s' % str(day).rjust(2, '0') for day in range(1, 11)])
logs
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
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-01</th>
      <td>1</td>
      <td>INFO</td>
      <td>scrapy</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-02</th>
      <td>2</td>
      <td>INFO</td>
      <td>django</td>
      <td>积分</td>
    </tr>
    <tr>
      <th>2019-04-03</th>
      <td>3</td>
      <td>WARNNING</td>
      <td>flask</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-04</th>
      <td>4</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-05</th>
      <td>5</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-06</th>
      <td>6</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-07</th>
      <td>7</td>
      <td>ERROR</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-08</th>
      <td>8</td>
      <td>CRITICAL</td>
      <td>scrapy</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-09</th>
      <td>9</td>
      <td>CRITICAL</td>
      <td>flask</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-10</th>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
    </tr>
  </tbody>
</table>
</div>



```python
logs.loc['2019-04-11'] = logs.loc['2019-04-10']
logs
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
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-01</th>
      <td>1</td>
      <td>INFO</td>
      <td>scrapy</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-02</th>
      <td>2</td>
      <td>INFO</td>
      <td>django</td>
      <td>积分</td>
    </tr>
    <tr>
      <th>2019-04-03</th>
      <td>3</td>
      <td>WARNNING</td>
      <td>flask</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-04</th>
      <td>4</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-05</th>
      <td>5</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-06</th>
      <td>6</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-07</th>
      <td>7</td>
      <td>ERROR</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-08</th>
      <td>8</td>
      <td>CRITICAL</td>
      <td>scrapy</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-09</th>
      <td>9</td>
      <td>CRITICAL</td>
      <td>flask</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-10</th>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
    </tr>
    <tr>
      <th>2019-04-11</th>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 查找重复行数据
# keep = { 'last',  'first'}  
# last表示最后一个重复行不是重复的， first 表示第一个重复行不是重复的，即保留哪一个
logs.duplicated(keep='last')
```



```
2019-04-01    False
2019-04-02    False
2019-04-03    False
2019-04-04    False
2019-04-05    False
2019-04-06    False
2019-04-07    False
2019-04-08    False
2019-04-09    False
2019-04-10     True
2019-04-11    False
dtype: bool
```



```python
# 获取哪些行值为True的行数据
logs.loc[logs.duplicated(keep='last')]
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
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-10</th>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
    </tr>
  </tbody>
</table>
</div>




```python
logs.drop(logs[logs.duplicated(keep='last')].index,
          axis=0)
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
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-01</th>
      <td>1</td>
      <td>INFO</td>
      <td>scrapy</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-02</th>
      <td>2</td>
      <td>INFO</td>
      <td>django</td>
      <td>积分</td>
    </tr>
    <tr>
      <th>2019-04-03</th>
      <td>3</td>
      <td>WARNNING</td>
      <td>flask</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-04</th>
      <td>4</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-05</th>
      <td>5</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-06</th>
      <td>6</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-07</th>
      <td>7</td>
      <td>ERROR</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-08</th>
      <td>8</td>
      <td>CRITICAL</td>
      <td>scrapy</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-09</th>
      <td>9</td>
      <td>CRITICAL</td>
      <td>flask</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-11</th>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 快速删除重复行数据
# inplace =True 在原有的数据上进行修改， 如果=False，表示返回修改后的复本
logs.drop_duplicates(keep='first', inplace=True) # 默认情况保留重复行的第一行
logs
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
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-01</th>
      <td>1</td>
      <td>INFO</td>
      <td>scrapy</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-02</th>
      <td>2</td>
      <td>INFO</td>
      <td>django</td>
      <td>积分</td>
    </tr>
    <tr>
      <th>2019-04-03</th>
      <td>3</td>
      <td>WARNNING</td>
      <td>flask</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-04</th>
      <td>4</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-05</th>
      <td>5</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-06</th>
      <td>6</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-07</th>
      <td>7</td>
      <td>ERROR</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-08</th>
      <td>8</td>
      <td>CRITICAL</td>
      <td>scrapy</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-09</th>
      <td>9</td>
      <td>CRITICAL</td>
      <td>flask</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-10</th>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 删除 LevelName, ID 列
# 删除 2019-04-05, 2019-04-08 行
# logs.drop(index='2019-04-05', columns='LevelName')
# logs.drop(index=['2019-04-05', '2019-04-08'],
#           columns=['ID', 'LevelName'])

# logs.drop(index=['2019-04-05', '2019-04-08'])
# logs.drop(columns=['ID', 'LevelName'])
# logs.drop(['ID', 'LevelName'], axis=1)
logs.drop(['2019-04-05', '2019-04-08'], axis=0)
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
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-01</th>
      <td>1</td>
      <td>INFO</td>
      <td>scrapy</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-02</th>
      <td>2</td>
      <td>INFO</td>
      <td>django</td>
      <td>积分</td>
    </tr>
    <tr>
      <th>2019-04-03</th>
      <td>3</td>
      <td>WARNNING</td>
      <td>flask</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-04</th>
      <td>4</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-06</th>
      <td>6</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-07</th>
      <td>7</td>
      <td>ERROR</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-09</th>
      <td>9</td>
      <td>CRITICAL</td>
      <td>flask</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-10</th>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
    </tr>
  </tbody>
</table>
</div>




### 映射操作

- replace(olds, news) 将olds的数据替换成news的数据
- map() 根据指定的列映射出相应的数据，如根据成绩，列出等级
- rename() 重命名

```python
logs
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
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-01</th>
      <td>1</td>
      <td>INFO</td>
      <td>scrapy</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-02</th>
      <td>2</td>
      <td>INFO</td>
      <td>django</td>
      <td>积分</td>
    </tr>
    <tr>
      <th>2019-04-03</th>
      <td>3</td>
      <td>WARNNING</td>
      <td>flask</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-04</th>
      <td>4</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-05</th>
      <td>5</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-06</th>
      <td>6</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-07</th>
      <td>7</td>
      <td>ERROR</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-08</th>
      <td>8</td>
      <td>CRITICAL</td>
      <td>scrapy</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-09</th>
      <td>9</td>
      <td>CRITICAL</td>
      <td>flask</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-10</th>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 将数据中所有ERROR修改成 "错误", INFO改成 '正常'
logs.replace(to_replace='ERROR', value='错误')
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
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-01</th>
      <td>1</td>
      <td>INFO</td>
      <td>scrapy</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-02</th>
      <td>2</td>
      <td>INFO</td>
      <td>django</td>
      <td>积分</td>
    </tr>
    <tr>
      <th>2019-04-03</th>
      <td>3</td>
      <td>WARNNING</td>
      <td>flask</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-04</th>
      <td>4</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-05</th>
      <td>5</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-06</th>
      <td>6</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-07</th>
      <td>7</td>
      <td>错误</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-08</th>
      <td>8</td>
      <td>CRITICAL</td>
      <td>scrapy</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-09</th>
      <td>9</td>
      <td>CRITICAL</td>
      <td>flask</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-10</th>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
    </tr>
  </tbody>
</table>
</div>




```python
logs.replace({
    'ERROR': '错误',
    'INFO': '正常'
})
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
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-01</th>
      <td>1</td>
      <td>正常</td>
      <td>scrapy</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-02</th>
      <td>2</td>
      <td>正常</td>
      <td>django</td>
      <td>积分</td>
    </tr>
    <tr>
      <th>2019-04-03</th>
      <td>3</td>
      <td>WARNNING</td>
      <td>flask</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-04</th>
      <td>4</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-05</th>
      <td>5</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-06</th>
      <td>6</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-07</th>
      <td>7</td>
      <td>错误</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-08</th>
      <td>8</td>
      <td>CRITICAL</td>
      <td>scrapy</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-09</th>
      <td>9</td>
      <td>CRITICAL</td>
      <td>flask</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-10</th>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
    </tr>
  </tbody>
</table>
</div>




```python
logs.replace(['ERROR','INFO'], ['错误', '正常'])
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
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-01</th>
      <td>1</td>
      <td>正常</td>
      <td>scrapy</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-02</th>
      <td>2</td>
      <td>正常</td>
      <td>django</td>
      <td>积分</td>
    </tr>
    <tr>
      <th>2019-04-03</th>
      <td>3</td>
      <td>WARNNING</td>
      <td>flask</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-04</th>
      <td>4</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-05</th>
      <td>5</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>验证码</td>
    </tr>
    <tr>
      <th>2019-04-06</th>
      <td>6</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-07</th>
      <td>7</td>
      <td>错误</td>
      <td>django</td>
      <td>下订单</td>
    </tr>
    <tr>
      <th>2019-04-08</th>
      <td>8</td>
      <td>CRITICAL</td>
      <td>scrapy</td>
      <td>支付</td>
    </tr>
    <tr>
      <th>2019-04-09</th>
      <td>9</td>
      <td>CRITICAL</td>
      <td>flask</td>
      <td>秒杀</td>
    </tr>
    <tr>
      <th>2019-04-10</th>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
    </tr>
  </tbody>
</table>
</div>




创建新的一列 version列， 根据 Name字段，指定不同列值映射不同的版本，详情如下：
scrapy -> 1.1
django -> 2.0
flask  -> 1.2

要求使用map()函数

```python
# 获取Name列值的Series,
# 再通过Series对象的map()函数，将每一行对应的数值映射成对应的值
logs['version'] = logs['Name'].map({
    'scrapy': 1.1,
    'django': 2.0,
    'flask': 1.2
})
logs
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
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
      <th>version</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-01</th>
      <td>1</td>
      <td>INFO</td>
      <td>scrapy</td>
      <td>验证码</td>
      <td>1.1</td>
    </tr>
    <tr>
      <th>2019-04-02</th>
      <td>2</td>
      <td>INFO</td>
      <td>django</td>
      <td>积分</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2019-04-03</th>
      <td>3</td>
      <td>WARNNING</td>
      <td>flask</td>
      <td>支付</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>2019-04-04</th>
      <td>4</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>秒杀</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2019-04-05</th>
      <td>5</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>验证码</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2019-04-06</th>
      <td>6</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>下订单</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2019-04-07</th>
      <td>7</td>
      <td>ERROR</td>
      <td>django</td>
      <td>下订单</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2019-04-08</th>
      <td>8</td>
      <td>CRITICAL</td>
      <td>scrapy</td>
      <td>支付</td>
      <td>1.1</td>
    </tr>
    <tr>
      <th>2019-04-09</th>
      <td>9</td>
      <td>CRITICAL</td>
      <td>flask</td>
      <td>秒杀</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>2019-04-10</th>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 将行索引转成一列，列名为Date
# drop=True, 表示重新生成行索引标签
logs_2 = logs.reset_index().rename(columns={'index': 'Date'})
logs_2
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
      <th>Date</th>
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
      <th>version</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2019-04-01</td>
      <td>1</td>
      <td>INFO</td>
      <td>scrapy</td>
      <td>验证码</td>
      <td>1.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019-04-02</td>
      <td>2</td>
      <td>INFO</td>
      <td>django</td>
      <td>积分</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019-04-03</td>
      <td>3</td>
      <td>WARNNING</td>
      <td>flask</td>
      <td>支付</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2019-04-04</td>
      <td>4</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>秒杀</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019-04-05</td>
      <td>5</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>验证码</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2019-04-06</td>
      <td>6</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>下订单</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2019-04-07</td>
      <td>7</td>
      <td>ERROR</td>
      <td>django</td>
      <td>下订单</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2019-04-08</td>
      <td>8</td>
      <td>CRITICAL</td>
      <td>scrapy</td>
      <td>支付</td>
      <td>1.1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2019-04-09</td>
      <td>9</td>
      <td>CRITICAL</td>
      <td>flask</td>
      <td>秒杀</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019-04-10</td>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 查看Date的类型
logs_2['Date'].dtype
```



```
dtype('O')
```



```python
logs_2.dtypes # 查看所有列的类型
```



```
Date          object
ID             int64
LevelName     object
Name          object
Message       object
version      float64
dtype: object
```



```python
# 修改version的数据类型 float64 为 string 类型
# map()中指定类型转换的函数，将version的每一行的数据经过转换函数转成指定的类型
logs_2['version'] = logs_2['version'].map(str)
logs_2.dtypes
```



```
Date         object
ID            int64
LevelName    object
Name         object
Message      object
version      object
dtype: object
```



```python
# 修改Date列的类型string为datetime类型
from datetime import datetime

def convert_dt(item):
    # item是每一行的数值，类型是str
    # item: 2019-04-01
    return datetime.strptime(item, '%Y-%m-%d')
```

```python
logs_2['Date'] = logs_2['Date'].map(convert_dt)
logs_2.dtypes
```



```
Date         datetime64[ns]
ID                    int64
LevelName            object
Name                 object
Message              object
version              object
dtype: object
```



```python
# 将Date列的数据转成 月和日的字符串
logs_2['Date'] = logs_2['Date'].map(lambda item:item.strftime('%m-%d'))
logs_2
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
      <th>Date</th>
      <th>ID</th>
      <th>LevelName</th>
      <th>Name</th>
      <th>Message</th>
      <th>version</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>04-01</td>
      <td>1</td>
      <td>INFO</td>
      <td>scrapy</td>
      <td>验证码</td>
      <td>1.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>04-02</td>
      <td>2</td>
      <td>INFO</td>
      <td>django</td>
      <td>积分</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>04-03</td>
      <td>3</td>
      <td>WARNNING</td>
      <td>flask</td>
      <td>支付</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>04-04</td>
      <td>4</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>秒杀</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>04-05</td>
      <td>5</td>
      <td>CRITICAL</td>
      <td>django</td>
      <td>验证码</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>04-06</td>
      <td>6</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>下订单</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>04-07</td>
      <td>7</td>
      <td>ERROR</td>
      <td>django</td>
      <td>下订单</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>04-08</td>
      <td>8</td>
      <td>CRITICAL</td>
      <td>scrapy</td>
      <td>支付</td>
      <td>1.1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>04-09</td>
      <td>9</td>
      <td>CRITICAL</td>
      <td>flask</td>
      <td>秒杀</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>04-10</td>
      <td>10</td>
      <td>WARNNING</td>
      <td>django</td>
      <td>登录</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 创建五位同学的三个课程的成绩表
# 五位同学的姓名分别是A, B, C, D, E
# 三门课程分别是 Python, Java, H5
scores = DataFrame(np.random.randint(40, 100, size=(5, 3)),
                  index=list('ABCDE'),
                  columns=['Python', 'Java', 'H5'])
scores
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
      <th>Java</th>
      <th>H5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>64</td>
      <td>44</td>
      <td>84</td>
    </tr>
    <tr>
      <th>B</th>
      <td>85</td>
      <td>76</td>
      <td>79</td>
    </tr>
    <tr>
      <th>C</th>
      <td>61</td>
      <td>96</td>
      <td>44</td>
    </tr>
    <tr>
      <th>D</th>
      <td>68</td>
      <td>56</td>
      <td>43</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>53</td>
      <td>56</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 增加一个 level列，根据Python列值，生成不同的等级，详情如下：
# >=90            -> A
# < 90 and  >= 75 -> B
# < 75 and >=60   -> C
# < 60            -> D
# 三目运算， Java/C->  item>=90?'A': item>=75?'B': item>=60?'C':'D'
level_convert = lambda item: 'A' if item >=90 else 'B' if item >=75 else 'C' if item>=60 else 'D'

scores['level'] = scores['Python'].map(level_convert)
scores
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
      <th>Java</th>
      <th>H5</th>
      <th>level</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>64</td>
      <td>44</td>
      <td>84</td>
      <td>C</td>
    </tr>
    <tr>
      <th>B</th>
      <td>85</td>
      <td>76</td>
      <td>79</td>
      <td>B</td>
    </tr>
    <tr>
      <th>C</th>
      <td>61</td>
      <td>96</td>
      <td>44</td>
      <td>C</td>
    </tr>
    <tr>
      <th>D</th>
      <td>68</td>
      <td>56</td>
      <td>43</td>
      <td>C</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>53</td>
      <td>56</td>
      <td>C</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 删除level列
scores.drop(columns='level', inplace=True)
scores
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
      <th>Java</th>
      <th>H5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>64</td>
      <td>44</td>
      <td>84</td>
    </tr>
    <tr>
      <th>B</th>
      <td>85</td>
      <td>76</td>
      <td>79</td>
    </tr>
    <tr>
      <th>C</th>
      <td>61</td>
      <td>96</td>
      <td>44</td>
    </tr>
    <tr>
      <th>D</th>
      <td>68</td>
      <td>56</td>
      <td>43</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>53</td>
      <td>56</td>
    </tr>
  </tbody>
</table>
</div>



### 扩展使用 transform()

- 功能，同map()函数，将某一行的值转成别一个行值
- 不同的是，map()函数支持dict映射， 而transform()函数不支持dict映射

```python
scores['level'] = scores['Python'].transform(level_convert)
scores
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
      <th>Java</th>
      <th>H5</th>
      <th>level</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>64</td>
      <td>44</td>
      <td>84</td>
      <td>C</td>
    </tr>
    <tr>
      <th>B</th>
      <td>85</td>
      <td>76</td>
      <td>79</td>
      <td>B</td>
    </tr>
    <tr>
      <th>C</th>
      <td>61</td>
      <td>96</td>
      <td>44</td>
      <td>C</td>
    </tr>
    <tr>
      <th>D</th>
      <td>68</td>
      <td>56</td>
      <td>43</td>
      <td>C</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>53</td>
      <td>56</td>
      <td>C</td>
    </tr>
  </tbody>
</table>
</div>



思考： 如果拿出三个课程（三列），如何进行映射？

```python
# transform可以针对多列进行映射，但必须同分组函数一块使用
# 计算三门课程的总成绩，并生成总成绩列
scores['total'] = scores.sum(axis=1)
scores
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
      <th>Java</th>
      <th>H5</th>
      <th>level</th>
      <th>total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>64</td>
      <td>44</td>
      <td>84</td>
      <td>C</td>
      <td>192</td>
    </tr>
    <tr>
      <th>B</th>
      <td>85</td>
      <td>76</td>
      <td>79</td>
      <td>B</td>
      <td>240</td>
    </tr>
    <tr>
      <th>C</th>
      <td>61</td>
      <td>96</td>
      <td>44</td>
      <td>C</td>
      <td>201</td>
    </tr>
    <tr>
      <th>D</th>
      <td>68</td>
      <td>56</td>
      <td>43</td>
      <td>C</td>
      <td>167</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>53</td>
      <td>56</td>
      <td>C</td>
      <td>175</td>
    </tr>
  </tbody>
</table>
</div>




练习：
新增两列，分别为张三、李四的成绩状态，如果分数低于90，则为"failed"，如果分数高于120，则为"excellent"，其他则为"pass"
【提示】使用函数作为map的参数

```python
scores2 = DataFrame({
    '张三': [50, 99, 130],
    '李四': [75, 150, 100],
    '王五': [90, 79, 110]
}, index=['Python', 'Flask', 'Scrapy'])
scores2
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
      <th>张三</th>
      <th>李四</th>
      <th>王五</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Python</th>
      <td>50</td>
      <td>75</td>
      <td>90</td>
    </tr>
    <tr>
      <th>Flask</th>
      <td>99</td>
      <td>150</td>
      <td>79</td>
    </tr>
    <tr>
      <th>Scrapy</th>
      <td>130</td>
      <td>100</td>
      <td>110</td>
    </tr>
  </tbody>
</table>
    </div>



```python
level_func = lambda item: 'failed' if item <90  else 'excellent' if item > 120 else 'pass'
scores2['level_z'] = scores2['张三'].map(level_func)
scores2['level_l'] = scores2['李四'].map(level_func)
scores2
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
      <th>张三</th>
      <th>李四</th>
      <th>王五</th>
      <th>level_z</th>
      <th>level_l</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Python</th>
      <td>50</td>
      <td>75</td>
      <td>90</td>
      <td>failed</td>
      <td>failed</td>
    </tr>
    <tr>
      <th>Flask</th>
      <td>99</td>
      <td>150</td>
      <td>79</td>
      <td>pass</td>
      <td>excellent</td>
    </tr>
    <tr>
      <th>Scrapy</th>
      <td>130</td>
      <td>100</td>
      <td>110</td>
      <td>excellent</td>
      <td>pass</td>
    </tr>
  </tbody>
</table>
</div>




```python
DataFrame(scores2.unstack()).unstack()
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
      <th colspan="3" halign="left">0</th>
    </tr>
    <tr>
      <th></th>
      <th>Python</th>
      <th>Flask</th>
      <th>Scrapy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>50</td>
      <td>99</td>
      <td>130</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>75</td>
      <td>150</td>
      <td>100</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>90</td>
      <td>79</td>
      <td>110</td>
    </tr>
    <tr>
      <th>level_z</th>
      <td>failed</td>
      <td>pass</td>
      <td>excellent</td>
    </tr>
    <tr>
      <th>level_l</th>
      <td>failed</td>
      <td>excellent</td>
      <td>pass</td>
    </tr>
  </tbody>
</table>
</div>




```python
scores2.transpose()
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
      <th>Flask</th>
      <th>Scrapy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>张三</th>
      <td>50</td>
      <td>99</td>
      <td>130</td>
    </tr>
    <tr>
      <th>李四</th>
      <td>75</td>
      <td>150</td>
      <td>100</td>
    </tr>
    <tr>
      <th>王五</th>
      <td>90</td>
      <td>79</td>
      <td>110</td>
    </tr>
    <tr>
      <th>level_z</th>
      <td>failed</td>
      <td>pass</td>
      <td>excellent</td>
    </tr>
    <tr>
      <th>level_l</th>
      <td>failed</td>
      <td>excellent</td>
      <td>pass</td>
    </tr>
  </tbody>
</table>
</div>




### rename()替换索引标签

- 行索引标签，index
- 列索引标签，columns
- 多层索引标签，level属性

```python
scores.drop(['level', 'total'], axis=1, inplace=True)
scores
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
      <th>Java</th>
      <th>H5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>64</td>
      <td>44</td>
      <td>84</td>
    </tr>
    <tr>
      <th>B</th>
      <td>85</td>
      <td>76</td>
      <td>79</td>
    </tr>
    <tr>
      <th>C</th>
      <td>61</td>
      <td>96</td>
      <td>44</td>
    </tr>
    <tr>
      <th>D</th>
      <td>68</td>
      <td>56</td>
      <td>43</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>53</td>
      <td>56</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 修改A的行标签为disen，B标签为jack
scores.rename(index={
    'A': 'disen',
    'B': 'jack',
})
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
      <th>Java</th>
      <th>H5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>disen</th>
      <td>64</td>
      <td>44</td>
      <td>84</td>
    </tr>
    <tr>
      <th>jack</th>
      <td>85</td>
      <td>76</td>
      <td>79</td>
    </tr>
    <tr>
      <th>C</th>
      <td>61</td>
      <td>96</td>
      <td>44</td>
    </tr>
    <tr>
      <th>D</th>
      <td>68</td>
      <td>56</td>
      <td>43</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>53</td>
      <td>56</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 修改Python为Py3，H5为HTML5
scores.rename(columns={
    'Python': 'Py3',
    'H5': 'HTML5'
})
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
      <th>Py3</th>
      <th>Java</th>
      <th>HTML5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>64</td>
      <td>44</td>
      <td>84</td>
    </tr>
    <tr>
      <th>B</th>
      <td>85</td>
      <td>76</td>
      <td>79</td>
    </tr>
    <tr>
      <th>C</th>
      <td>61</td>
      <td>96</td>
      <td>44</td>
    </tr>
    <tr>
      <th>D</th>
      <td>68</td>
      <td>56</td>
      <td>43</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>53</td>
      <td>56</td>
    </tr>
  </tbody>
</table>
</div>




```python
s2 = pd.concat((scores,scores), axis=1, keys=('上学期', '下学期'))
s2
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
      <th colspan="3" halign="left">上学期</th>
      <th colspan="3" halign="left">下学期</th>
    </tr>
    <tr>
      <th></th>
      <th>Python</th>
      <th>Java</th>
      <th>H5</th>
      <th>Python</th>
      <th>Java</th>
      <th>H5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>64</td>
      <td>44</td>
      <td>84</td>
      <td>64</td>
      <td>44</td>
      <td>84</td>
    </tr>
    <tr>
      <th>B</th>
      <td>85</td>
      <td>76</td>
      <td>79</td>
      <td>85</td>
      <td>76</td>
      <td>79</td>
    </tr>
    <tr>
      <th>C</th>
      <td>61</td>
      <td>96</td>
      <td>44</td>
      <td>61</td>
      <td>96</td>
      <td>44</td>
    </tr>
    <tr>
      <th>D</th>
      <td>68</td>
      <td>56</td>
      <td>43</td>
      <td>68</td>
      <td>56</td>
      <td>43</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>53</td>
      <td>56</td>
      <td>66</td>
      <td>53</td>
      <td>56</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 修改s2表中的上学期为”期中“，下学期为”期末“
s2.rename({
    '上学期': '期中',
    '下学期': '期末'
}, axis=1, level=0)
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
      <th colspan="3" halign="left">期中</th>
      <th colspan="3" halign="left">期末</th>
    </tr>
    <tr>
      <th></th>
      <th>Python</th>
      <th>Java</th>
      <th>H5</th>
      <th>Python</th>
      <th>Java</th>
      <th>H5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>64</td>
      <td>44</td>
      <td>84</td>
      <td>64</td>
      <td>44</td>
      <td>84</td>
    </tr>
    <tr>
      <th>B</th>
      <td>85</td>
      <td>76</td>
      <td>79</td>
      <td>85</td>
      <td>76</td>
      <td>79</td>
    </tr>
    <tr>
      <th>C</th>
      <td>61</td>
      <td>96</td>
      <td>44</td>
      <td>61</td>
      <td>96</td>
      <td>44</td>
    </tr>
    <tr>
      <th>D</th>
      <td>68</td>
      <td>56</td>
      <td>43</td>
      <td>68</td>
      <td>56</td>
      <td>43</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>53</td>
      <td>56</td>
      <td>66</td>
      <td>53</td>
      <td>56</td>
    </tr>
  </tbody>
</table>
</div>




### 异常值检测和过滤

- describe()
- any()和std()

```python
scores.describe()  # 统计每一列的数据分布
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
      <th>Java</th>
      <th>H5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.00000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>68.800000</td>
      <td>65.000000</td>
      <td>61.20000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>9.418068</td>
      <td>20.904545</td>
      <td>19.30544</td>
    </tr>
    <tr>
      <th>min</th>
      <td>61.000000</td>
      <td>44.000000</td>
      <td>43.00000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>64.000000</td>
      <td>53.000000</td>
      <td>44.00000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>66.000000</td>
      <td>56.000000</td>
      <td>56.00000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>68.000000</td>
      <td>76.000000</td>
      <td>79.00000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>85.000000</td>
      <td>96.000000</td>
      <td>84.00000</td>
    </tr>
  </tbody>
</table>
</div>




```python
scores.std(axis=1) # 查看每行数据的标准差，即没人的各科成绩的分布情况
```



```
A    20.000000
B     4.582576
C    26.514147
D    12.503333
E     6.806859
dtype: float64
```



```python
scores
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
      <th>Java</th>
      <th>H5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>64</td>
      <td>44</td>
      <td>84</td>
    </tr>
    <tr>
      <th>B</th>
      <td>85</td>
      <td>76</td>
      <td>79</td>
    </tr>
    <tr>
      <th>C</th>
      <td>61</td>
      <td>96</td>
      <td>44</td>
    </tr>
    <tr>
      <th>D</th>
      <td>68</td>
      <td>56</td>
      <td>43</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>53</td>
      <td>56</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 指定百分比显示的段
scores.describe(percentiles=[0.45, 0.65, 0.85])  # 默认0.5是必须存在的
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
      <th>Java</th>
      <th>H5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.00000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>68.800000</td>
      <td>65.000000</td>
      <td>61.20000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>9.418068</td>
      <td>20.904545</td>
      <td>19.30544</td>
    </tr>
    <tr>
      <th>min</th>
      <td>61.000000</td>
      <td>44.000000</td>
      <td>43.00000</td>
    </tr>
    <tr>
      <th>45%</th>
      <td>65.600000</td>
      <td>55.400000</td>
      <td>53.60000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>66.000000</td>
      <td>56.000000</td>
      <td>56.00000</td>
    </tr>
    <tr>
      <th>65%</th>
      <td>67.200000</td>
      <td>68.000000</td>
      <td>69.80000</td>
    </tr>
    <tr>
      <th>85%</th>
      <td>74.800000</td>
      <td>84.000000</td>
      <td>81.00000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>85.000000</td>
      <td>96.000000</td>
      <td>84.00000</td>
    </tr>
  </tbody>
</table>
</div>




```python
scores.dtypes
```



```
Python    int64
Java      int64
H5        int64
dtype: object
```



```python
scores.loc['A', 'Java'] = None
scores
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
      <th>Java</th>
      <th>H5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>64</td>
      <td>NaN</td>
      <td>84</td>
    </tr>
    <tr>
      <th>B</th>
      <td>85</td>
      <td>76.0</td>
      <td>79</td>
    </tr>
    <tr>
      <th>C</th>
      <td>61</td>
      <td>96.0</td>
      <td>44</td>
    </tr>
    <tr>
      <th>D</th>
      <td>68</td>
      <td>56.0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>E</th>
      <td>66</td>
      <td>53.0</td>
      <td>56</td>
    </tr>
  </tbody>
</table>
</div>




```python
scores.dtypes
```



```
Python      int64
Java      float64
H5          int64
dtype: object
```



```python
scores.describe(include=np.int64)  # 指定统计计算的数据类型
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>5.000000</td>
      <td>5.00000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>68.800000</td>
      <td>61.20000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>9.418068</td>
      <td>19.30544</td>
    </tr>
    <tr>
      <th>min</th>
      <td>61.000000</td>
      <td>43.00000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>64.000000</td>
      <td>44.00000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>66.000000</td>
      <td>56.00000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>68.000000</td>
      <td>79.00000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>85.000000</td>
      <td>84.00000</td>
    </tr>
  </tbody>
</table>
</div>




```python
scores.any(axis=1)
```



```
A    True
B    True
C    True
D    True
E    True
dtype: bool
```



练习：新建一个形状10000*3的标准正态分布的DataFrame(np.random.randn),去掉所有满足以下条件的行：其中任一元素的绝对值大于3倍标准差

**以100条数据示例**

```python
d = DataFrame(np.random.randn(100, 3), columns=('A', 'B', 'C'))
d
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
      <td>-1.164291</td>
      <td>0.797137</td>
      <td>-0.251975</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.201639</td>
      <td>-1.886578</td>
      <td>-1.352991</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.956560</td>
      <td>0.253978</td>
      <td>0.190281</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.106657</td>
      <td>0.791620</td>
      <td>-0.805228</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.964321</td>
      <td>0.545341</td>
      <td>-2.175794</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.044096</td>
      <td>-0.235177</td>
      <td>0.492157</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.500263</td>
      <td>-1.430520</td>
      <td>1.048750</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.293912</td>
      <td>0.896059</td>
      <td>-0.109282</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.464239</td>
      <td>-0.281743</td>
      <td>-0.712988</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-0.370665</td>
      <td>2.277106</td>
      <td>-1.424837</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.154458</td>
      <td>0.059086</td>
      <td>-0.115698</td>
    </tr>
    <tr>
      <th>11</th>
      <td>-0.265803</td>
      <td>0.160085</td>
      <td>-0.170685</td>
    </tr>
    <tr>
      <th>12</th>
      <td>-0.730650</td>
      <td>-0.109982</td>
      <td>-0.463942</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.201926</td>
      <td>1.263386</td>
      <td>0.629739</td>
    </tr>
    <tr>
      <th>14</th>
      <td>-2.177481</td>
      <td>-0.188986</td>
      <td>1.411646</td>
    </tr>
    <tr>
      <th>15</th>
      <td>-1.228296</td>
      <td>0.980455</td>
      <td>-1.354884</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-0.664823</td>
      <td>0.268899</td>
      <td>1.012338</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-0.190291</td>
      <td>-1.078339</td>
      <td>-0.456569</td>
    </tr>
    <tr>
      <th>18</th>
      <td>-0.108290</td>
      <td>-0.070409</td>
      <td>0.803164</td>
    </tr>
    <tr>
      <th>19</th>
      <td>0.887057</td>
      <td>-1.473393</td>
      <td>-1.126295</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1.057284</td>
      <td>0.010266</td>
      <td>1.677125</td>
    </tr>
    <tr>
      <th>21</th>
      <td>0.467551</td>
      <td>0.610109</td>
      <td>2.110309</td>
    </tr>
    <tr>
      <th>22</th>
      <td>-1.536377</td>
      <td>1.084455</td>
      <td>-0.134929</td>
    </tr>
    <tr>
      <th>23</th>
      <td>-0.335276</td>
      <td>1.242639</td>
      <td>-0.912711</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1.579240</td>
      <td>-0.077694</td>
      <td>0.960719</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2.334651</td>
      <td>1.118378</td>
      <td>-0.584885</td>
    </tr>
    <tr>
      <th>26</th>
      <td>-0.878469</td>
      <td>0.575112</td>
      <td>0.753077</td>
    </tr>
    <tr>
      <th>27</th>
      <td>-0.886514</td>
      <td>-1.596037</td>
      <td>-0.579165</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1.419417</td>
      <td>-2.660823</td>
      <td>-1.545299</td>
    </tr>
    <tr>
      <th>29</th>
      <td>-0.460868</td>
      <td>-0.773910</td>
      <td>0.617897</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>70</th>
      <td>0.324589</td>
      <td>-1.538287</td>
      <td>1.675682</td>
    </tr>
    <tr>
      <th>71</th>
      <td>-0.584616</td>
      <td>-0.489804</td>
      <td>0.885449</td>
    </tr>
    <tr>
      <th>72</th>
      <td>-0.158786</td>
      <td>0.432890</td>
      <td>-1.351910</td>
    </tr>
    <tr>
      <th>73</th>
      <td>-0.677642</td>
      <td>0.284412</td>
      <td>1.542141</td>
    </tr>
    <tr>
      <th>74</th>
      <td>1.197553</td>
      <td>-1.480051</td>
      <td>0.707695</td>
    </tr>
    <tr>
      <th>75</th>
      <td>0.866642</td>
      <td>-2.166048</td>
      <td>2.007399</td>
    </tr>
    <tr>
      <th>76</th>
      <td>1.342749</td>
      <td>-0.948632</td>
      <td>0.017686</td>
    </tr>
    <tr>
      <th>77</th>
      <td>1.211767</td>
      <td>1.790328</td>
      <td>-0.384149</td>
    </tr>
    <tr>
      <th>78</th>
      <td>-1.196269</td>
      <td>0.066043</td>
      <td>-1.108524</td>
    </tr>
    <tr>
      <th>79</th>
      <td>0.257693</td>
      <td>0.941103</td>
      <td>-0.352873</td>
    </tr>
    <tr>
      <th>80</th>
      <td>0.085246</td>
      <td>-0.644327</td>
      <td>0.171741</td>
    </tr>
    <tr>
      <th>81</th>
      <td>0.952371</td>
      <td>-0.411009</td>
      <td>-1.553032</td>
    </tr>
    <tr>
      <th>82</th>
      <td>-0.575233</td>
      <td>1.195594</td>
      <td>-0.838789</td>
    </tr>
    <tr>
      <th>83</th>
      <td>-0.666920</td>
      <td>-0.361069</td>
      <td>0.384706</td>
    </tr>
    <tr>
      <th>84</th>
      <td>-0.766464</td>
      <td>1.255243</td>
      <td>0.399759</td>
    </tr>
    <tr>
      <th>85</th>
      <td>-2.505601</td>
      <td>-0.940245</td>
      <td>-0.250290</td>
    </tr>
    <tr>
      <th>86</th>
      <td>0.136244</td>
      <td>-0.984630</td>
      <td>0.148026</td>
    </tr>
    <tr>
      <th>87</th>
      <td>-0.639923</td>
      <td>-0.485517</td>
      <td>-0.117722</td>
    </tr>
    <tr>
      <th>88</th>
      <td>-1.004030</td>
      <td>-1.865177</td>
      <td>-0.342262</td>
    </tr>
    <tr>
      <th>89</th>
      <td>1.718531</td>
      <td>-0.419141</td>
      <td>-1.190334</td>
    </tr>
    <tr>
      <th>90</th>
      <td>-1.586579</td>
      <td>-0.452029</td>
      <td>-1.717858</td>
    </tr>
    <tr>
      <th>91</th>
      <td>0.619875</td>
      <td>-0.913514</td>
      <td>-0.642626</td>
    </tr>
    <tr>
      <th>92</th>
      <td>0.463219</td>
      <td>-0.272244</td>
      <td>0.166245</td>
    </tr>
    <tr>
      <th>93</th>
      <td>-1.267858</td>
      <td>-1.868737</td>
      <td>0.174040</td>
    </tr>
    <tr>
      <th>94</th>
      <td>-0.346080</td>
      <td>0.715584</td>
      <td>1.688834</td>
    </tr>
    <tr>
      <th>95</th>
      <td>-0.554673</td>
      <td>0.806156</td>
      <td>-0.757331</td>
    </tr>
    <tr>
      <th>96</th>
      <td>-0.349220</td>
      <td>-0.274901</td>
      <td>-1.190019</td>
    </tr>
    <tr>
      <th>97</th>
      <td>1.204126</td>
      <td>-0.134090</td>
      <td>-2.924324</td>
    </tr>
    <tr>
      <th>98</th>
      <td>-0.017631</td>
      <td>0.360200</td>
      <td>-0.189692</td>
    </tr>
    <tr>
      <th>99</th>
      <td>1.257691</td>
      <td>0.037950</td>
      <td>0.198003</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 3 columns</p>
</div>



```python
# 使用DataFrame的关系运算函数 gt(other, axis=0)
# 从d中删除某一行中每一个元素的值大于这一行的所有数值标准差的3倍的行
d.drop(index=d[d.gt(3*d.std(axis=1), axis=0).any(axis=1)].index)
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
      <td>-1.164291</td>
      <td>0.797137</td>
      <td>-0.251975</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.201639</td>
      <td>-1.886578</td>
      <td>-1.352991</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.956560</td>
      <td>0.253978</td>
      <td>0.190281</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.106657</td>
      <td>0.791620</td>
      <td>-0.805228</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.964321</td>
      <td>0.545341</td>
      <td>-2.175794</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.044096</td>
      <td>-0.235177</td>
      <td>0.492157</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.500263</td>
      <td>-1.430520</td>
      <td>1.048750</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.293912</td>
      <td>0.896059</td>
      <td>-0.109282</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.464239</td>
      <td>-0.281743</td>
      <td>-0.712988</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-0.370665</td>
      <td>2.277106</td>
      <td>-1.424837</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.154458</td>
      <td>0.059086</td>
      <td>-0.115698</td>
    </tr>
    <tr>
      <th>11</th>
      <td>-0.265803</td>
      <td>0.160085</td>
      <td>-0.170685</td>
    </tr>
    <tr>
      <th>12</th>
      <td>-0.730650</td>
      <td>-0.109982</td>
      <td>-0.463942</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.201926</td>
      <td>1.263386</td>
      <td>0.629739</td>
    </tr>
    <tr>
      <th>14</th>
      <td>-2.177481</td>
      <td>-0.188986</td>
      <td>1.411646</td>
    </tr>
    <tr>
      <th>15</th>
      <td>-1.228296</td>
      <td>0.980455</td>
      <td>-1.354884</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-0.664823</td>
      <td>0.268899</td>
      <td>1.012338</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-0.190291</td>
      <td>-1.078339</td>
      <td>-0.456569</td>
    </tr>
    <tr>
      <th>18</th>
      <td>-0.108290</td>
      <td>-0.070409</td>
      <td>0.803164</td>
    </tr>
    <tr>
      <th>19</th>
      <td>0.887057</td>
      <td>-1.473393</td>
      <td>-1.126295</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1.057284</td>
      <td>0.010266</td>
      <td>1.677125</td>
    </tr>
    <tr>
      <th>21</th>
      <td>0.467551</td>
      <td>0.610109</td>
      <td>2.110309</td>
    </tr>
    <tr>
      <th>22</th>
      <td>-1.536377</td>
      <td>1.084455</td>
      <td>-0.134929</td>
    </tr>
    <tr>
      <th>23</th>
      <td>-0.335276</td>
      <td>1.242639</td>
      <td>-0.912711</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1.579240</td>
      <td>-0.077694</td>
      <td>0.960719</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2.334651</td>
      <td>1.118378</td>
      <td>-0.584885</td>
    </tr>
    <tr>
      <th>26</th>
      <td>-0.878469</td>
      <td>0.575112</td>
      <td>0.753077</td>
    </tr>
    <tr>
      <th>27</th>
      <td>-0.886514</td>
      <td>-1.596037</td>
      <td>-0.579165</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1.419417</td>
      <td>-2.660823</td>
      <td>-1.545299</td>
    </tr>
    <tr>
      <th>29</th>
      <td>-0.460868</td>
      <td>-0.773910</td>
      <td>0.617897</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>70</th>
      <td>0.324589</td>
      <td>-1.538287</td>
      <td>1.675682</td>
    </tr>
    <tr>
      <th>71</th>
      <td>-0.584616</td>
      <td>-0.489804</td>
      <td>0.885449</td>
    </tr>
    <tr>
      <th>72</th>
      <td>-0.158786</td>
      <td>0.432890</td>
      <td>-1.351910</td>
    </tr>
    <tr>
      <th>73</th>
      <td>-0.677642</td>
      <td>0.284412</td>
      <td>1.542141</td>
    </tr>
    <tr>
      <th>74</th>
      <td>1.197553</td>
      <td>-1.480051</td>
      <td>0.707695</td>
    </tr>
    <tr>
      <th>75</th>
      <td>0.866642</td>
      <td>-2.166048</td>
      <td>2.007399</td>
    </tr>
    <tr>
      <th>76</th>
      <td>1.342749</td>
      <td>-0.948632</td>
      <td>0.017686</td>
    </tr>
    <tr>
      <th>77</th>
      <td>1.211767</td>
      <td>1.790328</td>
      <td>-0.384149</td>
    </tr>
    <tr>
      <th>78</th>
      <td>-1.196269</td>
      <td>0.066043</td>
      <td>-1.108524</td>
    </tr>
    <tr>
      <th>79</th>
      <td>0.257693</td>
      <td>0.941103</td>
      <td>-0.352873</td>
    </tr>
    <tr>
      <th>80</th>
      <td>0.085246</td>
      <td>-0.644327</td>
      <td>0.171741</td>
    </tr>
    <tr>
      <th>81</th>
      <td>0.952371</td>
      <td>-0.411009</td>
      <td>-1.553032</td>
    </tr>
    <tr>
      <th>82</th>
      <td>-0.575233</td>
      <td>1.195594</td>
      <td>-0.838789</td>
    </tr>
    <tr>
      <th>83</th>
      <td>-0.666920</td>
      <td>-0.361069</td>
      <td>0.384706</td>
    </tr>
    <tr>
      <th>84</th>
      <td>-0.766464</td>
      <td>1.255243</td>
      <td>0.399759</td>
    </tr>
    <tr>
      <th>85</th>
      <td>-2.505601</td>
      <td>-0.940245</td>
      <td>-0.250290</td>
    </tr>
    <tr>
      <th>86</th>
      <td>0.136244</td>
      <td>-0.984630</td>
      <td>0.148026</td>
    </tr>
    <tr>
      <th>87</th>
      <td>-0.639923</td>
      <td>-0.485517</td>
      <td>-0.117722</td>
    </tr>
    <tr>
      <th>88</th>
      <td>-1.004030</td>
      <td>-1.865177</td>
      <td>-0.342262</td>
    </tr>
    <tr>
      <th>89</th>
      <td>1.718531</td>
      <td>-0.419141</td>
      <td>-1.190334</td>
    </tr>
    <tr>
      <th>90</th>
      <td>-1.586579</td>
      <td>-0.452029</td>
      <td>-1.717858</td>
    </tr>
    <tr>
      <th>91</th>
      <td>0.619875</td>
      <td>-0.913514</td>
      <td>-0.642626</td>
    </tr>
    <tr>
      <th>92</th>
      <td>0.463219</td>
      <td>-0.272244</td>
      <td>0.166245</td>
    </tr>
    <tr>
      <th>93</th>
      <td>-1.267858</td>
      <td>-1.868737</td>
      <td>0.174040</td>
    </tr>
    <tr>
      <th>94</th>
      <td>-0.346080</td>
      <td>0.715584</td>
      <td>1.688834</td>
    </tr>
    <tr>
      <th>95</th>
      <td>-0.554673</td>
      <td>0.806156</td>
      <td>-0.757331</td>
    </tr>
    <tr>
      <th>96</th>
      <td>-0.349220</td>
      <td>-0.274901</td>
      <td>-1.190019</td>
    </tr>
    <tr>
      <th>97</th>
      <td>1.204126</td>
      <td>-0.134090</td>
      <td>-2.924324</td>
    </tr>
    <tr>
      <th>98</th>
      <td>-0.017631</td>
      <td>0.360200</td>
      <td>-0.189692</td>
    </tr>
    <tr>
      <th>99</th>
      <td>1.257691</td>
      <td>0.037950</td>
      <td>0.198003</td>
    </tr>
  </tbody>
</table>
<p>94 rows × 3 columns</p>
</div>



### 排列

- df.take() 按索引位置提取行或列的数据

```python
# axis=0 按行索引
d.take([0, 3, 4], axis=0) # 获取指定索引的数据
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
      <td>-1.164291</td>
      <td>0.797137</td>
      <td>-0.251975</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.106657</td>
      <td>0.791620</td>
      <td>-0.805228</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.964321</td>
      <td>0.545341</td>
      <td>-2.175794</td>
    </tr>
  </tbody>
</table>
</div>




```python
# axis=1 按列索引
d.take([2, 0], axis=1)  # 使用的是列的索引
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
      <th>C</th>
      <th>A</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.251975</td>
      <td>-1.164291</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.352991</td>
      <td>0.201639</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.190281</td>
      <td>-0.956560</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.805228</td>
      <td>-0.106657</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-2.175794</td>
      <td>0.964321</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.492157</td>
      <td>0.044096</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1.048750</td>
      <td>-0.500263</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.109282</td>
      <td>-0.293912</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-0.712988</td>
      <td>0.464239</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-1.424837</td>
      <td>-0.370665</td>
    </tr>
    <tr>
      <th>10</th>
      <td>-0.115698</td>
      <td>0.154458</td>
    </tr>
    <tr>
      <th>11</th>
      <td>-0.170685</td>
      <td>-0.265803</td>
    </tr>
    <tr>
      <th>12</th>
      <td>-0.463942</td>
      <td>-0.730650</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.629739</td>
      <td>0.201926</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1.411646</td>
      <td>-2.177481</td>
    </tr>
    <tr>
      <th>15</th>
      <td>-1.354884</td>
      <td>-1.228296</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1.012338</td>
      <td>-0.664823</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-0.456569</td>
      <td>-0.190291</td>
    </tr>
    <tr>
      <th>18</th>
      <td>0.803164</td>
      <td>-0.108290</td>
    </tr>
    <tr>
      <th>19</th>
      <td>-1.126295</td>
      <td>0.887057</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1.677125</td>
      <td>1.057284</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2.110309</td>
      <td>0.467551</td>
    </tr>
    <tr>
      <th>22</th>
      <td>-0.134929</td>
      <td>-1.536377</td>
    </tr>
    <tr>
      <th>23</th>
      <td>-0.912711</td>
      <td>-0.335276</td>
    </tr>
    <tr>
      <th>24</th>
      <td>0.960719</td>
      <td>1.579240</td>
    </tr>
    <tr>
      <th>25</th>
      <td>-0.584885</td>
      <td>2.334651</td>
    </tr>
    <tr>
      <th>26</th>
      <td>0.753077</td>
      <td>-0.878469</td>
    </tr>
    <tr>
      <th>27</th>
      <td>-0.579165</td>
      <td>-0.886514</td>
    </tr>
    <tr>
      <th>28</th>
      <td>-1.545299</td>
      <td>1.419417</td>
    </tr>
    <tr>
      <th>29</th>
      <td>0.617897</td>
      <td>-0.460868</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>70</th>
      <td>1.675682</td>
      <td>0.324589</td>
    </tr>
    <tr>
      <th>71</th>
      <td>0.885449</td>
      <td>-0.584616</td>
    </tr>
    <tr>
      <th>72</th>
      <td>-1.351910</td>
      <td>-0.158786</td>
    </tr>
    <tr>
      <th>73</th>
      <td>1.542141</td>
      <td>-0.677642</td>
    </tr>
    <tr>
      <th>74</th>
      <td>0.707695</td>
      <td>1.197553</td>
    </tr>
    <tr>
      <th>75</th>
      <td>2.007399</td>
      <td>0.866642</td>
    </tr>
    <tr>
      <th>76</th>
      <td>0.017686</td>
      <td>1.342749</td>
    </tr>
    <tr>
      <th>77</th>
      <td>-0.384149</td>
      <td>1.211767</td>
    </tr>
    <tr>
      <th>78</th>
      <td>-1.108524</td>
      <td>-1.196269</td>
    </tr>
    <tr>
      <th>79</th>
      <td>-0.352873</td>
      <td>0.257693</td>
    </tr>
    <tr>
      <th>80</th>
      <td>0.171741</td>
      <td>0.085246</td>
    </tr>
    <tr>
      <th>81</th>
      <td>-1.553032</td>
      <td>0.952371</td>
    </tr>
    <tr>
      <th>82</th>
      <td>-0.838789</td>
      <td>-0.575233</td>
    </tr>
    <tr>
      <th>83</th>
      <td>0.384706</td>
      <td>-0.666920</td>
    </tr>
    <tr>
      <th>84</th>
      <td>0.399759</td>
      <td>-0.766464</td>
    </tr>
    <tr>
      <th>85</th>
      <td>-0.250290</td>
      <td>-2.505601</td>
    </tr>
    <tr>
      <th>86</th>
      <td>0.148026</td>
      <td>0.136244</td>
    </tr>
    <tr>
      <th>87</th>
      <td>-0.117722</td>
      <td>-0.639923</td>
    </tr>
    <tr>
      <th>88</th>
      <td>-0.342262</td>
      <td>-1.004030</td>
    </tr>
    <tr>
      <th>89</th>
      <td>-1.190334</td>
      <td>1.718531</td>
    </tr>
    <tr>
      <th>90</th>
      <td>-1.717858</td>
      <td>-1.586579</td>
    </tr>
    <tr>
      <th>91</th>
      <td>-0.642626</td>
      <td>0.619875</td>
    </tr>
    <tr>
      <th>92</th>
      <td>0.166245</td>
      <td>0.463219</td>
    </tr>
    <tr>
      <th>93</th>
      <td>0.174040</td>
      <td>-1.267858</td>
    </tr>
    <tr>
      <th>94</th>
      <td>1.688834</td>
      <td>-0.346080</td>
    </tr>
    <tr>
      <th>95</th>
      <td>-0.757331</td>
      <td>-0.554673</td>
    </tr>
    <tr>
      <th>96</th>
      <td>-1.190019</td>
      <td>-0.349220</td>
    </tr>
    <tr>
      <th>97</th>
      <td>-2.924324</td>
      <td>1.204126</td>
    </tr>
    <tr>
      <th>98</th>
      <td>-0.189692</td>
      <td>-0.017631</td>
    </tr>
    <tr>
      <th>99</th>
      <td>0.198003</td>
      <td>1.257691</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 2 columns</p>
</div>



```python
np.random.permutation(d)  # 行索引随机排列
```



```
array([[-1.53637673,  1.08445526, -0.13492947],
       [-0.10665737,  0.79161967, -0.80522752],
       [-0.67764199,  0.28441236,  1.542141  ],
       [ 1.34274858, -0.94863236,  0.0176861 ],
       [ 0.88705681, -1.47339335, -1.12629525],
       [ 0.08524615, -0.64432748,  0.17174129],
       [-1.07621935, -1.52843328, -0.51188344],
       [ 1.19755344, -1.48005054,  0.70769501],
       [-0.66482255,  0.26889936,  1.01233848],
       [ 0.25271899,  0.16765991,  0.20635153],
       [-0.58461607, -0.48980375,  0.88544903],
       [ 2.33465136,  1.11837819, -0.58488493],
       [-0.87846901,  0.57511178,  0.75307679],
       [ 2.92324165,  0.23942027,  0.28790037],
       [ 0.46321869, -0.2722443 ,  0.16624544],
       [ 1.57924003, -0.07769439,  0.9607191 ],
       [ 0.14866542,  1.55298961,  0.97487729],
       [-1.58657871, -0.45202914, -1.71785795],
       [ 0.75153559,  0.35419736,  0.88669576],
       [-0.25898061, -0.17926159, -0.20883057],
       [ 0.76417317, -1.56947926,  0.21653596],
       [-0.19029146, -1.07833877, -0.45656882],
       [ 0.27379659, -1.25839717, -0.20598106],
       [-0.40163904, -0.33021426, -1.13700141],
       [-0.31895677, -3.1063322 ,  0.47571046],
       [-0.37066453,  2.27710577, -1.42483707],
       [-1.17863968, -1.86884747, -0.56859643],
       [ 1.7185307 , -0.41914124, -1.1903335 ],
       [ 0.46423907, -0.28174321, -0.71298846],
       [ 0.66578421,  0.49131552,  0.73192933],
       [ 0.25769286,  0.94110296, -0.35287332],
       [-1.26785792, -1.86873657,  0.17404006],
       [ 0.04409576, -0.23517703,  0.49215674],
       [-0.29570943,  0.40474328, -0.23005976],
       [-2.50560146, -0.94024531, -0.25029039],
       [ 1.05728399,  0.01026643,  1.677125  ],
       [ 0.3245894 , -1.53828668,  1.67568232],
       [ 0.87221377,  1.19484678,  0.18824794],
       [-0.63992255, -0.48551672, -0.11772157],
       [-0.46086836, -0.77391013,  0.61789665],
       [-1.19626944,  0.06604291, -1.10852433],
       [ 1.20412601, -0.13408964, -2.92432368],
       [-1.0040302 , -1.86517743, -0.34226164],
       [ 0.74529943, -1.43741424,  0.76660628],
       [-1.17297346, -1.00213529, -1.00705225],
       [-0.04418469,  0.70220937,  1.34609585],
       [ 0.61987487, -0.91351381, -0.64262553],
       [-0.34921995, -0.27490071, -1.19001899],
       [-0.48349277, -2.21230522,  0.75348734],
       [-0.66177152,  1.39698582, -0.70344233],
       [ 0.46755078,  0.61010902,  2.11030856],
       [-0.03656433, -0.32166214, -0.53643193],
       [ 1.21176722,  1.79032819, -0.38414932],
       [ 1.41941704, -2.66082277, -1.54529942],
       [-0.33527593,  1.24263909, -0.91271137],
       [ 0.8821974 , -0.792584  , -0.4603104 ],
       [-0.8144514 , -2.5224221 , -0.74103789],
       [-0.95655992,  0.25397797,  0.19028136],
       [-2.17748081, -0.18898619,  1.41164612],
       [-0.57523277,  1.19559379, -0.83878902],
       [ 1.03460475, -0.71565665, -0.11342188],
       [-1.2282959 ,  0.98045534, -1.35488367],
       [-0.55467295,  0.80615552, -0.75733098],
       [-0.23822131,  0.37780076,  0.34689632],
       [-0.34608   ,  0.71558374,  1.68883422],
       [ 1.21525054, -0.33618904,  1.32922366],
       [-0.50037052,  2.29273735,  0.20962005],
       [ 2.86203218, -0.85041155, -1.28144286],
       [-0.01763088,  0.36019972, -0.1896925 ],
       [-0.66692035, -0.36106907,  0.38470566],
       [ 0.8666419 , -2.16604795,  2.00739915],
       [ 0.96432056,  0.5453409 , -2.17579431],
       [ 0.67369366,  0.08077827,  2.5005612 ],
       [-1.16429123,  0.79713727, -0.25197537],
       [-0.2939124 ,  0.89605861, -0.10928228],
       [ 0.20163915, -1.88657785, -1.35299109],
       [ 1.40667152,  0.8492366 ,  0.59121519],
       [ 1.25769127,  0.03794971,  0.19800272],
       [-1.58991563, -0.13940638,  1.57186172],
       [ 0.15445805,  0.05908573, -0.11569776],
       [ 0.95237121, -0.41100879, -1.5530315 ],
       [-0.54598302,  0.75780254,  1.46904955],
       [-0.10828954, -0.07040856,  0.80316361],
       [-0.50026256, -1.43052028,  1.04875044],
       [ 0.36532874,  0.31554344,  0.80914269],
       [-0.46564749,  1.67776276,  1.20278925],
       [-0.15878616,  0.43289021, -1.35191002],
       [ 0.69994909,  1.27138114,  1.43294663],
       [ 0.15374554, -0.0955892 ,  0.30035091],
       [-0.26580255,  0.16008549, -0.17068522],
       [ 0.17722122, -0.41482462,  0.27209482],
       [ 0.13624352, -0.98462975,  0.14802624],
       [ 0.3062014 ,  0.23298596,  0.5700139 ],
       [-0.73064952, -0.10998176, -0.4639415 ],
       [-0.28404186, -0.75203351, -0.04664054],
       [-1.72127943, -0.42792277, -0.429139  ],
       [ 1.02690415,  1.27322693, -0.02700592],
       [-0.88651406, -1.5960373 , -0.57916499],
       [ 0.20192568,  1.26338595,  0.62973911],
       [-0.76646432,  1.25524314,  0.39975903]])
```



```python
d.take(np.random.permutation(d.index))
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
      <th>66</th>
      <td>0.952371</td>
      <td>-0.411009</td>
      <td>-1.553032</td>
    </tr>
    <tr>
      <th>84</th>
      <td>-0.584616</td>
      <td>-0.489804</td>
      <td>0.885449</td>
    </tr>
    <tr>
      <th>94</th>
      <td>0.464239</td>
      <td>-0.281743</td>
      <td>-0.712988</td>
    </tr>
    <tr>
      <th>19</th>
      <td>-1.589916</td>
      <td>-0.139406</td>
      <td>1.571862</td>
    </tr>
    <tr>
      <th>39</th>
      <td>0.467551</td>
      <td>0.610109</td>
      <td>2.110309</td>
    </tr>
    <tr>
      <th>26</th>
      <td>-0.265803</td>
      <td>0.160085</td>
      <td>-0.170685</td>
    </tr>
    <tr>
      <th>35</th>
      <td>2.862032</td>
      <td>-0.850412</td>
      <td>-1.281443</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.664823</td>
      <td>0.268899</td>
      <td>1.012338</td>
    </tr>
    <tr>
      <th>28</th>
      <td>-0.346080</td>
      <td>0.715584</td>
      <td>1.688834</td>
    </tr>
    <tr>
      <th>44</th>
      <td>-0.036564</td>
      <td>-0.321662</td>
      <td>-0.536432</td>
    </tr>
    <tr>
      <th>63</th>
      <td>-0.370665</td>
      <td>2.277106</td>
      <td>-1.424837</td>
    </tr>
    <tr>
      <th>24</th>
      <td>-0.878469</td>
      <td>0.575112</td>
      <td>0.753077</td>
    </tr>
    <tr>
      <th>37</th>
      <td>0.201926</td>
      <td>1.263386</td>
      <td>0.629739</td>
    </tr>
    <tr>
      <th>88</th>
      <td>0.252719</td>
      <td>0.167660</td>
      <td>0.206352</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-0.293912</td>
      <td>0.896059</td>
      <td>-0.109282</td>
    </tr>
    <tr>
      <th>56</th>
      <td>-0.677642</td>
      <td>0.284412</td>
      <td>1.542141</td>
    </tr>
    <tr>
      <th>68</th>
      <td>-0.106657</td>
      <td>0.791620</td>
      <td>-0.805228</td>
    </tr>
    <tr>
      <th>27</th>
      <td>0.764173</td>
      <td>-1.569479</td>
      <td>0.216536</td>
    </tr>
    <tr>
      <th>92</th>
      <td>-0.554673</td>
      <td>0.806156</td>
      <td>-0.757331</td>
    </tr>
    <tr>
      <th>95</th>
      <td>-0.108290</td>
      <td>-0.070409</td>
      <td>0.803164</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0.136244</td>
      <td>-0.984630</td>
      <td>0.148026</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.882197</td>
      <td>-0.792584</td>
      <td>-0.460310</td>
    </tr>
    <tr>
      <th>59</th>
      <td>1.406672</td>
      <td>0.849237</td>
      <td>0.591215</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.365329</td>
      <td>0.315543</td>
      <td>0.809143</td>
    </tr>
    <tr>
      <th>61</th>
      <td>0.324589</td>
      <td>-1.538287</td>
      <td>1.675682</td>
    </tr>
    <tr>
      <th>36</th>
      <td>-0.814451</td>
      <td>-2.522422</td>
      <td>-0.741038</td>
    </tr>
    <tr>
      <th>70</th>
      <td>1.579240</td>
      <td>-0.077694</td>
      <td>0.960719</td>
    </tr>
    <tr>
      <th>80</th>
      <td>1.211767</td>
      <td>1.790328</td>
      <td>-0.384149</td>
    </tr>
    <tr>
      <th>86</th>
      <td>1.057284</td>
      <td>0.010266</td>
      <td>1.677125</td>
    </tr>
    <tr>
      <th>42</th>
      <td>-1.076219</td>
      <td>-1.528433</td>
      <td>-0.511883</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>78</th>
      <td>0.148665</td>
      <td>1.552990</td>
      <td>0.974877</td>
    </tr>
    <tr>
      <th>29</th>
      <td>-0.766464</td>
      <td>1.255243</td>
      <td>0.399759</td>
    </tr>
    <tr>
      <th>30</th>
      <td>-0.190291</td>
      <td>-1.078339</td>
      <td>-0.456569</td>
    </tr>
    <tr>
      <th>93</th>
      <td>0.745299</td>
      <td>-1.437414</td>
      <td>0.766606</td>
    </tr>
    <tr>
      <th>79</th>
      <td>0.866642</td>
      <td>-2.166048</td>
      <td>2.007399</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.257693</td>
      <td>0.941103</td>
      <td>-0.352873</td>
    </tr>
    <tr>
      <th>96</th>
      <td>1.257691</td>
      <td>0.037950</td>
      <td>0.198003</td>
    </tr>
    <tr>
      <th>50</th>
      <td>0.085246</td>
      <td>-0.644327</td>
      <td>0.171741</td>
    </tr>
    <tr>
      <th>57</th>
      <td>1.026904</td>
      <td>1.273227</td>
      <td>-0.027006</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-0.956560</td>
      <td>0.253978</td>
      <td>0.190281</td>
    </tr>
    <tr>
      <th>90</th>
      <td>-0.483493</td>
      <td>-2.212305</td>
      <td>0.753487</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.665784</td>
      <td>0.491316</td>
      <td>0.731929</td>
    </tr>
    <tr>
      <th>47</th>
      <td>2.923242</td>
      <td>0.239420</td>
      <td>0.287900</td>
    </tr>
    <tr>
      <th>55</th>
      <td>1.718531</td>
      <td>-0.419141</td>
      <td>-1.190334</td>
    </tr>
    <tr>
      <th>64</th>
      <td>-0.460868</td>
      <td>-0.773910</td>
      <td>0.617897</td>
    </tr>
    <tr>
      <th>89</th>
      <td>-0.666920</td>
      <td>-0.361069</td>
      <td>0.384706</td>
    </tr>
    <tr>
      <th>81</th>
      <td>-1.164291</td>
      <td>0.797137</td>
      <td>-0.251975</td>
    </tr>
    <tr>
      <th>25</th>
      <td>0.177221</td>
      <td>-0.414825</td>
      <td>0.272095</td>
    </tr>
    <tr>
      <th>32</th>
      <td>-0.335276</td>
      <td>1.242639</td>
      <td>-0.912711</td>
    </tr>
    <tr>
      <th>45</th>
      <td>0.273797</td>
      <td>-1.258397</td>
      <td>-0.205981</td>
    </tr>
    <tr>
      <th>41</th>
      <td>-0.639923</td>
      <td>-0.485517</td>
      <td>-0.117722</td>
    </tr>
    <tr>
      <th>33</th>
      <td>0.673694</td>
      <td>0.080778</td>
      <td>2.500561</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-0.158786</td>
      <td>0.432890</td>
      <td>-1.351910</td>
    </tr>
    <tr>
      <th>40</th>
      <td>-0.017631</td>
      <td>0.360200</td>
      <td>-0.189692</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1.419417</td>
      <td>-2.660823</td>
      <td>-1.545299</td>
    </tr>
    <tr>
      <th>72</th>
      <td>0.463219</td>
      <td>-0.272244</td>
      <td>0.166245</td>
    </tr>
    <tr>
      <th>85</th>
      <td>1.204126</td>
      <td>-0.134090</td>
      <td>-2.924324</td>
    </tr>
    <tr>
      <th>83</th>
      <td>-2.505601</td>
      <td>-0.940245</td>
      <td>-0.250290</td>
    </tr>
    <tr>
      <th>62</th>
      <td>-0.401639</td>
      <td>-0.330214</td>
      <td>-1.137001</td>
    </tr>
    <tr>
      <th>97</th>
      <td>-0.349220</td>
      <td>-0.274901</td>
      <td>-1.190019</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 3 columns</p>
</div>



```python
d[np.random.permutation(d.columns)]
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
      <td>-1.164291</td>
      <td>0.797137</td>
      <td>-0.251975</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.201639</td>
      <td>-1.886578</td>
      <td>-1.352991</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.956560</td>
      <td>0.253978</td>
      <td>0.190281</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.106657</td>
      <td>0.791620</td>
      <td>-0.805228</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.964321</td>
      <td>0.545341</td>
      <td>-2.175794</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.044096</td>
      <td>-0.235177</td>
      <td>0.492157</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.500263</td>
      <td>-1.430520</td>
      <td>1.048750</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.293912</td>
      <td>0.896059</td>
      <td>-0.109282</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.464239</td>
      <td>-0.281743</td>
      <td>-0.712988</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-0.370665</td>
      <td>2.277106</td>
      <td>-1.424837</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.154458</td>
      <td>0.059086</td>
      <td>-0.115698</td>
    </tr>
    <tr>
      <th>11</th>
      <td>-0.265803</td>
      <td>0.160085</td>
      <td>-0.170685</td>
    </tr>
    <tr>
      <th>12</th>
      <td>-0.730650</td>
      <td>-0.109982</td>
      <td>-0.463942</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.201926</td>
      <td>1.263386</td>
      <td>0.629739</td>
    </tr>
    <tr>
      <th>14</th>
      <td>-2.177481</td>
      <td>-0.188986</td>
      <td>1.411646</td>
    </tr>
    <tr>
      <th>15</th>
      <td>-1.228296</td>
      <td>0.980455</td>
      <td>-1.354884</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-0.664823</td>
      <td>0.268899</td>
      <td>1.012338</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-0.190291</td>
      <td>-1.078339</td>
      <td>-0.456569</td>
    </tr>
    <tr>
      <th>18</th>
      <td>-0.108290</td>
      <td>-0.070409</td>
      <td>0.803164</td>
    </tr>
    <tr>
      <th>19</th>
      <td>0.887057</td>
      <td>-1.473393</td>
      <td>-1.126295</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1.057284</td>
      <td>0.010266</td>
      <td>1.677125</td>
    </tr>
    <tr>
      <th>21</th>
      <td>0.467551</td>
      <td>0.610109</td>
      <td>2.110309</td>
    </tr>
    <tr>
      <th>22</th>
      <td>-1.536377</td>
      <td>1.084455</td>
      <td>-0.134929</td>
    </tr>
    <tr>
      <th>23</th>
      <td>-0.335276</td>
      <td>1.242639</td>
      <td>-0.912711</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1.579240</td>
      <td>-0.077694</td>
      <td>0.960719</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2.334651</td>
      <td>1.118378</td>
      <td>-0.584885</td>
    </tr>
    <tr>
      <th>26</th>
      <td>-0.878469</td>
      <td>0.575112</td>
      <td>0.753077</td>
    </tr>
    <tr>
      <th>27</th>
      <td>-0.886514</td>
      <td>-1.596037</td>
      <td>-0.579165</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1.419417</td>
      <td>-2.660823</td>
      <td>-1.545299</td>
    </tr>
    <tr>
      <th>29</th>
      <td>-0.460868</td>
      <td>-0.773910</td>
      <td>0.617897</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>70</th>
      <td>0.324589</td>
      <td>-1.538287</td>
      <td>1.675682</td>
    </tr>
    <tr>
      <th>71</th>
      <td>-0.584616</td>
      <td>-0.489804</td>
      <td>0.885449</td>
    </tr>
    <tr>
      <th>72</th>
      <td>-0.158786</td>
      <td>0.432890</td>
      <td>-1.351910</td>
    </tr>
    <tr>
      <th>73</th>
      <td>-0.677642</td>
      <td>0.284412</td>
      <td>1.542141</td>
    </tr>
    <tr>
      <th>74</th>
      <td>1.197553</td>
      <td>-1.480051</td>
      <td>0.707695</td>
    </tr>
    <tr>
      <th>75</th>
      <td>0.866642</td>
      <td>-2.166048</td>
      <td>2.007399</td>
    </tr>
    <tr>
      <th>76</th>
      <td>1.342749</td>
      <td>-0.948632</td>
      <td>0.017686</td>
    </tr>
    <tr>
      <th>77</th>
      <td>1.211767</td>
      <td>1.790328</td>
      <td>-0.384149</td>
    </tr>
    <tr>
      <th>78</th>
      <td>-1.196269</td>
      <td>0.066043</td>
      <td>-1.108524</td>
    </tr>
    <tr>
      <th>79</th>
      <td>0.257693</td>
      <td>0.941103</td>
      <td>-0.352873</td>
    </tr>
    <tr>
      <th>80</th>
      <td>0.085246</td>
      <td>-0.644327</td>
      <td>0.171741</td>
    </tr>
    <tr>
      <th>81</th>
      <td>0.952371</td>
      <td>-0.411009</td>
      <td>-1.553032</td>
    </tr>
    <tr>
      <th>82</th>
      <td>-0.575233</td>
      <td>1.195594</td>
      <td>-0.838789</td>
    </tr>
    <tr>
      <th>83</th>
      <td>-0.666920</td>
      <td>-0.361069</td>
      <td>0.384706</td>
    </tr>
    <tr>
      <th>84</th>
      <td>-0.766464</td>
      <td>1.255243</td>
      <td>0.399759</td>
    </tr>
    <tr>
      <th>85</th>
      <td>-2.505601</td>
      <td>-0.940245</td>
      <td>-0.250290</td>
    </tr>
    <tr>
      <th>86</th>
      <td>0.136244</td>
      <td>-0.984630</td>
      <td>0.148026</td>
    </tr>
    <tr>
      <th>87</th>
      <td>-0.639923</td>
      <td>-0.485517</td>
      <td>-0.117722</td>
    </tr>
    <tr>
      <th>88</th>
      <td>-1.004030</td>
      <td>-1.865177</td>
      <td>-0.342262</td>
    </tr>
    <tr>
      <th>89</th>
      <td>1.718531</td>
      <td>-0.419141</td>
      <td>-1.190334</td>
    </tr>
    <tr>
      <th>90</th>
      <td>-1.586579</td>
      <td>-0.452029</td>
      <td>-1.717858</td>
    </tr>
    <tr>
      <th>91</th>
      <td>0.619875</td>
      <td>-0.913514</td>
      <td>-0.642626</td>
    </tr>
    <tr>
      <th>92</th>
      <td>0.463219</td>
      <td>-0.272244</td>
      <td>0.166245</td>
    </tr>
    <tr>
      <th>93</th>
      <td>-1.267858</td>
      <td>-1.868737</td>
      <td>0.174040</td>
    </tr>
    <tr>
      <th>94</th>
      <td>-0.346080</td>
      <td>0.715584</td>
      <td>1.688834</td>
    </tr>
    <tr>
      <th>95</th>
      <td>-0.554673</td>
      <td>0.806156</td>
      <td>-0.757331</td>
    </tr>
    <tr>
      <th>96</th>
      <td>-0.349220</td>
      <td>-0.274901</td>
      <td>-1.190019</td>
    </tr>
    <tr>
      <th>97</th>
      <td>1.204126</td>
      <td>-0.134090</td>
      <td>-2.924324</td>
    </tr>
    <tr>
      <th>98</th>
      <td>-0.017631</td>
      <td>0.360200</td>
      <td>-0.189692</td>
    </tr>
    <tr>
      <th>99</th>
      <td>1.257691</td>
      <td>0.037950</td>
      <td>0.198003</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 3 columns</p>
</div>



### 数据分类

- groupby()

练习：
假设菜市场张大妈在卖菜，有以下属性：
菜品(item)：萝卜，白菜，辣椒，冬瓜
颜色(color)：白，青，红
重量(weight)
价格(price)
要求以属性作为列索引，新建一个df = DataFrame
对df进行聚合操作，求出颜色为白色的价格总和
对df进行聚合操作，求出萝卜的所有重量(包括白萝卜，胡萝卜，青萝卜）以及平均价格

```python
df = DataFrame({
    'item': np.random.choice(['萝卜', '白菜', '辣椒', '冬瓜'], size=20),
    'color': np.random.choice(['白', '青', '红'], size=20),
    'weight': np.random.randint(1, 5, size=20),
    'price': np.round(np.random.uniform(1, 5, size=20), 1)
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
      <th>item</th>
      <th>color</th>
      <th>weight</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>白菜</td>
      <td>青</td>
      <td>4</td>
      <td>3.4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>辣椒</td>
      <td>青</td>
      <td>3</td>
      <td>3.3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>辣椒</td>
      <td>白</td>
      <td>4</td>
      <td>4.4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>辣椒</td>
      <td>红</td>
      <td>1</td>
      <td>1.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>辣椒</td>
      <td>白</td>
      <td>3</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>5</th>
      <td>冬瓜</td>
      <td>青</td>
      <td>2</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>萝卜</td>
      <td>红</td>
      <td>1</td>
      <td>3.8</td>
    </tr>
    <tr>
      <th>7</th>
      <td>冬瓜</td>
      <td>白</td>
      <td>3</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>白菜</td>
      <td>红</td>
      <td>3</td>
      <td>3.4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>萝卜</td>
      <td>红</td>
      <td>2</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>10</th>
      <td>白菜</td>
      <td>红</td>
      <td>2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>萝卜</td>
      <td>白</td>
      <td>2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>萝卜</td>
      <td>红</td>
      <td>4</td>
      <td>2.3</td>
    </tr>
    <tr>
      <th>13</th>
      <td>冬瓜</td>
      <td>青</td>
      <td>2</td>
      <td>2.7</td>
    </tr>
    <tr>
      <th>14</th>
      <td>萝卜</td>
      <td>青</td>
      <td>4</td>
      <td>4.8</td>
    </tr>
    <tr>
      <th>15</th>
      <td>冬瓜</td>
      <td>白</td>
      <td>1</td>
      <td>3.8</td>
    </tr>
    <tr>
      <th>16</th>
      <td>辣椒</td>
      <td>青</td>
      <td>4</td>
      <td>2.8</td>
    </tr>
    <tr>
      <th>17</th>
      <td>辣椒</td>
      <td>白</td>
      <td>4</td>
      <td>3.4</td>
    </tr>
    <tr>
      <th>18</th>
      <td>萝卜</td>
      <td>白</td>
      <td>2</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>19</th>
      <td>萝卜</td>
      <td>青</td>
      <td>3</td>
      <td>4.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('color') # 返回 DataFrameGroupBy 类对象
```



```
<pandas.core.groupby.groupby.DataFrameGroupBy object at 0x7fb8656ace10>
```



```python
df.groupby('color')['price'].sum() # 返回Series
```



```
color
白    25.9
红    17.5
青    24.5
Name: price, dtype: float64
```



```python
df.groupby('color')['price'].sum()['白']
```



```
25.9
```



```python
df.groupby('item')['weight'].sum()['萝卜']
```



```
18
```



```python
df.groupby('item')['price'].sum()['萝卜']
```



```
26.6
```



```python
def weight_price(item):
    # item -> Series表示每个品种的weight或price
    if item.name == 'weight':
        return item.sum()
    else:
        return item.mean()

```

```python
# item -> Series对象
# transform() 返回的行索引与原表的行索引保持一致
df2_w_p = df.groupby('item')['weight', 'price'].transform(weight_price)
df2_w_p.rename(columns={'weight': 'weight_total',
                       'price': 'price_mean'}, inplace=True)
```



```
pd.concat((df, df2_w_p), axis=1)
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
      <th>item</th>
      <th>color</th>
      <th>weight</th>
      <th>price</th>
      <th>weight_total</th>
      <th>price_mean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>白菜</td>
      <td>青</td>
      <td>4</td>
      <td>3.4</td>
      <td>9.0</td>
      <td>2.933333</td>
    </tr>
    <tr>
      <th>1</th>
      <td>辣椒</td>
      <td>青</td>
      <td>3</td>
      <td>3.3</td>
      <td>19.0</td>
      <td>3.333333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>辣椒</td>
      <td>白</td>
      <td>4</td>
      <td>4.4</td>
      <td>19.0</td>
      <td>3.333333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>辣椒</td>
      <td>红</td>
      <td>1</td>
      <td>1.4</td>
      <td>19.0</td>
      <td>3.333333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>辣椒</td>
      <td>白</td>
      <td>3</td>
      <td>4.7</td>
      <td>19.0</td>
      <td>3.333333</td>
    </tr>
    <tr>
      <th>5</th>
      <td>冬瓜</td>
      <td>青</td>
      <td>2</td>
      <td>3.0</td>
      <td>8.0</td>
      <td>3.125000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>萝卜</td>
      <td>红</td>
      <td>1</td>
      <td>3.8</td>
      <td>18.0</td>
      <td>3.800000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>冬瓜</td>
      <td>白</td>
      <td>3</td>
      <td>3.0</td>
      <td>8.0</td>
      <td>3.125000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>白菜</td>
      <td>红</td>
      <td>3</td>
      <td>3.4</td>
      <td>9.0</td>
      <td>2.933333</td>
    </tr>
    <tr>
      <th>9</th>
      <td>萝卜</td>
      <td>红</td>
      <td>2</td>
      <td>4.6</td>
      <td>18.0</td>
      <td>3.800000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>白菜</td>
      <td>红</td>
      <td>2</td>
      <td>2.0</td>
      <td>9.0</td>
      <td>2.933333</td>
    </tr>
    <tr>
      <th>11</th>
      <td>萝卜</td>
      <td>白</td>
      <td>2</td>
      <td>2.0</td>
      <td>18.0</td>
      <td>3.800000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>萝卜</td>
      <td>红</td>
      <td>4</td>
      <td>2.3</td>
      <td>18.0</td>
      <td>3.800000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>冬瓜</td>
      <td>青</td>
      <td>2</td>
      <td>2.7</td>
      <td>8.0</td>
      <td>3.125000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>萝卜</td>
      <td>青</td>
      <td>4</td>
      <td>4.8</td>
      <td>18.0</td>
      <td>3.800000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>冬瓜</td>
      <td>白</td>
      <td>1</td>
      <td>3.8</td>
      <td>8.0</td>
      <td>3.125000</td>
    </tr>
    <tr>
      <th>16</th>
      <td>辣椒</td>
      <td>青</td>
      <td>4</td>
      <td>2.8</td>
      <td>19.0</td>
      <td>3.333333</td>
    </tr>
    <tr>
      <th>17</th>
      <td>辣椒</td>
      <td>白</td>
      <td>4</td>
      <td>3.4</td>
      <td>19.0</td>
      <td>3.333333</td>
    </tr>
    <tr>
      <th>18</th>
      <td>萝卜</td>
      <td>白</td>
      <td>2</td>
      <td>4.6</td>
      <td>18.0</td>
      <td>3.800000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>萝卜</td>
      <td>青</td>
      <td>3</td>
      <td>4.5</td>
      <td>18.0</td>
      <td>3.800000</td>
    </tr>
  </tbody>
</table>
</div>




```python
def weight_price_2(item):
    # item -> DataFrame类型
    rs = DataFrame({'weight_total': item['weight'].sum(),
                   'price_mean': round(item['price'].mean(), 2)},
                  index=[''])
    return rs
```



```
# 返回结果， 默认情况是Series， 索引跟分组的品种保持一致

df.groupby('item')['weight', 'price'].apply(weight_price_2)
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
      <th>weight_total</th>
      <th>price_mean</th>
    </tr>
    <tr>
      <th>item</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>冬瓜</th>
      <th></th>
      <td>8</td>
      <td>3.12</td>
    </tr>
    <tr>
      <th>白菜</th>
      <th></th>
      <td>9</td>
      <td>2.93</td>
    </tr>
    <tr>
      <th>萝卜</th>
      <th></th>
      <td>18</td>
      <td>3.80</td>
    </tr>
    <tr>
      <th>辣椒</th>
      <th></th>
      <td>19</td>
      <td>3.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('item')['weight', 'price'].apply(weight_price_2).loc['萝卜']
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
      <th>weight_total</th>
      <th>price_mean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th></th>
      <td>18</td>
      <td>3.8</td>
    </tr>
  </tbody>
</table>
</div>




