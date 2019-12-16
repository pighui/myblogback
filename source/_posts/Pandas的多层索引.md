---
title: Pandas的多层索引
comments: true
tags:
  - Python
  - 数据分析
categories:
  - 数据分析
date: 2019-04-30 12:54:03
---


### 行的多层索引

- Series的多层索引
- DataFrame的多层索引

<!--more-->

- 创建方式
  - 隐式方式，使用二维数组，如[[一级索引名称,], [二级索引名称,]]
  - 显式方式，MultiIndex
    - MultiIndex.from_arrays([[一级索引名称,], [二级索引名称,]])
    - MultiIndex.from_tuples([(一级索引名称, 二级索引名称), ])
    - MultiIndex.from_product([[一级索引名称,], [二级索引名称,]])

<font color='red'>**说明：from_arrays()中索引名称会重复多次，而from_product()中索引不会重复。**</font>



```python
import numpy as np
import pandas as pd
from pandas import Series, DataFrame, MultiIndex
```

```python
# 创建1月份的五大城市(西安、上海、北京、广州、深圳)的
# Oppo、华为、小米、iphone四中手机的销售量情况
cosumers_1 = Series(np.random.randint(1000, 2000, size=20),
                   index=[['西安','西安','西安','西安',
                          '上海','上海','上海','上海',
                          '北京','北京','北京','北京',
                          '广州','广州','广州','广州',
                          '深圳','深圳','深圳','深圳'],
                         ['Oppo','华为','小米','iphone']*5])
cosumers_1
```



```
西安  Oppo      1430
    华为        1217
    小米        1679
    iphone    1514
上海  Oppo      1067
    华为        1513
    小米        1736
    iphone    1168
北京  Oppo      1361
    华为        1070
    小米        1157
    iphone    1025
广州  Oppo      1161
    华为        1565
    小米        1670
    iphone    1261
深圳  Oppo      1781
    华为        1283
    小米        1720
    iphone    1566
dtype: int64
```



```python
# 创建二月份的两个城市(西安，上海)的Oppo/iphone2种手机的销售量情况
cosumers_2 = Series([1500,600,2412,50],
                   index=MultiIndex.from_tuples([('西安','Oppo'),
                                                ('西安','iphone'),
                                                ('上海','Oppo'),
                                                ('上海','iphone')]))
cosumers_2
```



```
西安  Oppo      1500
    iphone     600
上海  Oppo      2412
    iphone      50
dtype: int64
```



```python
# 使用product()方式，将以上两个创建多层索引的表的方式优化
c1 = Series(np.random.randint(100, 2000, size=20),
           index=MultiIndex.from_product([['西安', '上海', '北京', '广州', '深圳'],
                                          ['Oppo', '华为', '小米', 'iPhone']]))
c1
```



```
西安  Oppo      1558
    华为         397
    小米         404
    iPhone     682
上海  Oppo       452
    华为        1993
    小米         654
    iPhone    1397
北京  Oppo       400
    华为         146
    小米         721
    iPhone     648
广州  Oppo      1804
    华为        1955
    小米         529
    iPhone     992
深圳  Oppo      1795
    华为        1985
    小米        1435
    iPhone    1034
dtype: int64
```



```python
# 创建1~12月份的五大城市的四种手机的售量情况表
index = MultiIndex.from_product([['西安', '上海', '北京', '广州', '深圳'],
                                 ['Oppo', '华为', '小米', 'iPhone']])
sales = DataFrame(np.random.randint(50, 2000, size=(20, 12)),
                 index=index,
                 columns=np.arange(1, 13, step=1))
sales
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
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">西安</th>
      <th>Oppo</th>
      <td>1213</td>
      <td>1407</td>
      <td>691</td>
      <td>1734</td>
      <td>86</td>
      <td>484</td>
      <td>365</td>
      <td>1699</td>
      <td>1759</td>
      <td>1806</td>
      <td>1930</td>
      <td>1390</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>1206</td>
      <td>180</td>
      <td>1392</td>
      <td>337</td>
      <td>268</td>
      <td>1332</td>
      <td>298</td>
      <td>724</td>
      <td>330</td>
      <td>549</td>
      <td>1479</td>
      <td>1229</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>509</td>
      <td>1280</td>
      <td>1354</td>
      <td>1414</td>
      <td>1981</td>
      <td>862</td>
      <td>183</td>
      <td>377</td>
      <td>1925</td>
      <td>369</td>
      <td>179</td>
      <td>813</td>
    </tr>
    <tr>
      <th>iPhone</th>
      <td>1364</td>
      <td>1420</td>
      <td>1188</td>
      <td>584</td>
      <td>1974</td>
      <td>349</td>
      <td>226</td>
      <td>1745</td>
      <td>1571</td>
      <td>797</td>
      <td>1751</td>
      <td>1663</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">上海</th>
      <th>Oppo</th>
      <td>718</td>
      <td>1605</td>
      <td>1047</td>
      <td>1224</td>
      <td>760</td>
      <td>246</td>
      <td>1236</td>
      <td>1652</td>
      <td>1939</td>
      <td>695</td>
      <td>581</td>
      <td>379</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>562</td>
      <td>1173</td>
      <td>357</td>
      <td>565</td>
      <td>1796</td>
      <td>65</td>
      <td>609</td>
      <td>1869</td>
      <td>1464</td>
      <td>211</td>
      <td>1584</td>
      <td>988</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>1631</td>
      <td>567</td>
      <td>121</td>
      <td>1140</td>
      <td>1843</td>
      <td>651</td>
      <td>1480</td>
      <td>224</td>
      <td>1740</td>
      <td>250</td>
      <td>1167</td>
      <td>1286</td>
    </tr>
    <tr>
      <th>iPhone</th>
      <td>532</td>
      <td>1692</td>
      <td>1536</td>
      <td>112</td>
      <td>1370</td>
      <td>526</td>
      <td>1633</td>
      <td>1150</td>
      <td>1669</td>
      <td>218</td>
      <td>1395</td>
      <td>993</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">北京</th>
      <th>Oppo</th>
      <td>1822</td>
      <td>575</td>
      <td>143</td>
      <td>429</td>
      <td>138</td>
      <td>1804</td>
      <td>439</td>
      <td>1548</td>
      <td>966</td>
      <td>290</td>
      <td>1783</td>
      <td>1985</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>1397</td>
      <td>1378</td>
      <td>941</td>
      <td>1575</td>
      <td>580</td>
      <td>1472</td>
      <td>922</td>
      <td>988</td>
      <td>1486</td>
      <td>478</td>
      <td>1838</td>
      <td>1289</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>1309</td>
      <td>1097</td>
      <td>618</td>
      <td>1935</td>
      <td>736</td>
      <td>1105</td>
      <td>198</td>
      <td>1639</td>
      <td>807</td>
      <td>1699</td>
      <td>1225</td>
      <td>1248</td>
    </tr>
    <tr>
      <th>iPhone</th>
      <td>793</td>
      <td>1128</td>
      <td>1809</td>
      <td>1296</td>
      <td>378</td>
      <td>144</td>
      <td>1544</td>
      <td>1175</td>
      <td>1736</td>
      <td>922</td>
      <td>1462</td>
      <td>1292</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">广州</th>
      <th>Oppo</th>
      <td>1463</td>
      <td>1227</td>
      <td>1535</td>
      <td>906</td>
      <td>1745</td>
      <td>1270</td>
      <td>828</td>
      <td>1729</td>
      <td>1894</td>
      <td>160</td>
      <td>723</td>
      <td>196</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>1192</td>
      <td>1170</td>
      <td>1171</td>
      <td>1770</td>
      <td>773</td>
      <td>871</td>
      <td>1222</td>
      <td>796</td>
      <td>1141</td>
      <td>1028</td>
      <td>1699</td>
      <td>1137</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>1830</td>
      <td>692</td>
      <td>885</td>
      <td>1064</td>
      <td>1961</td>
      <td>1632</td>
      <td>1691</td>
      <td>1653</td>
      <td>387</td>
      <td>661</td>
      <td>467</td>
      <td>1253</td>
    </tr>
    <tr>
      <th>iPhone</th>
      <td>1847</td>
      <td>1294</td>
      <td>1199</td>
      <td>760</td>
      <td>1547</td>
      <td>425</td>
      <td>1931</td>
      <td>1046</td>
      <td>407</td>
      <td>904</td>
      <td>1571</td>
      <td>1354</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">深圳</th>
      <th>Oppo</th>
      <td>895</td>
      <td>1733</td>
      <td>390</td>
      <td>513</td>
      <td>573</td>
      <td>977</td>
      <td>397</td>
      <td>899</td>
      <td>1946</td>
      <td>1157</td>
      <td>1307</td>
      <td>1409</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>626</td>
      <td>1012</td>
      <td>1889</td>
      <td>1363</td>
      <td>868</td>
      <td>199</td>
      <td>190</td>
      <td>1601</td>
      <td>679</td>
      <td>1681</td>
      <td>1815</td>
      <td>931</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>1503</td>
      <td>1742</td>
      <td>525</td>
      <td>1097</td>
      <td>1476</td>
      <td>586</td>
      <td>752</td>
      <td>1840</td>
      <td>182</td>
      <td>1745</td>
      <td>556</td>
      <td>1052</td>
    </tr>
    <tr>
      <th>iPhone</th>
      <td>1285</td>
      <td>810</td>
      <td>1446</td>
      <td>521</td>
      <td>717</td>
      <td>805</td>
      <td>1814</td>
      <td>976</td>
      <td>1650</td>
      <td>1452</td>
      <td>1311</td>
      <td>301</td>
    </tr>
  </tbody>
</table>
    </div>



### 多层列索引

- 同多层行索引

```python
# 生成5大城市的四种手机品牌的2017、2018两个年度的4个季节的售量表
datas = np.random.randint(50,5000,size=(20,8))
index = MultiIndex.from_product([['西安', '上海', '北京', '广州', '深圳'],
                           ['Oppo', '华为', '小米', 'iphone']])
columns = MultiIndex.from_product([['2017', '2018'],
                             ['1', '2', '3', '4']])
df = DataFrame(datas, index, columns)
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
.dataframe thead tr th {
    text-align: left;
}
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th colspan="4" halign="left">2017</th>
      <th colspan="4" halign="left">2018</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">西安</th>
      <th>Oppo</th>
      <td>1083</td>
      <td>3895</td>
      <td>589</td>
      <td>1675</td>
      <td>3620</td>
      <td>2033</td>
      <td>3712</td>
      <td>1140</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>4519</td>
      <td>271</td>
      <td>286</td>
      <td>4029</td>
      <td>3189</td>
      <td>2208</td>
      <td>2072</td>
      <td>3957</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>2195</td>
      <td>679</td>
      <td>1467</td>
      <td>1793</td>
      <td>3025</td>
      <td>864</td>
      <td>1362</td>
      <td>2566</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>2356</td>
      <td>537</td>
      <td>205</td>
      <td>1246</td>
      <td>768</td>
      <td>1555</td>
      <td>734</td>
      <td>4252</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">上海</th>
      <th>Oppo</th>
      <td>415</td>
      <td>2999</td>
      <td>2039</td>
      <td>2517</td>
      <td>4035</td>
      <td>1400</td>
      <td>2602</td>
      <td>4731</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>1781</td>
      <td>1732</td>
      <td>1476</td>
      <td>1236</td>
      <td>1973</td>
      <td>4875</td>
      <td>891</td>
      <td>76</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>993</td>
      <td>190</td>
      <td>2148</td>
      <td>3934</td>
      <td>4008</td>
      <td>3662</td>
      <td>119</td>
      <td>3928</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>1595</td>
      <td>819</td>
      <td>3033</td>
      <td>4157</td>
      <td>4645</td>
      <td>4489</td>
      <td>1058</td>
      <td>268</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">北京</th>
      <th>Oppo</th>
      <td>3472</td>
      <td>3334</td>
      <td>494</td>
      <td>1888</td>
      <td>1283</td>
      <td>2286</td>
      <td>4246</td>
      <td>3683</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>4348</td>
      <td>2115</td>
      <td>2153</td>
      <td>295</td>
      <td>2830</td>
      <td>2625</td>
      <td>576</td>
      <td>1608</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>2343</td>
      <td>3544</td>
      <td>4272</td>
      <td>2806</td>
      <td>3380</td>
      <td>3105</td>
      <td>2432</td>
      <td>2220</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>1163</td>
      <td>4934</td>
      <td>517</td>
      <td>4357</td>
      <td>508</td>
      <td>2372</td>
      <td>3048</td>
      <td>2326</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">广州</th>
      <th>Oppo</th>
      <td>2574</td>
      <td>3347</td>
      <td>1768</td>
      <td>2933</td>
      <td>848</td>
      <td>1787</td>
      <td>1887</td>
      <td>3121</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>1965</td>
      <td>401</td>
      <td>1719</td>
      <td>2495</td>
      <td>1552</td>
      <td>482</td>
      <td>584</td>
      <td>4940</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>963</td>
      <td>2257</td>
      <td>2237</td>
      <td>1281</td>
      <td>816</td>
      <td>1782</td>
      <td>2694</td>
      <td>3769</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>855</td>
      <td>61</td>
      <td>1596</td>
      <td>1001</td>
      <td>121</td>
      <td>942</td>
      <td>4385</td>
      <td>429</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">深圳</th>
      <th>Oppo</th>
      <td>535</td>
      <td>4147</td>
      <td>1049</td>
      <td>4212</td>
      <td>3290</td>
      <td>1644</td>
      <td>2499</td>
      <td>4938</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>1301</td>
      <td>3747</td>
      <td>4177</td>
      <td>416</td>
      <td>1030</td>
      <td>2800</td>
      <td>2829</td>
      <td>400</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>1914</td>
      <td>4762</td>
      <td>1573</td>
      <td>2578</td>
      <td>2230</td>
      <td>1891</td>
      <td>993</td>
      <td>1047</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>2047</td>
      <td>3159</td>
      <td>1492</td>
      <td>3990</td>
      <td>803</td>
      <td>4354</td>
      <td>4012</td>
      <td>2580</td>
    </tr>
  </tbody>
</table>
</div>




### 多层索引选择和切片操作

```python
# 查看2017年西安城市的所有手机品牌的销售量情况
# 一级标签索引的选择，同DataFrame的普通索引和选择操作
df.loc['西安', '2017']
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
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Oppo</th>
      <td>1083</td>
      <td>3895</td>
      <td>589</td>
      <td>1675</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>4519</td>
      <td>271</td>
      <td>286</td>
      <td>4029</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>2195</td>
      <td>679</td>
      <td>1467</td>
      <td>1793</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>2356</td>
      <td>537</td>
      <td>205</td>
      <td>1246</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 查看北京城市的所有手机品牌在不同年度的第2季度销售量情况
# 一级行标签 + 二级列标签 (元组中包含一级标签和二级标签)
df.loc['北京',[('2017','2'),('2018','2')]]
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
      <th>2017</th>
      <th>2018</th>
    </tr>
    <tr>
      <th></th>
      <th>2</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Oppo</th>
      <td>3334</td>
      <td>2286</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>2115</td>
      <td>2625</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>3544</td>
      <td>3105</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>4934</td>
      <td>2372</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 查看2018年不同城市的小米手机的销售量情况
# 一级列标签 + 二级行标签
df.loc[[('西安','小米'),
        ('上海','小米'),
        ('北京','小米'),
        ('广州','小米'),
        ('深圳','小米'),
       ],'2018']
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
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>西安</th>
      <th>小米</th>
      <td>3025</td>
      <td>864</td>
      <td>1362</td>
      <td>2566</td>
    </tr>
    <tr>
      <th>上海</th>
      <th>小米</th>
      <td>4008</td>
      <td>3662</td>
      <td>119</td>
      <td>3928</td>
    </tr>
    <tr>
      <th>北京</th>
      <th>小米</th>
      <td>3380</td>
      <td>3105</td>
      <td>2432</td>
      <td>2220</td>
    </tr>
    <tr>
      <th>广州</th>
      <th>小米</th>
      <td>816</td>
      <td>1782</td>
      <td>2694</td>
      <td>3769</td>
    </tr>
    <tr>
      <th>深圳</th>
      <th>小米</th>
      <td>2230</td>
      <td>1891</td>
      <td>993</td>
      <td>1047</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 查看2018年不同城市的小米手机的销售量情况
# 使用.iloc[]方式,以切片方式实现
df.iloc[2::4,4:]
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
      <th></th>
      <th colspan="4" halign="left">2018</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>西安</th>
      <th>小米</th>
      <td>3025</td>
      <td>864</td>
      <td>1362</td>
      <td>2566</td>
    </tr>
    <tr>
      <th>上海</th>
      <th>小米</th>
      <td>4008</td>
      <td>3662</td>
      <td>119</td>
      <td>3928</td>
    </tr>
    <tr>
      <th>北京</th>
      <th>小米</th>
      <td>3380</td>
      <td>3105</td>
      <td>2432</td>
      <td>2220</td>
    </tr>
    <tr>
      <th>广州</th>
      <th>小米</th>
      <td>816</td>
      <td>1782</td>
      <td>2694</td>
      <td>3769</td>
    </tr>
    <tr>
      <th>深圳</th>
      <th>小米</th>
      <td>2230</td>
      <td>1891</td>
      <td>993</td>
      <td>1047</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 查看不同城市的iphone品牌在不同年度的3季度的销售量情况
# 二级行索引 + 二级列索引
df.loc[[('西安','iphone'),
        ('上海','iphone'),
        ('北京','iphone'),
        ('广州','iphone'),
        ('深圳','iphone'),
       ],[('2017','3'),
         ('2018','3')
         ]]
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
      <th></th>
      <th>2017</th>
      <th>2018</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>3</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>西安</th>
      <th>iphone</th>
      <td>205</td>
      <td>734</td>
    </tr>
    <tr>
      <th>上海</th>
      <th>iphone</th>
      <td>3033</td>
      <td>1058</td>
    </tr>
    <tr>
      <th>北京</th>
      <th>iphone</th>
      <td>517</td>
      <td>3048</td>
    </tr>
    <tr>
      <th>广州</th>
      <th>iphone</th>
      <td>1596</td>
      <td>4385</td>
    </tr>
    <tr>
      <th>深圳</th>
      <th>iphone</th>
      <td>1492</td>
      <td>4012</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.iloc[3::4, 2::4]
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
      <th></th>
      <th>2017</th>
      <th>2018</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>3</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>西安</th>
      <th>iphone</th>
      <td>205</td>
      <td>734</td>
    </tr>
    <tr>
      <th>上海</th>
      <th>iphone</th>
      <td>3033</td>
      <td>1058</td>
    </tr>
    <tr>
      <th>北京</th>
      <th>iphone</th>
      <td>517</td>
      <td>3048</td>
    </tr>
    <tr>
      <th>广州</th>
      <th>iphone</th>
      <td>1596</td>
      <td>4385</td>
    </tr>
    <tr>
      <th>深圳</th>
      <th>iphone</th>
      <td>1492</td>
      <td>4012</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 将上海的苹果品牌在2017第3季度的销量减去1000
df.loc[('上海','iphone'),('2017','3')] -= 1000
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
.dataframe thead tr th {
    text-align: left;
}
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th colspan="4" halign="left">2017</th>
      <th colspan="4" halign="left">2018</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">西安</th>
      <th>Oppo</th>
      <td>1083</td>
      <td>3895</td>
      <td>589</td>
      <td>1675</td>
      <td>3620</td>
      <td>2033</td>
      <td>3712</td>
      <td>1140</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>4519</td>
      <td>271</td>
      <td>286</td>
      <td>4029</td>
      <td>3189</td>
      <td>2208</td>
      <td>2072</td>
      <td>3957</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>2195</td>
      <td>679</td>
      <td>1467</td>
      <td>1793</td>
      <td>3025</td>
      <td>864</td>
      <td>1362</td>
      <td>2566</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>2356</td>
      <td>537</td>
      <td>205</td>
      <td>1246</td>
      <td>768</td>
      <td>1555</td>
      <td>734</td>
      <td>4252</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">上海</th>
      <th>Oppo</th>
      <td>415</td>
      <td>2999</td>
      <td>2039</td>
      <td>2517</td>
      <td>4035</td>
      <td>1400</td>
      <td>2602</td>
      <td>4731</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>1781</td>
      <td>1732</td>
      <td>1476</td>
      <td>1236</td>
      <td>1973</td>
      <td>4875</td>
      <td>891</td>
      <td>76</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>993</td>
      <td>190</td>
      <td>2148</td>
      <td>3934</td>
      <td>4008</td>
      <td>3662</td>
      <td>119</td>
      <td>3928</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>1595</td>
      <td>819</td>
      <td>2033</td>
      <td>4157</td>
      <td>4645</td>
      <td>4489</td>
      <td>1058</td>
      <td>268</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">北京</th>
      <th>Oppo</th>
      <td>3472</td>
      <td>3334</td>
      <td>494</td>
      <td>1888</td>
      <td>1283</td>
      <td>2286</td>
      <td>4246</td>
      <td>3683</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>4348</td>
      <td>2115</td>
      <td>2153</td>
      <td>295</td>
      <td>2830</td>
      <td>2625</td>
      <td>576</td>
      <td>1608</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>2343</td>
      <td>3544</td>
      <td>4272</td>
      <td>2806</td>
      <td>3380</td>
      <td>3105</td>
      <td>2432</td>
      <td>2220</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>1163</td>
      <td>4934</td>
      <td>517</td>
      <td>4357</td>
      <td>508</td>
      <td>2372</td>
      <td>3048</td>
      <td>2326</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">广州</th>
      <th>Oppo</th>
      <td>2574</td>
      <td>3347</td>
      <td>1768</td>
      <td>2933</td>
      <td>848</td>
      <td>1787</td>
      <td>1887</td>
      <td>3121</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>1965</td>
      <td>401</td>
      <td>1719</td>
      <td>2495</td>
      <td>1552</td>
      <td>482</td>
      <td>584</td>
      <td>4940</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>963</td>
      <td>2257</td>
      <td>2237</td>
      <td>1281</td>
      <td>816</td>
      <td>1782</td>
      <td>2694</td>
      <td>3769</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>855</td>
      <td>61</td>
      <td>1596</td>
      <td>1001</td>
      <td>121</td>
      <td>942</td>
      <td>4385</td>
      <td>429</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">深圳</th>
      <th>Oppo</th>
      <td>535</td>
      <td>4147</td>
      <td>1049</td>
      <td>4212</td>
      <td>3290</td>
      <td>1644</td>
      <td>2499</td>
      <td>4938</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>1301</td>
      <td>3747</td>
      <td>4177</td>
      <td>416</td>
      <td>1030</td>
      <td>2800</td>
      <td>2829</td>
      <td>400</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>1914</td>
      <td>4762</td>
      <td>1573</td>
      <td>2578</td>
      <td>2230</td>
      <td>1891</td>
      <td>993</td>
      <td>1047</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>2047</td>
      <td>3159</td>
      <td>1492</td>
      <td>3990</td>
      <td>803</td>
      <td>4354</td>
      <td>4012</td>
      <td>2580</td>
    </tr>
  </tbody>
</table>
</div>




### 扩展：Python中的对象，哪些可以作为dict的key

```python
class ChildError(Exception):
    pass
```

```python
e = ChildError('不能创建分身')
```

```python
# str, int, float, bool(True, False), None
# tuple(), object, fun, class,
# 如果类对象作为dict的key必须是可以被hash的
# 可以通过hash()内置函数尝试获取对象的hash值
disen = {
    'name': 'disen',
    'age': 20,
    'salary': 1000.5,
    'action': lambda x: x**2,
    'is_alive': True,
    'level': None,
    'city': ('陕西', '西安'),
    'error': ChildError,
    'error_obj': e
}
```

```python
disen_ct = { value:key for key,value in disen.items() }
disen_ct
```



```
{'disen': 'name',
 20: 'age',
 1000.5: 'salary',
 <function __main__.<lambda>(x)>: 'action',
 True: 'is_alive',
 None: 'level',
 ('陕西', '西安'): 'city',
 __main__.ChildError: 'error',
 __main__.ChildError('不能创建分身'): 'error_obj'}
```



```python
# 调用字典中的函数
action = disen.get('action')
action(100)
```



```
10000
```



```python
# 字典中的key使用hash生成唯一标识
hash(e)
```



```
-9223363251881703466
```



### 索引的堆操作

- stack() 将列索引转成行索引(标签)
- unstack() 将行索引转成列索引(标签)

两个函数中，有一个level属性，表示哪一级别的标签，0 一级， -1 最内级别

```python
df.stack(level=-1) # 将列的第二级的标签转成行标签（第三级）
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
      <th></th>
      <th>2017</th>
      <th>2018</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="16" valign="top">西安</th>
      <th rowspan="4" valign="top">Oppo</th>
      <th>1</th>
      <td>1083</td>
      <td>3620</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3895</td>
      <td>2033</td>
    </tr>
    <tr>
      <th>3</th>
      <td>589</td>
      <td>3712</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1675</td>
      <td>1140</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">华为</th>
      <th>1</th>
      <td>4519</td>
      <td>3189</td>
    </tr>
    <tr>
      <th>2</th>
      <td>271</td>
      <td>2208</td>
    </tr>
    <tr>
      <th>3</th>
      <td>286</td>
      <td>2072</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4029</td>
      <td>3957</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">小米</th>
      <th>1</th>
      <td>2195</td>
      <td>3025</td>
    </tr>
    <tr>
      <th>2</th>
      <td>679</td>
      <td>864</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1467</td>
      <td>1362</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1793</td>
      <td>2566</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">iphone</th>
      <th>1</th>
      <td>2356</td>
      <td>768</td>
    </tr>
    <tr>
      <th>2</th>
      <td>537</td>
      <td>1555</td>
    </tr>
    <tr>
      <th>3</th>
      <td>205</td>
      <td>734</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1246</td>
      <td>4252</td>
    </tr>
    <tr>
      <th rowspan="14" valign="top">上海</th>
      <th rowspan="4" valign="top">Oppo</th>
      <th>1</th>
      <td>415</td>
      <td>4035</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2999</td>
      <td>1400</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2039</td>
      <td>2602</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2517</td>
      <td>4731</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">华为</th>
      <th>1</th>
      <td>1781</td>
      <td>1973</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1732</td>
      <td>4875</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1476</td>
      <td>891</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1236</td>
      <td>76</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">小米</th>
      <th>1</th>
      <td>993</td>
      <td>4008</td>
    </tr>
    <tr>
      <th>2</th>
      <td>190</td>
      <td>3662</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2148</td>
      <td>119</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3934</td>
      <td>3928</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">iphone</th>
      <th>1</th>
      <td>1595</td>
      <td>4645</td>
    </tr>
    <tr>
      <th>2</th>
      <td>819</td>
      <td>4489</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="14" valign="top">广州</th>
      <th rowspan="2" valign="top">Oppo</th>
      <th>3</th>
      <td>1768</td>
      <td>1887</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2933</td>
      <td>3121</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">华为</th>
      <th>1</th>
      <td>1965</td>
      <td>1552</td>
    </tr>
    <tr>
      <th>2</th>
      <td>401</td>
      <td>482</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1719</td>
      <td>584</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2495</td>
      <td>4940</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">小米</th>
      <th>1</th>
      <td>963</td>
      <td>816</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2257</td>
      <td>1782</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2237</td>
      <td>2694</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1281</td>
      <td>3769</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">iphone</th>
      <th>1</th>
      <td>855</td>
      <td>121</td>
    </tr>
    <tr>
      <th>2</th>
      <td>61</td>
      <td>942</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1596</td>
      <td>4385</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1001</td>
      <td>429</td>
    </tr>
    <tr>
      <th rowspan="16" valign="top">深圳</th>
      <th rowspan="4" valign="top">Oppo</th>
      <th>1</th>
      <td>535</td>
      <td>3290</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4147</td>
      <td>1644</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1049</td>
      <td>2499</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4212</td>
      <td>4938</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">华为</th>
      <th>1</th>
      <td>1301</td>
      <td>1030</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3747</td>
      <td>2800</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4177</td>
      <td>2829</td>
    </tr>
    <tr>
      <th>4</th>
      <td>416</td>
      <td>400</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">小米</th>
      <th>1</th>
      <td>1914</td>
      <td>2230</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4762</td>
      <td>1891</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1573</td>
      <td>993</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2578</td>
      <td>1047</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">iphone</th>
      <th>1</th>
      <td>2047</td>
      <td>803</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3159</td>
      <td>4354</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1492</td>
      <td>4012</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3990</td>
      <td>2580</td>
    </tr>
  </tbody>
</table>
<p>80 rows × 2 columns</p>
</div>



```python
df.stack(level=-1).loc[('西安', 'Oppo', '3'), '2017']
```



```
589
```



```python
df.stack(level=-1).index
```



```
MultiIndex(levels=[['上海', '北京', '广州', '深圳', '西安'], ['Oppo', 'iphone', '华为', '小米'], ['1', '2', '3', '4']],
           labels=[[4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3], [0, 0, 0, 0, 2, 2, 2, 2, 3, 3, 3, 3, 1, 1, 1, 1, 0, 0, 0, 0, 2, 2, 2, 2, 3, 3, 3, 3, 1, 1, 1, 1, 0, 0, 0, 0, 2, 2, 2, 2, 3, 3, 3, 3, 1, 1, 1, 1, 0, 0, 0, 0, 2, 2, 2, 2, 3, 3, 3, 3, 1, 1, 1, 1, 0, 0, 0, 0, 2, 2, 2, 2, 3, 3, 3, 3, 1, 1, 1, 1], [0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3]])
```



```python
df.stack(level=0) # 将列的一级标签转成行的三级标签
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
      <th></th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">西安</th>
      <th rowspan="2" valign="top">Oppo</th>
      <th>2017</th>
      <td>1083</td>
      <td>3895</td>
      <td>589</td>
      <td>1675</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>3620</td>
      <td>2033</td>
      <td>3712</td>
      <td>1140</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">华为</th>
      <th>2017</th>
      <td>4519</td>
      <td>271</td>
      <td>286</td>
      <td>4029</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>3189</td>
      <td>2208</td>
      <td>2072</td>
      <td>3957</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">小米</th>
      <th>2017</th>
      <td>2195</td>
      <td>679</td>
      <td>1467</td>
      <td>1793</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>3025</td>
      <td>864</td>
      <td>1362</td>
      <td>2566</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">iphone</th>
      <th>2017</th>
      <td>2356</td>
      <td>537</td>
      <td>205</td>
      <td>1246</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>768</td>
      <td>1555</td>
      <td>734</td>
      <td>4252</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">上海</th>
      <th rowspan="2" valign="top">Oppo</th>
      <th>2017</th>
      <td>415</td>
      <td>2999</td>
      <td>2039</td>
      <td>2517</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>4035</td>
      <td>1400</td>
      <td>2602</td>
      <td>4731</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">华为</th>
      <th>2017</th>
      <td>1781</td>
      <td>1732</td>
      <td>1476</td>
      <td>1236</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>1973</td>
      <td>4875</td>
      <td>891</td>
      <td>76</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">小米</th>
      <th>2017</th>
      <td>993</td>
      <td>190</td>
      <td>2148</td>
      <td>3934</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>4008</td>
      <td>3662</td>
      <td>119</td>
      <td>3928</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">iphone</th>
      <th>2017</th>
      <td>1595</td>
      <td>819</td>
      <td>2033</td>
      <td>4157</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>4645</td>
      <td>4489</td>
      <td>1058</td>
      <td>268</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">北京</th>
      <th rowspan="2" valign="top">Oppo</th>
      <th>2017</th>
      <td>3472</td>
      <td>3334</td>
      <td>494</td>
      <td>1888</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>1283</td>
      <td>2286</td>
      <td>4246</td>
      <td>3683</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">华为</th>
      <th>2017</th>
      <td>4348</td>
      <td>2115</td>
      <td>2153</td>
      <td>295</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>2830</td>
      <td>2625</td>
      <td>576</td>
      <td>1608</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">小米</th>
      <th>2017</th>
      <td>2343</td>
      <td>3544</td>
      <td>4272</td>
      <td>2806</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>3380</td>
      <td>3105</td>
      <td>2432</td>
      <td>2220</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">iphone</th>
      <th>2017</th>
      <td>1163</td>
      <td>4934</td>
      <td>517</td>
      <td>4357</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>508</td>
      <td>2372</td>
      <td>3048</td>
      <td>2326</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">广州</th>
      <th rowspan="2" valign="top">Oppo</th>
      <th>2017</th>
      <td>2574</td>
      <td>3347</td>
      <td>1768</td>
      <td>2933</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>848</td>
      <td>1787</td>
      <td>1887</td>
      <td>3121</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">华为</th>
      <th>2017</th>
      <td>1965</td>
      <td>401</td>
      <td>1719</td>
      <td>2495</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>1552</td>
      <td>482</td>
      <td>584</td>
      <td>4940</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">小米</th>
      <th>2017</th>
      <td>963</td>
      <td>2257</td>
      <td>2237</td>
      <td>1281</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>816</td>
      <td>1782</td>
      <td>2694</td>
      <td>3769</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">iphone</th>
      <th>2017</th>
      <td>855</td>
      <td>61</td>
      <td>1596</td>
      <td>1001</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>121</td>
      <td>942</td>
      <td>4385</td>
      <td>429</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">深圳</th>
      <th rowspan="2" valign="top">Oppo</th>
      <th>2017</th>
      <td>535</td>
      <td>4147</td>
      <td>1049</td>
      <td>4212</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>3290</td>
      <td>1644</td>
      <td>2499</td>
      <td>4938</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">华为</th>
      <th>2017</th>
      <td>1301</td>
      <td>3747</td>
      <td>4177</td>
      <td>416</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>1030</td>
      <td>2800</td>
      <td>2829</td>
      <td>400</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">小米</th>
      <th>2017</th>
      <td>1914</td>
      <td>4762</td>
      <td>1573</td>
      <td>2578</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>2230</td>
      <td>1891</td>
      <td>993</td>
      <td>1047</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">iphone</th>
      <th>2017</th>
      <td>2047</td>
      <td>3159</td>
      <td>1492</td>
      <td>3990</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>803</td>
      <td>4354</td>
      <td>4012</td>
      <td>2580</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.unstack(level=0) # 将行的一级标签转成列的三级标签
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
      <th colspan="20" halign="left">2017</th>
      <th colspan="20" halign="left">2018</th>
    </tr>
    <tr>
      <th></th>
      <th colspan="5" halign="left">1</th>
      <th colspan="5" halign="left">2</th>
      <th colspan="5" halign="left">3</th>
      <th colspan="5" halign="left">4</th>
      <th colspan="5" halign="left">1</th>
      <th colspan="5" halign="left">2</th>
      <th colspan="5" halign="left">3</th>
      <th colspan="5" halign="left">4</th>
    </tr>
    <tr>
      <th></th>
      <th>上海</th>
      <th>北京</th>
      <th>广州</th>
      <th>深圳</th>
      <th>西安</th>
      <th>上海</th>
      <th>北京</th>
      <th>广州</th>
      <th>深圳</th>
      <th>西安</th>
      <th>上海</th>
      <th>北京</th>
      <th>广州</th>
      <th>深圳</th>
      <th>西安</th>
      <th>上海</th>
      <th>北京</th>
      <th>广州</th>
      <th>深圳</th>
      <th>西安</th>
      <th>上海</th>
      <th>北京</th>
      <th>广州</th>
      <th>深圳</th>
      <th>西安</th>
      <th>上海</th>
      <th>北京</th>
      <th>广州</th>
      <th>深圳</th>
      <th>西安</th>
      <th>上海</th>
      <th>北京</th>
      <th>广州</th>
      <th>深圳</th>
      <th>西安</th>
      <th>上海</th>
      <th>北京</th>
      <th>广州</th>
      <th>深圳</th>
      <th>西安</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Oppo</th>
      <td>415</td>
      <td>3472</td>
      <td>2574</td>
      <td>535</td>
      <td>1083</td>
      <td>2999</td>
      <td>3334</td>
      <td>3347</td>
      <td>4147</td>
      <td>3895</td>
      <td>2039</td>
      <td>494</td>
      <td>1768</td>
      <td>1049</td>
      <td>589</td>
      <td>2517</td>
      <td>1888</td>
      <td>2933</td>
      <td>4212</td>
      <td>1675</td>
      <td>4035</td>
      <td>1283</td>
      <td>848</td>
      <td>3290</td>
      <td>3620</td>
      <td>1400</td>
      <td>2286</td>
      <td>1787</td>
      <td>1644</td>
      <td>2033</td>
      <td>2602</td>
      <td>4246</td>
      <td>1887</td>
      <td>2499</td>
      <td>3712</td>
      <td>4731</td>
      <td>3683</td>
      <td>3121</td>
      <td>4938</td>
      <td>1140</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>1595</td>
      <td>1163</td>
      <td>855</td>
      <td>2047</td>
      <td>2356</td>
      <td>819</td>
      <td>4934</td>
      <td>61</td>
      <td>3159</td>
      <td>537</td>
      <td>2033</td>
      <td>517</td>
      <td>1596</td>
      <td>1492</td>
      <td>205</td>
      <td>4157</td>
      <td>4357</td>
      <td>1001</td>
      <td>3990</td>
      <td>1246</td>
      <td>4645</td>
      <td>508</td>
      <td>121</td>
      <td>803</td>
      <td>768</td>
      <td>4489</td>
      <td>2372</td>
      <td>942</td>
      <td>4354</td>
      <td>1555</td>
      <td>1058</td>
      <td>3048</td>
      <td>4385</td>
      <td>4012</td>
      <td>734</td>
      <td>268</td>
      <td>2326</td>
      <td>429</td>
      <td>2580</td>
      <td>4252</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>1781</td>
      <td>4348</td>
      <td>1965</td>
      <td>1301</td>
      <td>4519</td>
      <td>1732</td>
      <td>2115</td>
      <td>401</td>
      <td>3747</td>
      <td>271</td>
      <td>1476</td>
      <td>2153</td>
      <td>1719</td>
      <td>4177</td>
      <td>286</td>
      <td>1236</td>
      <td>295</td>
      <td>2495</td>
      <td>416</td>
      <td>4029</td>
      <td>1973</td>
      <td>2830</td>
      <td>1552</td>
      <td>1030</td>
      <td>3189</td>
      <td>4875</td>
      <td>2625</td>
      <td>482</td>
      <td>2800</td>
      <td>2208</td>
      <td>891</td>
      <td>576</td>
      <td>584</td>
      <td>2829</td>
      <td>2072</td>
      <td>76</td>
      <td>1608</td>
      <td>4940</td>
      <td>400</td>
      <td>3957</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>993</td>
      <td>2343</td>
      <td>963</td>
      <td>1914</td>
      <td>2195</td>
      <td>190</td>
      <td>3544</td>
      <td>2257</td>
      <td>4762</td>
      <td>679</td>
      <td>2148</td>
      <td>4272</td>
      <td>2237</td>
      <td>1573</td>
      <td>1467</td>
      <td>3934</td>
      <td>2806</td>
      <td>1281</td>
      <td>2578</td>
      <td>1793</td>
      <td>4008</td>
      <td>3380</td>
      <td>816</td>
      <td>2230</td>
      <td>3025</td>
      <td>3662</td>
      <td>3105</td>
      <td>1782</td>
      <td>1891</td>
      <td>864</td>
      <td>119</td>
      <td>2432</td>
      <td>2694</td>
      <td>993</td>
      <td>1362</td>
      <td>3928</td>
      <td>2220</td>
      <td>3769</td>
      <td>1047</td>
      <td>2566</td>
    </tr>
  </tbody>
</table>
</div>



### 多层索引的聚合操作

- max(level=0)  
- min()
- mean()

指定了level之后，按level层级进行数据的聚合操作

```python
# 统计全年的不同城市不同品牌的售量
df.sum(axis=1, level=0) # 保留一级列标签， 理解为按一级的列标签进行分组聚合
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
      <th>2017</th>
      <th>2018</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">西安</th>
      <th>Oppo</th>
      <td>7242</td>
      <td>10505</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>9105</td>
      <td>11426</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>6134</td>
      <td>7817</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>4344</td>
      <td>7309</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">上海</th>
      <th>Oppo</th>
      <td>7970</td>
      <td>12768</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>6225</td>
      <td>7815</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>7265</td>
      <td>11717</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>8604</td>
      <td>10460</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">北京</th>
      <th>Oppo</th>
      <td>9188</td>
      <td>11498</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>8911</td>
      <td>7639</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>12965</td>
      <td>11137</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>10971</td>
      <td>8254</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">广州</th>
      <th>Oppo</th>
      <td>10622</td>
      <td>7643</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>6580</td>
      <td>7558</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>6738</td>
      <td>9061</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>3513</td>
      <td>5877</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">深圳</th>
      <th>Oppo</th>
      <td>9943</td>
      <td>12371</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>9641</td>
      <td>7059</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>10827</td>
      <td>6161</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>10688</td>
      <td>11749</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 统计不同季度下各个城市所有手机的售量情况
df.sum(axis=0, level=0)
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
      <th colspan="4" halign="left">2017</th>
      <th colspan="4" halign="left">2018</th>
    </tr>
    <tr>
      <th></th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>西安</th>
      <td>10153</td>
      <td>5382</td>
      <td>2547</td>
      <td>8743</td>
      <td>10602</td>
      <td>6660</td>
      <td>7880</td>
      <td>11915</td>
    </tr>
    <tr>
      <th>上海</th>
      <td>4784</td>
      <td>5740</td>
      <td>7696</td>
      <td>11844</td>
      <td>14661</td>
      <td>14426</td>
      <td>4670</td>
      <td>9003</td>
    </tr>
    <tr>
      <th>北京</th>
      <td>11326</td>
      <td>13927</td>
      <td>7436</td>
      <td>9346</td>
      <td>8001</td>
      <td>10388</td>
      <td>10302</td>
      <td>9837</td>
    </tr>
    <tr>
      <th>广州</th>
      <td>6357</td>
      <td>6066</td>
      <td>7320</td>
      <td>7710</td>
      <td>3337</td>
      <td>4993</td>
      <td>9550</td>
      <td>12259</td>
    </tr>
    <tr>
      <th>深圳</th>
      <td>5797</td>
      <td>15815</td>
      <td>8291</td>
      <td>11196</td>
      <td>7353</td>
      <td>10689</td>
      <td>10333</td>
      <td>8965</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 统计不同品牌的全年售量情况
df.sum(axis=0, level=1).sum(axis=1, level=0)
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
      <th>2017</th>
      <th>2018</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Oppo</th>
      <td>44965</td>
      <td>54785</td>
    </tr>
    <tr>
      <th>华为</th>
      <td>40462</td>
      <td>41497</td>
    </tr>
    <tr>
      <th>小米</th>
      <td>43929</td>
      <td>45893</td>
    </tr>
    <tr>
      <th>iphone</th>
      <td>38120</td>
      <td>43649</td>
    </tr>
  </tbody>
</table>
</div>


