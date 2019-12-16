---
title: Pandas的数据加载
comments: true
tags:
  - Python
  - 数据分析
categories:
  - 数据分析
date: 2019-05-06 13:29:58
---


```python
import pandas as pd
```

### 加载文本数据

- pd.read_csv()
- pd.read_table()

<!--more-->

```python
# 加载person.csv问价，分割符是‘；’
# sep 指定分隔符
persons = pd.read_csv('data2/persons.csv', sep=';')
persons.head()
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
      <th>Unnamed: 0</th>
      <th>age</th>
      <th>height</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>22</td>
      <td>159</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>19</td>
      <td>191</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>24</td>
      <td>189</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>21</td>
      <td>185</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>20</td>
      <td>231</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
persons.drop(columns='Unnamed: 0', inplace=True)
persons.head()
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
      <th>age</th>
      <th>height</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>22</td>
      <td>159</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>19</td>
      <td>191</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>24</td>
      <td>189</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>185</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20</td>
      <td>231</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 将列按 id, age, height的顺序显示
persons.take([2, 0, 1], axis=1).head()
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
      <th>id</th>
      <th>age</th>
      <th>height</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>22</td>
      <td>159</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>19</td>
      <td>191</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>24</td>
      <td>189</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>21</td>
      <td>185</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>20</td>
      <td>231</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 加载seeds.tsv文件， 分隔符是'\t'
# header=None 表示数据是无标题的
seeds = pd.read_csv('data2/seeds.tsv', sep='\t', header=None)
seeds.head()
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15.26</td>
      <td>14.84</td>
      <td>0.8710</td>
      <td>5.763</td>
      <td>3.312</td>
      <td>2.221</td>
      <td>5.220</td>
      <td>Kama</td>
    </tr>
    <tr>
      <th>1</th>
      <td>14.88</td>
      <td>14.57</td>
      <td>0.8811</td>
      <td>5.554</td>
      <td>3.333</td>
      <td>1.018</td>
      <td>4.956</td>
      <td>Kama</td>
    </tr>
    <tr>
      <th>2</th>
      <td>14.29</td>
      <td>14.09</td>
      <td>0.9050</td>
      <td>5.291</td>
      <td>3.337</td>
      <td>2.699</td>
      <td>4.825</td>
      <td>Kama</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13.84</td>
      <td>13.94</td>
      <td>0.8955</td>
      <td>5.324</td>
      <td>3.379</td>
      <td>2.259</td>
      <td>4.805</td>
      <td>Kama</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16.14</td>
      <td>14.99</td>
      <td>0.9034</td>
      <td>5.658</td>
      <td>3.562</td>
      <td>1.355</td>
      <td>5.175</td>
      <td>Kama</td>
    </tr>
  </tbody>
</table>
</div>




```python
# read_table()默认情况下读取的数据是以\t分隔的
seeds2 = pd.read_table('data2/seeds.tsv', header=None)
seeds2.head()
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15.26</td>
      <td>14.84</td>
      <td>0.8710</td>
      <td>5.763</td>
      <td>3.312</td>
      <td>2.221</td>
      <td>5.220</td>
      <td>Kama</td>
    </tr>
    <tr>
      <th>1</th>
      <td>14.88</td>
      <td>14.57</td>
      <td>0.8811</td>
      <td>5.554</td>
      <td>3.333</td>
      <td>1.018</td>
      <td>4.956</td>
      <td>Kama</td>
    </tr>
    <tr>
      <th>2</th>
      <td>14.29</td>
      <td>14.09</td>
      <td>0.9050</td>
      <td>5.291</td>
      <td>3.337</td>
      <td>2.699</td>
      <td>4.825</td>
      <td>Kama</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13.84</td>
      <td>13.94</td>
      <td>0.8955</td>
      <td>5.324</td>
      <td>3.379</td>
      <td>2.259</td>
      <td>4.805</td>
      <td>Kama</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16.14</td>
      <td>14.99</td>
      <td>0.9034</td>
      <td>5.658</td>
      <td>3.562</td>
      <td>1.355</td>
      <td>5.175</td>
      <td>Kama</td>
    </tr>
  </tbody>
</table>
</div>




### 加载excel的是数据文件

- pd.read_execl()

```python
# 加载students.xlsx数据文件
students = pd.read_excel('data2/students.xlsx')
students.head()
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
      <th>id</th>
      <th>name</th>
      <th>age</th>
      <th>sex</th>
      <th>height(cm)</th>
      <th>weight(kg)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>吴果</td>
      <td>20</td>
      <td>男</td>
      <td>165</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>李平</td>
      <td>33</td>
      <td>女</td>
      <td>158</td>
      <td>45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>王和</td>
      <td>21</td>
      <td>男</td>
      <td>179</td>
      <td>75</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>刘言</td>
      <td>27</td>
      <td>男</td>
      <td>180</td>
      <td>80</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>王平</td>
      <td>20</td>
      <td>女</td>
      <td>164</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 将students的id列设置为行索引
students.set_index('id')
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
      <th>name</th>
      <th>age</th>
      <th>sex</th>
      <th>height(cm)</th>
      <th>weight(kg)</th>
    </tr>
    <tr>
      <th>id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>吴果</td>
      <td>20</td>
      <td>男</td>
      <td>165</td>
      <td>50</td>
    </tr>
    <tr>
      <th>2</th>
      <td>李平</td>
      <td>33</td>
      <td>女</td>
      <td>158</td>
      <td>45</td>
    </tr>
    <tr>
      <th>3</th>
      <td>王和</td>
      <td>21</td>
      <td>男</td>
      <td>179</td>
      <td>75</td>
    </tr>
    <tr>
      <th>4</th>
      <td>刘言</td>
      <td>27</td>
      <td>男</td>
      <td>180</td>
      <td>80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>王平</td>
      <td>20</td>
      <td>女</td>
      <td>164</td>
      <td>82</td>
    </tr>
    <tr>
      <th>6</th>
      <td>宁国柱</td>
      <td>19</td>
      <td>男</td>
      <td>178</td>
      <td>85</td>
    </tr>
    <tr>
      <th>7</th>
      <td>刘佳敏</td>
      <td>25</td>
      <td>女</td>
      <td>183</td>
      <td>90</td>
    </tr>
    <tr>
      <th>8</th>
      <td>张先</td>
      <td>30</td>
      <td>女</td>
      <td>165</td>
      <td>55</td>
    </tr>
    <tr>
      <th>9</th>
      <td>刘四七</td>
      <td>27</td>
      <td>女</td>
      <td>170</td>
      <td>61</td>
    </tr>
    <tr>
      <th>10</th>
      <td>关小弟</td>
      <td>29</td>
      <td>男</td>
      <td>190</td>
      <td>94</td>
    </tr>
  </tbody>
</table>
</div>




### 加载sqlite3的数据文件

- pd.read_sql(sql,conn)

#### 1.连接sqlite3的数据库

```python
import sqlite3
```

```python
sqlite_conn = sqlite3.connect('data2/persons.db')
print('连接成功')
```

```
连接成功
```



```python
# 查看文件中，所有的表信息
pd.read_sql('select * from sqlite_master', sqlite_conn)
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
      <th>type</th>
      <th>name</th>
      <th>tbl_name</th>
      <th>rootpage</th>
      <th>sql</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>table</td>
      <td>person</td>
      <td>person</td>
      <td>2</td>
      <td>CREATE TABLE person(id,name,sex,age)</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 查看 db文件中person表的数据
pd.read_sql('select * from person', sqlite_conn)
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
      <th>id</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




#### sqlites3的数据库特点

- sqlite3主要用于小型设备中，如手机、平板、手表等智能设备上，也可以用于前端浏览器存储数据
- sqlite3 支持通用的sql语句
- sqlite3 没有特定的数据类型，具体的数据类型是根据开发语言来指定

```python
insert_sql = 'insert into person(id, name, age, sex) values(%s, %s, %s, %s)'
c = sqlite_conn.cursor()
# execute()函数中，不存在args参数
c.execute(insert_sql % (2, "'jack'", 20, "'女'"))
sqlite_conn.commit()
print('--insert ok--')
```

```
--insert ok--
```



```python
p1 = pd.read_sql('select * from person', sqlite_conn)
p1
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
      <th>id</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>jack</td>
      <td>女</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 将第二行数据 的id修改为3, name改为 rose, sex改为 女, age 改为19
p1.loc[1] = [3, 'rose', '女', 19]
p1
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
      <th>id</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>jack</td>
      <td>女</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>rose</td>
      <td>女</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 将修改后的DataFrame保存到数据库中
# if_exists = {'fail', 'replace', 'append'}
# index=False 不存储索引
p1.to_sql('person', sqlite_conn, if_exists='replace', index=False)
```

```python
pd.read_sql('select * from person', sqlite_conn)
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
      <th>id</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>jack</td>
      <td>女</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>rose</td>
      <td>女</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




### 加载mysql数据库中数据

- sqlalchemy库中create_engine创建连接， 不能直接使用pymysql

```python
from sqlalchemy import create_engine
```

```python
# dialect[+driver]://user:password@host/dbname[?key=value..]
conn = create_engine("mysql+pymysql://root:xuhui19951203@localhost/stu",
                     encoding='utf-8')
print('--连接MySQL数据库成功--')
```

```
--连接MySQL数据库成功--
```



```python
pd.read_sql('select * from Student', conn)
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
      <th>sn</th>
      <th>name</th>
      <th>age</th>
      <th>sex</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>赵雷</td>
      <td>1990-01-01</td>
      <td>男</td>
    </tr>
    <tr>
      <th>1</th>
      <td>02</td>
      <td>钱电</td>
      <td>1990-12-21</td>
      <td>男</td>
    </tr>
    <tr>
      <th>2</th>
      <td>03</td>
      <td>孙风</td>
      <td>1990-05-20</td>
      <td>男</td>
    </tr>
    <tr>
      <th>3</th>
      <td>04</td>
      <td>李云</td>
      <td>1990-08-06</td>
      <td>男</td>
    </tr>
    <tr>
      <th>4</th>
      <td>05</td>
      <td>周梅</td>
      <td>1991-12-01</td>
      <td>女</td>
    </tr>
    <tr>
      <th>5</th>
      <td>06</td>
      <td>吴兰</td>
      <td>1992-03-01</td>
      <td>女</td>
    </tr>
    <tr>
      <th>6</th>
      <td>07</td>
      <td>郑竹</td>
      <td>1989-08-17</td>
      <td>女</td>
    </tr>
    <tr>
      <th>7</th>
      <td>08</td>
      <td>王菊</td>
      <td>1990-01-20</td>
      <td>女</td>
    </tr>
  </tbody>
</table>
</div>



### 加载网络数据

```python
url = 'https://raw.githubusercontent.com/datasets/investor-flow-of-funds-us/master/data/weekly.csv'
weekly = pd.read_csv(url)
weekly.head()
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
      <th>Total Equity</th>
      <th>Domestic Equity</th>
      <th>World Equity</th>
      <th>Hybrid</th>
      <th>Total Bond</th>
      <th>Taxable Bond</th>
      <th>Municipal Bond</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2012-12-05</td>
      <td>-7426</td>
      <td>-6060</td>
      <td>-1367</td>
      <td>-74</td>
      <td>5317</td>
      <td>4210</td>
      <td>1107</td>
      <td>-2183</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2012-12-12</td>
      <td>-8783</td>
      <td>-7520</td>
      <td>-1263</td>
      <td>123</td>
      <td>1818</td>
      <td>1598</td>
      <td>219</td>
      <td>-6842</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012-12-19</td>
      <td>-5496</td>
      <td>-5470</td>
      <td>-26</td>
      <td>-73</td>
      <td>103</td>
      <td>3472</td>
      <td>-3369</td>
      <td>-5466</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2012-12-26</td>
      <td>-4451</td>
      <td>-4076</td>
      <td>-375</td>
      <td>550</td>
      <td>2610</td>
      <td>3333</td>
      <td>-722</td>
      <td>-1291</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2013-01-02</td>
      <td>-11156</td>
      <td>-9622</td>
      <td>-1533</td>
      <td>-158</td>
      <td>2383</td>
      <td>2103</td>
      <td>280</td>
      <td>-8931</td>
    </tr>
  </tbody>
</table>
</div>




```python
weekly.shape
```



```
(44, 9)
```