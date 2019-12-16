---
title: Pandas的合并操作
comments: true
date: 2019-04-30 16:35:24
tags: [Python,数据分析]
categories: [数据分析]
---


### 合并操作

- pd.merge(left,right)

<!--more-->

```python
import numpy as np
import pandas as pd
from pandas import Series, DataFrame
```

```python
# 创建员工表 employees(id, name, age, dept_id)
# 创建部门表 dept(id, name)

dept = DataFrame({
    'dept_id': ['1001', '1002', '1003'],
    'dept_name': ['软件部', '会计部', '生产部'],
})

emp = DataFrame({
    'id':['01', '02', '03', '04', '05'],
    'name': ['disen', 'lucy', 'jack', 'judy', 'mack'],
    'age': [16, 17, 19, 20, 22],
    'dept_id': ['1001', '1002', '1001', '1001', '1003']
})
```

```python
dept
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
      <th>dept_id</th>
      <th>dept_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1001</td>
      <td>软件部</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1002</td>
      <td>会计部</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1003</td>
      <td>生产部</td>
    </tr>
  </tbody>
</table>
</div>




```python
emp
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
      <th>dept_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>02</td>
      <td>lucy</td>
      <td>17</td>
      <td>1002</td>
    </tr>
    <tr>
      <th>2</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
    </tr>
    <tr>
      <th>3</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
    </tr>
    <tr>
      <th>4</th>
      <td>05</td>
      <td>mack</td>
      <td>22</td>
      <td>1003</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 将部门表和员工表合并
pd.merge(emp, dept)
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
      <th>dept_id</th>
      <th>dept_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
      <td>软件部</td>
    </tr>
    <tr>
      <th>1</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
      <td>软件部</td>
    </tr>
    <tr>
      <th>2</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
      <td>软件部</td>
    </tr>
    <tr>
      <th>3</th>
      <td>02</td>
      <td>lucy</td>
      <td>17</td>
      <td>1002</td>
      <td>会计部</td>
    </tr>
    <tr>
      <th>4</th>
      <td>05</td>
      <td>mack</td>
      <td>22</td>
      <td>1003</td>
      <td>生产部</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 添加新的员工，部门是新成立的 1004
emp = emp.append(Series({
    'id': '06',
    'name': 'jerry',
    'age': 33,
    'dept_id': 1004
}, name=5))
# append(Series)增加一行数据时，Series中必须指定行索引标签名
emp

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
      <th>dept_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>02</td>
      <td>lucy</td>
      <td>17</td>
      <td>1002</td>
    </tr>
    <tr>
      <th>2</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
    </tr>
    <tr>
      <th>3</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
    </tr>
    <tr>
      <th>4</th>
      <td>05</td>
      <td>mack</td>
      <td>22</td>
      <td>1003</td>
    </tr>
    <tr>
      <th>5</th>
      <td>06</td>
      <td>jerry</td>
      <td>33</td>
      <td>1004</td>
    </tr>
  </tbody>
</table>
</div>




```python
# how 指定合并方式，{'inner', 'outer', 'left', 'right'}
# inner 两个都存在的数据，进行合并， 类似于数据库的内连接
# outer 两个表全部显示，不管是否都存在，类似于数据库的全外连接
# left 除了共有的数据之外，额外将左表中的数据也显示
# right 除了共有的数据之外额外将右表中的数据也显示
# 注： outer/left/right都可能出现NaN值
pd.merge(emp, dept, how='inner')
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
      <th>dept_id</th>
      <th>dept_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
      <td>软件部</td>
    </tr>
    <tr>
      <th>1</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
      <td>软件部</td>
    </tr>
    <tr>
      <th>2</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
      <td>软件部</td>
    </tr>
    <tr>
      <th>3</th>
      <td>02</td>
      <td>lucy</td>
      <td>17</td>
      <td>1002</td>
      <td>会计部</td>
    </tr>
    <tr>
      <th>4</th>
      <td>05</td>
      <td>mack</td>
      <td>22</td>
      <td>1003</td>
      <td>生产部</td>
    </tr>
  </tbody>
</table>
</div>




```python
dept = dept.append({
    'dept_id': '1005',
    'dept_name': '测试部'
}, ignore_index=True)   # ignore_index=True重新创建行索引
dept
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
      <th>dept_id</th>
      <th>dept_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1001</td>
      <td>软件部</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1002</td>
      <td>会计部</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1003</td>
      <td>生产部</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1005</td>
      <td>测试部</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(emp, dept, how='outer')
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
      <th>dept_id</th>
      <th>dept_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>disen</td>
      <td>16.0</td>
      <td>1001</td>
      <td>软件部</td>
    </tr>
    <tr>
      <th>1</th>
      <td>03</td>
      <td>jack</td>
      <td>19.0</td>
      <td>1001</td>
      <td>软件部</td>
    </tr>
    <tr>
      <th>2</th>
      <td>04</td>
      <td>judy</td>
      <td>20.0</td>
      <td>1001</td>
      <td>软件部</td>
    </tr>
    <tr>
      <th>3</th>
      <td>02</td>
      <td>lucy</td>
      <td>17.0</td>
      <td>1002</td>
      <td>会计部</td>
    </tr>
    <tr>
      <th>4</th>
      <td>05</td>
      <td>mack</td>
      <td>22.0</td>
      <td>1003</td>
      <td>生产部</td>
    </tr>
    <tr>
      <th>5</th>
      <td>06</td>
      <td>jerry</td>
      <td>33.0</td>
      <td>1004</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1005</td>
      <td>测试部</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 创建管理者表 manager(manage_id, department_id, mgr_name)
manager = DataFrame({
    'manage_id': ['01', '02', '03'],# 员工的id
    'department_id': ['1001', '1001', '1003'], # 部门的id
    'mgr_name': ['Rose','Kobe', 'Oleay']
})
manager
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
      <th>manage_id</th>
      <th>department_id</th>
      <th>mgr_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>1001</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>1</th>
      <td>02</td>
      <td>1001</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>2</th>
      <td>03</td>
      <td>1003</td>
      <td>Oleay</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 将员工表和管理者表进行合并
# 如果两个表合并时没有相同的列标签，则使用left_on和right_on 来指定两个表的连接字段
pd.merge(emp, manager, left_on='dept_id', right_on='department_id')
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
      <th>dept_id</th>
      <th>manage_id</th>
      <th>department_id</th>
      <th>mgr_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
      <td>01</td>
      <td>1001</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
      <td>02</td>
      <td>1001</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>2</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
      <td>01</td>
      <td>1001</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>3</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
      <td>02</td>
      <td>1001</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>4</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
      <td>01</td>
      <td>1001</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>5</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
      <td>02</td>
      <td>1001</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>6</th>
      <td>05</td>
      <td>mack</td>
      <td>22</td>
      <td>1003</td>
      <td>03</td>
      <td>1003</td>
      <td>Oleay</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 删除某一列
pd.merge(emp, manager, left_on='dept_id', right_on='department_id').drop(columns='department_id')
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
      <th>dept_id</th>
      <th>manage_id</th>
      <th>mgr_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
      <td>01</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
      <td>02</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>2</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
      <td>01</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>3</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
      <td>02</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>4</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
      <td>01</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>5</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
      <td>02</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>6</th>
      <td>05</td>
      <td>mack</td>
      <td>22</td>
      <td>1003</td>
      <td>03</td>
      <td>Oleay</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 删除某一行
pd.merge(emp, manager, left_on='dept_id', right_on='department_id').drop(index=6)
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
      <th>dept_id</th>
      <th>manage_id</th>
      <th>department_id</th>
      <th>mgr_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
      <td>01</td>
      <td>1001</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
      <td>02</td>
      <td>1001</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>2</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
      <td>01</td>
      <td>1001</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>3</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
      <td>02</td>
      <td>1001</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>4</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
      <td>01</td>
      <td>1001</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>5</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
      <td>02</td>
      <td>1001</td>
      <td>Kobe</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 修改字段名
manager.rename(columns={'department_id':'dept_id',
                       'mange_id':'mgr_id'}, inplace=True)
manager
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
      <th>mgr_id</th>
      <th>dept_id</th>
      <th>mgr_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>1001</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>1</th>
      <td>02</td>
      <td>1001</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>2</th>
      <td>03</td>
      <td>1003</td>
      <td>Oleay</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 增加员工表的mgr_id
emp['mgr_id'] = Series(['01', '01', '02', '03', '01', '02'], index= emp.index)
emp
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
      <th>dept_id</th>
      <th>mgr_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
      <td>01</td>
    </tr>
    <tr>
      <th>1</th>
      <td>02</td>
      <td>lucy</td>
      <td>17</td>
      <td>1002</td>
      <td>01</td>
    </tr>
    <tr>
      <th>2</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
      <td>02</td>
    </tr>
    <tr>
      <th>3</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
      <td>03</td>
    </tr>
    <tr>
      <th>4</th>
      <td>05</td>
      <td>mack</td>
      <td>22</td>
      <td>1003</td>
      <td>01</td>
    </tr>
    <tr>
      <th>5</th>
      <td>06</td>
      <td>jerry</td>
      <td>33</td>
      <td>1004</td>
      <td>02</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 如果两个表中出现了相同列标签超出2个以上，则使用on来指定使用哪一个字段进行连接
# suffixes 指定相同列的后缀名
pd.merge(emp, manager, on='dept_id', suffixes=['_北京', '_西安'])
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
      <th>dept_id</th>
      <th>mgr_id_北京</th>
      <th>mgr_id_西安</th>
      <th>mgr_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
      <td>01</td>
      <td>01</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01</td>
      <td>disen</td>
      <td>16</td>
      <td>1001</td>
      <td>01</td>
      <td>02</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>2</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
      <td>02</td>
      <td>01</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>3</th>
      <td>03</td>
      <td>jack</td>
      <td>19</td>
      <td>1001</td>
      <td>02</td>
      <td>02</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>4</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
      <td>03</td>
      <td>01</td>
      <td>Rose</td>
    </tr>
    <tr>
      <th>5</th>
      <td>04</td>
      <td>judy</td>
      <td>20</td>
      <td>1001</td>
      <td>03</td>
      <td>02</td>
      <td>Kobe</td>
    </tr>
    <tr>
      <th>6</th>
      <td>05</td>
      <td>mack</td>
      <td>22</td>
      <td>1003</td>
      <td>01</td>
      <td>03</td>
      <td>Oleay</td>
    </tr>
  </tbody>
</table>
</div>


