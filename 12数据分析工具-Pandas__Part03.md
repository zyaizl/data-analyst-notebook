

```python
'''
【课程2.14】  数值计算和统计基础

常用数学、统计方法
 
'''
```


```python
# 基本参数：axis、skipna

import numpy as np
import pandas as pd

df = pd.DataFrame({'key1':[4,5,3,np.nan,2],
                 'key2':[1,2,np.nan,4,5],
                 'key3':[1,2,3,'j','k']},
                 index = ['a','b','c','d','e'])
print(df)
print(df['key1'].dtype,df['key2'].dtype,df['key3'].dtype)
print('-----')

m1 = df.mean()
print(m1,type(m1))
print('单独统计一列:',df['key2'].mean())
print('-----')
# np.nan ：空值
# .mean()计算均值
# 只统计数字列
# 可以通过索引单独统计一列

m2 = df.mean(axis=1)
print(m2)
print('-----')
# axis参数：默认为0，以列来计算，axis=1，以行来计算，这里就按照行来汇总了

m3 = df.mean(skipna=False)
print(m3)
print('-----')
# skipna参数：是否忽略NaN，默认True，如False，有NaN的列统计结果仍未NaN
```

       key1  key2 key3
    a   4.0   1.0    1
    b   5.0   2.0    2
    c   3.0   NaN    3
    d   NaN   4.0    j
    e   2.0   5.0    k
    float64 float64 object
    -----
    key1    3.5
    key2    3.0
    dtype: float64 <class 'pandas.core.series.Series'>
    单独统计一列: 3.0
    -----
    a    2.5
    b    3.5
    c    3.0
    d    4.0
    e    3.5
    dtype: float64
    -----
    key1   NaN
    key2   NaN
    dtype: float64
    -----
    


```python
# 主要数学计算方法，可用于Series和DataFrame（1）

df = pd.DataFrame({'key1':np.arange(10),
                  'key2':np.random.rand(10)*10})
print(df)
print('-----')

print(df.count(),'→ count统计非Na值的数量\n')
print(df.min(),'→ min统计最小值\n',df['key2'].max(),'→ max统计最大值\n')
print(df.quantile(q=0.75),'→ quantile统计分位数，参数q确定位置\n')
print(df.sum(),'→ sum求和\n')
print(df.mean(),'→ mean求平均值\n')
print(df.median(),'→ median求算数中位数，50%分位数\n')
print(df.std(),'\n',df.var(),'→ std,var分别求标准差，方差\n')
print(df.skew(),'→ skew样本的偏度\n')
print(df.kurt(),'→ kurt样本的峰度\n')
```

       key1      key2
    0     0  4.667989
    1     1  4.336625
    2     2  0.746852
    3     3  9.670919
    4     4  8.732045
    5     5  0.013751
    6     6  8.963752
    7     7  0.279303
    8     8  8.586821
    9     9  8.899657
    -----
    key1    10
    key2    10
    dtype: int64 → count统计非Na值的数量
    
    key1    0.000000
    key2    0.013751
    dtype: float64 → min统计最小值
     9.67091932107 → max统计最大值
    
    key1    6.750000
    key2    8.857754
    dtype: float64 → quantile统计分位数，参数q确定位置
    
    key1    45.000000
    key2    54.897714
    dtype: float64 → sum求和
    
    key1    4.500000
    key2    5.489771
    dtype: float64 → mean求平均值
    
    key1    4.500000
    key2    6.627405
    dtype: float64 → median求算数中位数，50%分位数
    
    key1    3.027650
    key2    3.984945
    dtype: float64 
     key1     9.166667
    key2    15.879783
    dtype: float64 → std,var分别求标准差，方差
    
    key1    0.000000
    key2   -0.430166
    dtype: float64 → skew样本的偏度
    
    key1   -1.200000
    key2   -1.800296
    dtype: float64 → kurt样本的峰度
    
    


```python
# 主要数学计算方法，可用于Series和DataFrame（2）

df['key1_s'] = df['key1'].cumsum()
df['key2_s'] = df['key2'].cumsum()
print(df,'→ cumsum样本的累计和\n')

df['key1_p'] = df['key1'].cumprod()
df['key2_p'] = df['key2'].cumprod()
print(df,'→ cumprod样本的累计积\n')

print(df.cummax(),'\n',df.cummin(),'→ cummax,cummin分别求累计最大值，累计最小值\n')
# 会填充key1，和key2的值
```

       key1      key2  key1_s     key2_s
    0     0  4.667989       0   4.667989
    1     1  4.336625       1   9.004614
    2     2  0.746852       3   9.751466
    3     3  9.670919       6  19.422386
    4     4  8.732045      10  28.154431
    5     5  0.013751      15  28.168182
    6     6  8.963752      21  37.131934
    7     7  0.279303      28  37.411236
    8     8  8.586821      36  45.998057
    9     9  8.899657      45  54.897714 → cumsum样本的累计和
    
       key1      key2  key1_s     key2_s  key1_p       key2_p
    0     0  4.667989       0   4.667989       0     4.667989
    1     1  4.336625       1   9.004614       0    20.243318
    2     2  0.746852       3   9.751466       0    15.118767
    3     3  9.670919       6  19.422386       0   146.212377
    4     4  8.732045      10  28.154431       0  1276.733069
    5     5  0.013751      15  28.168182       0    17.556729
    6     6  8.963752      21  37.131934       0   157.374157
    7     7  0.279303      28  37.411236       0    43.955024
    8     8  8.586821      36  45.998057       0   377.433921
    9     9  8.899657      45  54.897714       0  3359.032396 → cumprod样本的累计积
    
       key1      key2  key1_s     key2_s  key1_p       key2_p
    0   0.0  4.667989     0.0   4.667989     0.0     4.667989
    1   1.0  4.667989     1.0   9.004614     0.0    20.243318
    2   2.0  4.667989     3.0   9.751466     0.0    20.243318
    3   3.0  9.670919     6.0  19.422386     0.0   146.212377
    4   4.0  9.670919    10.0  28.154431     0.0  1276.733069
    5   5.0  9.670919    15.0  28.168182     0.0  1276.733069
    6   6.0  9.670919    21.0  37.131934     0.0  1276.733069
    7   7.0  9.670919    28.0  37.411236     0.0  1276.733069
    8   8.0  9.670919    36.0  45.998057     0.0  1276.733069
    9   9.0  9.670919    45.0  54.897714     0.0  3359.032396 
        key1      key2  key1_s    key2_s  key1_p    key2_p
    0   0.0  4.667989     0.0  4.667989     0.0  4.667989
    1   0.0  4.336625     0.0  4.667989     0.0  4.667989
    2   0.0  0.746852     0.0  4.667989     0.0  4.667989
    3   0.0  0.746852     0.0  4.667989     0.0  4.667989
    4   0.0  0.746852     0.0  4.667989     0.0  4.667989
    5   0.0  0.013751     0.0  4.667989     0.0  4.667989
    6   0.0  0.013751     0.0  4.667989     0.0  4.667989
    7   0.0  0.013751     0.0  4.667989     0.0  4.667989
    8   0.0  0.013751     0.0  4.667989     0.0  4.667989
    9   0.0  0.013751     0.0  4.667989     0.0  4.667989 → cummax,cummin分别求累计最大值，累计最小值
    
    


```python
# 唯一值：.unique()

s = pd.Series(list('asdvasdcfgg'))
sq = s.unique()
print(s)
print(sq,type(sq))
print(pd.Series(sq))
# 得到一个唯一值数组
# 通过pd.Series重新变成新的Series

sq.sort()
print(sq)
# 重新排序
```

    0     a
    1     s
    2     d
    3     v
    4     a
    5     s
    6     d
    7     c
    8     f
    9     g
    10    g
    dtype: object
    ['a' 's' 'd' 'v' 'c' 'f' 'g'] <class 'numpy.ndarray'>
    0    a
    1    s
    2    d
    3    v
    4    c
    5    f
    6    g
    dtype: object
    ['a' 'c' 'd' 'f' 'g' 's' 'v']
    


```python
# 值计数：.value_counts()

sc = s.value_counts(sort = False)  # 也可以这样写：pd.value_counts(sc, sort = False)
print(sc)
# 得到一个新的Series，计算出不同值出现的频率
# sort参数：排序，默认为True
```

    s    2
    d    2
    v    1
    c    1
    a    2
    g    2
    f    1
    dtype: int64
    


```python
# 成员资格：.isin()

s = pd.Series(np.arange(10,15))
df = pd.DataFrame({'key1':list('asdcbvasd'),
                  'key2':np.arange(4,13)})
print(s)
print(df)
print('-----')

print(s.isin([5,14]))
print(df.isin(['a','bc','10',8]))
# 用[]表示
# 得到一个布尔值的Series或者Dataframe
```

    0    10
    1    11
    2    12
    3    13
    4    14
    dtype: int32
      key1  key2
    0    a     4
    1    s     5
    2    d     6
    3    c     7
    4    b     8
    5    v     9
    6    a    10
    7    s    11
    8    d    12
    -----
    0    False
    1    False
    2    False
    3    False
    4     True
    dtype: bool
        key1   key2
    0   True  False
    1  False  False
    2  False  False
    3  False  False
    4  False   True
    5  False  False
    6   True  False
    7  False  False
    8  False  False
    


```python
'''
【课程2.15】  文本数据

Pandas针对字符串配备的一套方法，使其易于对数组的每个元素进行操作
 
'''
```


```python
# 通过str访问，且自动排除丢失/ NA值

s = pd.Series(['A','b','C','bbhello','123',np.nan,'hj'])
df = pd.DataFrame({'key1':list('abcdef'),
                  'key2':['hee','fv','w','hija','123',np.nan]})
print(s)
print(df)
print('-----')
print(s.str.count('b'))
print(df['key2'].str.upper())
# print(df['key1'].str.upper())  # dateframe 不能直接调用str?
print('-----')
# 直接通过.str调用字符串方法
# 可以对Series、Dataframe使用
# 自动过滤NaN值

df.columns = df.columns.str.upper()
print(df)
# df.columns是一个Index对象，也可使用.str
```

    0          A
    1          b
    2          C
    3    bbhello
    4        123
    5        NaN
    6         hj
    dtype: object
      key1  key2
    0    a   hee
    1    b    fv
    2    c     w
    3    d  hija
    4    e   123
    5    f   NaN
    -----
    0    0.0
    1    1.0
    2    0.0
    3    2.0
    4    0.0
    5    NaN
    6    0.0
    dtype: float64
    0     HEE
    1      FV
    2       W
    3    HIJA
    4     123
    5     NaN
    Name: key2, dtype: object
    -----
      KEY1  KEY2
    0    a   hee
    1    b    fv
    2    c     w
    3    d  hija
    4    e   123
    5    f   NaN
    


```python
# 字符串常用方法（1） - lower，upper，len，startswith，endswith

s = pd.Series(['A','b','bbhello','123',np.nan])

print(s.str.lower(),'→ lower小写\n')
print(s.str.upper(),'→ upper大写\n')
print(s.str.len(),'→ len字符长度\n')
print(s.str.startswith('b'),'→ 判断起始是否为a\n')
print(s.str.endswith('3'),'→ 判断结束是否为3\n')
```

    0          a
    1          b
    2    bbhello
    3        123
    4        NaN
    dtype: object → lower小写
    
    0          A
    1          B
    2    BBHELLO
    3        123
    4        NaN
    dtype: object → upper大写
    
    0    1.0
    1    1.0
    2    7.0
    3    3.0
    4    NaN
    dtype: float64 → len字符长度
    
    0    False
    1     True
    2     True
    3    False
    4      NaN
    dtype: object → 判断起始是否为a
    
    0    False
    1    False
    2    False
    3     True
    4      NaN
    dtype: object → 判断结束是否为3
    
    


```python
# 字符串常用方法（2） - strip

s = pd.Series([' jack', 'jill ', ' jesse ', 'frank'])
df = pd.DataFrame(np.random.randn(3, 2), columns=[' Column A ', ' Column B '],
                  index=range(3))
print(s)
print(df)
print('-----')

print(s.str.strip())  # 去除字符串中的空格
print(s.str.lstrip())  # 去除字符串中的左空格
print(s.str.rstrip())  # 去除字符串中的右空格

df.columns = df.columns.str.strip()
print(df)
# 这里去掉了columns的前后空格，但没有去掉中间空格
```

    0       jack
    1      jill 
    2     jesse 
    3      frank
    dtype: object
        Column A    Column B 
    0    0.647766    0.094747
    1    0.342940   -0.660643
    2    1.183315   -0.143729
    -----
    0     jack
    1     jill
    2    jesse
    3    frank
    dtype: object
    0      jack
    1     jill 
    2    jesse 
    3     frank
    dtype: object
    0      jack
    1      jill
    2     jesse
    3     frank
    dtype: object
       Column A  Column B
    0  0.647766  0.094747
    1  0.342940 -0.660643
    2  1.183315 -0.143729
    


```python
# 字符串常用方法（3） - replace

df = pd.DataFrame(np.random.randn(3, 2), columns=[' Column A ', ' Column B '],
                  index=range(3))
df.columns = df.columns.str.replace(' ','-')
print(df)
# 替换

df.columns = df.columns.str.replace('-','hehe',n=1)
print(df)
# n：替换个数
```

       -Column-A-  -Column-B-
    0    0.754580    1.414158
    1    0.020862    0.358670
    2    0.137037    0.908150
       heheColumn-A-  heheColumn-B-
    0       0.754580       1.414158
    1       0.020862       0.358670
    2       0.137037       0.908150
    


```python
# 字符串常用方法（4） - split、rsplit

s = pd.Series(['a,b,c','1,2,3',['a,,,c'],np.nan])
print(s)
print(s.str.split(','))
print('-----')
# 类似字符串的split

print(s.str.split(',')[0])
print('-----')
# 直接索引得到一个list

print(s.str.split(',').str[0])
print(s.str.split(',').str.get(1))
print('-----')
# 可以使用get或[]符号访问拆分列表中的元素

print(s.str.split(',', expand=True))
print(s.str.split(',', expand=True, n = 1))
print(s.str.rsplit(',', expand=True, n = 1))
print('-----')
# 可以使用expand可以轻松扩展此操作以返回DataFrame
# n参数限制分割数
# rsplit类似于split，反向工作，即从字符串的末尾到字符串的开头

df = pd.DataFrame({'key1':['a,b,c','1,2,3',[':,., ']],
                  'key2':['a-b-c','1-2-3',[':-.- ']]})
print(df['key2'].str.split('-'))
# Dataframe使用split
```

    0      a,b,c
    1      1,2,3
    2    [a,,,c]
    3        NaN
    dtype: object
    0    [a, b, c]
    1    [1, 2, 3]
    2          NaN
    3          NaN
    dtype: object
    -----
    ['a', 'b', 'c']
    -----
    0      a
    1      1
    2    NaN
    3    NaN
    dtype: object
    0      b
    1      2
    2    NaN
    3    NaN
    dtype: object
    -----
         0    1    2
    0    a    b    c
    1    1    2    3
    2  NaN  NaN  NaN
    3  NaN  NaN  NaN
         0    1
    0    a  b,c
    1    1  2,3
    2  NaN  NaN
    3  NaN  NaN
         0    1
    0  a,b    c
    1  1,2    3
    2  NaN  NaN
    3  NaN  NaN
    -----
    0    [a, b, c]
    1    [1, 2, 3]
    2          NaN
    Name: key2, dtype: object
    


```python
# 字符串索引

s = pd.Series(['A','b','C','bbhello','123',np.nan,'hj'])
df = pd.DataFrame({'key1':list('abcdef'),
                  'key2':['hee','fv','w','hija','123',np.nan]})

print(s.str[0])  # 取第一个字符串
print(s.str[:2])  # 取前两个字符串
print(df['key2'].str[0]) 
# str之后和字符串本身索引方式相同
```

    0      A
    1      b
    2      C
    3      b
    4      1
    5    NaN
    6      h
    dtype: object
    0      A
    1      b
    2      C
    3     bb
    4     12
    5    NaN
    6     hj
    dtype: object
    0      h
    1      f
    2      w
    3      h
    4      1
    5    NaN
    Name: key2, dtype: object
    


```python
'''
【课程2.16】  合并 merge、join

Pandas具有全功能的，高性能内存中连接操作，与SQL等关系数据库非常相似

pd.merge(left, right, how='inner', on=None, left_on=None, right_on=None,
         left_index=False, right_index=False, sort=True,
         suffixes=('_x', '_y'), copy=True, indicator=False)
 
'''
```


```python
# merge合并 → 类似excel的vlookup

df1 = pd.DataFrame({'key': ['K0', 'K1', 'K2', 'K3'],
                     'A': ['A0', 'A1', 'A2', 'A3'],
                     'B': ['B0', 'B1', 'B2', 'B3']})
df2 = pd.DataFrame({'key': ['K0', 'K1', 'K2', 'K3'],
                      'C': ['C0', 'C1', 'C2', 'C3'],
                      'D': ['D0', 'D1', 'D2', 'D3']})
df3 = pd.DataFrame({'key1': ['K0', 'K0', 'K1', 'K2'],
                    'key2': ['K0', 'K1', 'K0', 'K1'],
                    'A': ['A0', 'A1', 'A2', 'A3'],
                    'B': ['B0', 'B1', 'B2', 'B3']})
df4 = pd.DataFrame({'key1': ['K0', 'K1', 'K1', 'K2'],
                    'key2': ['K0', 'K0', 'K0', 'K0'],
                    'C': ['C0', 'C1', 'C2', 'C3'],
                    'D': ['D0', 'D1', 'D2', 'D3']})
print(pd.merge(df1, df2, on='key'))
print('------')
# left：第一个df
# right：第二个df
# on：参考键

print(pd.merge(df3, df4, on=['key1','key2']))
# 多个链接键
```

        A   B key   C   D
    0  A0  B0  K0  C0  D0
    1  A1  B1  K1  C1  D1
    2  A2  B2  K2  C2  D2
    3  A3  B3  K3  C3  D3
    ------
        A   B key1 key2   C   D
    0  A0  B0   K0   K0  C0  D0
    1  A2  B2   K1   K0  C1  D1
    2  A2  B2   K1   K0  C2  D2
    


```python
# 参数how → 合并方式

print(pd.merge(df3, df4,on=['key1','key2'], how = 'inner'))  
print('------')
# inner：默认，取交集

print(pd.merge(df3, df4, on=['key1','key2'], how = 'outer'))  
print('------')
# outer：取并集，数据缺失范围NaN

print(pd.merge(df3, df4, on=['key1','key2'], how = 'left'))  
print('------')
# left：按照df3为参考合并，数据缺失范围NaN

print(pd.merge(df3, df4, on=['key1','key2'], how = 'right'))  
# right：按照df4为参考合并，数据缺失范围NaN
```

        A   B key1 key2   C   D
    0  A0  B0   K0   K0  C0  D0
    1  A2  B2   K1   K0  C1  D1
    2  A2  B2   K1   K0  C2  D2
    ------
         A    B key1 key2    C    D
    0   A0   B0   K0   K0   C0   D0
    1   A1   B1   K0   K1  NaN  NaN
    2   A2   B2   K1   K0   C1   D1
    3   A2   B2   K1   K0   C2   D2
    4   A3   B3   K2   K1  NaN  NaN
    5  NaN  NaN   K2   K0   C3   D3
    ------
        A   B key1 key2    C    D
    0  A0  B0   K0   K0   C0   D0
    1  A1  B1   K0   K1  NaN  NaN
    2  A2  B2   K1   K0   C1   D1
    3  A2  B2   K1   K0   C2   D2
    4  A3  B3   K2   K1  NaN  NaN
    ------
         A    B key1 key2   C   D
    0   A0   B0   K0   K0  C0  D0
    1   A2   B2   K1   K0  C1  D1
    2   A2   B2   K1   K0  C2  D2
    3  NaN  NaN   K2   K0  C3  D3
    


```python
# 参数 left_on, right_on, left_index, right_index → 当键不为一个列时，可以单独设置左键与右键

df1 = pd.DataFrame({'lkey':list('bbacaab'),
                   'data1':range(7)})
df2 = pd.DataFrame({'rkey':list('abd'),
                   'date2':range(3)})
print(df1)
print(df2)
print(pd.merge(df1, df2, left_on='lkey', right_on='rkey'))
print('------')
# df1以‘lkey’为键，df2以‘rkey’为键

df1 = pd.DataFrame({'key':list('abcdfeg'),
                   'data1':range(7)})
df2 = pd.DataFrame({'date2':range(100,105)},
                  index = list('abcde'))
print(df1)
print(df2)
print(pd.merge(df1, df2, left_on='key', right_index=True))
# df1以‘key’为键，df2以index为键
# left_index：为True时，第一个df以index为键，默认False
# right_index：为True时，第二个df以index为键，默认False

# 所以left_on, right_on, left_index, right_index可以相互组合：
# left_on + right_on, left_on + right_index, left_index + right_on, left_index + right_index
```

      lkey  data1
    0    b      0
    1    b      1
    2    a      2
    3    c      3
    4    a      4
    5    a      5
    6    b      6
      rkey  date2
    0    a      0
    1    b      1
    2    d      2
      lkey  data1 rkey  date2
    0    b      0    b      1
    1    b      1    b      1
    2    b      6    b      1
    3    a      2    a      0
    4    a      4    a      0
    5    a      5    a      0
    ------
      key  data1
    0   a      0
    1   b      1
    2   c      2
    3   d      3
    4   f      4
    5   e      5
    6   g      6
       date2
    a    100
    b    101
    c    102
    d    103
    e    104
      key  data1  date2
    0   a      0    100
    1   b      1    101
    2   c      2    102
    3   d      3    103
    5   e      5    104
    


```python
# 参数 sort

df1 = pd.DataFrame({'key':list('bbacaab'),
                   'data1':[1,3,2,4,5,9,7]})
df2 = pd.DataFrame({'key':list('abd'),
                   'date2':[11,2,33]})
x1 = pd.merge(df1,df2, on = 'key', how = 'outer')
x2 = pd.merge(df1,df2, on = 'key', sort=True, how = 'outer')
print(x1)
print(x2)
print('------')
# sort：按照字典顺序通过 连接键 对结果DataFrame进行排序。默认为False，设置为False会大幅提高性能

print(x2.sort_values('data1'))
# 也可直接用Dataframe的排序方法：sort_values，sort_index
```

       data1 key  date2
    0    1.0   b    2.0
    1    3.0   b    2.0
    2    7.0   b    2.0
    3    2.0   a   11.0
    4    5.0   a   11.0
    5    9.0   a   11.0
    6    4.0   c    NaN
    7    NaN   d   33.0
       data1 key  date2
    0    2.0   a   11.0
    1    5.0   a   11.0
    2    9.0   a   11.0
    3    1.0   b    2.0
    4    3.0   b    2.0
    5    7.0   b    2.0
    6    4.0   c    NaN
    7    NaN   d   33.0
    ------
       data1 key  date2
    3    1.0   b    2.0
    0    2.0   a   11.0
    4    3.0   b    2.0
    6    4.0   c    NaN
    1    5.0   a   11.0
    5    7.0   b    2.0
    2    9.0   a   11.0
    7    NaN   d   33.0
    


```python
# pd.join() → 直接通过索引链接

left = pd.DataFrame({'A': ['A0', 'A1', 'A2'],
                     'B': ['B0', 'B1', 'B2']},
                    index=['K0', 'K1', 'K2'])
right = pd.DataFrame({'C': ['C0', 'C2', 'C3'],
                      'D': ['D0', 'D2', 'D3']},
                     index=['K0', 'K2', 'K3'])
print(left)
print(right)
print(left.join(right))
print(left.join(right, how='outer'))  
print('-----')
# 等价于：pd.merge(left, right, left_index=True, right_index=True, how='outer')

df1 = pd.DataFrame({'key':list('bbacaab'),
                   'data1':[1,3,2,4,5,9,7]})
df2 = pd.DataFrame({'key':list('abd'),
                   'date2':[11,2,33]})
print(df1)
print(df2)
print(pd.merge(df1, df2, left_index=True, right_index=True, suffixes=('_1', '_2')))  
print(df1.join(df2['date2']))
print('-----')
# suffixes=('_x', '_y')默认

left = pd.DataFrame({'A': ['A0', 'A1', 'A2', 'A3'],
                     'B': ['B0', 'B1', 'B2', 'B3'],
                     'key': ['K0', 'K1', 'K0', 'K1']})
right = pd.DataFrame({'C': ['C0', 'C1'],
                      'D': ['D0', 'D1']},
                     index=['K0', 'K1'])
print(left)
print(right)
print(left.join(right, on = 'key'))
# 等价于pd.merge(left, right, left_on='key', right_index=True, how='left', sort=False);
# left的‘key’和right的index
```

         A   B
    K0  A0  B0
    K1  A1  B1
    K2  A2  B2
         C   D
    K0  C0  D0
    K2  C2  D2
    K3  C3  D3
         A   B    C    D
    K0  A0  B0   C0   D0
    K1  A1  B1  NaN  NaN
    K2  A2  B2   C2   D2
          A    B    C    D
    K0   A0   B0   C0   D0
    K1   A1   B1  NaN  NaN
    K2   A2   B2   C2   D2
    K3  NaN  NaN   C3   D3
    -----
       data1 key
    0      1   b
    1      3   b
    2      2   a
    3      4   c
    4      5   a
    5      9   a
    6      7   b
       date2 key
    0     11   a
    1      2   b
    2     33   d
       data1 key_1  date2 key_2
    0      1     b     11     a
    1      3     b      2     b
    2      2     a     33     d
       data1 key  date2
    0      1   b   11.0
    1      3   b    2.0
    2      2   a   33.0
    3      4   c    NaN
    4      5   a    NaN
    5      9   a    NaN
    6      7   b    NaN
    -----
        A   B key
    0  A0  B0  K0
    1  A1  B1  K1
    2  A2  B2  K0
    3  A3  B3  K1
         C   D
    K0  C0  D0
    K1  C1  D1
        A   B key   C   D
    0  A0  B0  K0  C0  D0
    1  A1  B1  K1  C1  D1
    2  A2  B2  K0  C0  D0
    3  A3  B3  K1  C1  D1
    


```python
'''
【课程2.17】  连接与修补 concat、combine_first

连接 - 沿轴执行连接操作

pd.concat(objs, axis=0, join='outer', join_axes=None, ignore_index=False,
          keys=None, levels=None, names=None, verify_integrity=False,
          copy=True)
 
'''
```


```python
# 连接：concat

s1 = pd.Series([1,2,3])
s2 = pd.Series([2,3,4])
s3 = pd.Series([1,2,3],index = ['a','c','h'])
s4 = pd.Series([2,3,4],index = ['b','e','d'])
print(pd.concat([s1,s2]))
print(pd.concat([s3,s4]).sort_index())
print('-----')
# 默认axis=0，行+行

print(pd.concat([s3,s4], axis=1))
print('-----')
# axis=1,列+列，成为一个Dataframe
```

    0    1
    1    2
    2    3
    0    2
    1    3
    2    4
    dtype: int64
    a    1
    b    2
    c    2
    d    4
    e    3
    h    3
    dtype: int64
    -----
         0    1
    a  1.0  NaN
    b  NaN  2.0
    c  2.0  NaN
    d  NaN  4.0
    e  NaN  3.0
    h  3.0  NaN
    -----
    


```python
# 连接方式：join，join_axes

s5 = pd.Series([1,2,3],index = ['a','b','c'])
s6 = pd.Series([2,3,4],index = ['b','c','d'])
print(pd.concat([s5,s6], axis= 1))
print(pd.concat([s5,s6], axis= 1, join='inner'))
print(pd.concat([s5,s6], axis= 1, join_axes=[['a','b','d']]))
# join：{'inner'，'outer'}，默认为“outer”。如何处理其他轴上的索引。outer为联合和inner为交集。
# join_axes：指定联合的index
```

         0    1
    a  1.0  NaN
    b  2.0  2.0
    c  3.0  3.0
    d  NaN  4.0
       0  1
    b  2  2
    c  3  3
         0    1
    a  1.0  NaN
    b  2.0  2.0
    d  NaN  4.0
    


```python
# 覆盖列名

sre = pd.concat([s5,s6], keys = ['one','two'])
print(sre,type(sre))
print(sre.index)
print('-----')
# keys：序列，默认值无。使用传递的键作为最外层构建层次索引

sre = pd.concat([s5,s6], axis=1, keys = ['one','two'])
print(sre,type(sre))
# axis = 1, 覆盖列名
```

    one  a    1
         b    2
         c    3
    two  b    2
         c    3
         d    4
    dtype: int64 <class 'pandas.core.series.Series'>
    MultiIndex(levels=[['one', 'two'], ['a', 'b', 'c', 'd']],
               labels=[[0, 0, 0, 1, 1, 1], [0, 1, 2, 1, 2, 3]])
    -----
       one  two
    a  1.0  NaN
    b  2.0  2.0
    c  3.0  3.0
    d  NaN  4.0 <class 'pandas.core.frame.DataFrame'>
    


```python
# 修补 pd.combine_first()

df1 = pd.DataFrame([[np.nan, 3., 5.], [-4.6, np.nan, np.nan],[np.nan, 7., np.nan]])
df2 = pd.DataFrame([[-42.6, np.nan, -8.2], [-5., 1.6, 4]],index=[1, 2])
print(df1)
print(df2)
print(df1.combine_first(df2))
print('-----')
# 根据index，df1的空值被df2替代
# 如果df2的index多于df1，则更新到df1上，比如index=['a',1]

df1.update(df2)
print(df1)
# update，直接df2覆盖df1，相同index位置
```

         0    1    2
    0  NaN  3.0  5.0
    1 -4.6  NaN  NaN
    2  NaN  7.0  NaN
          0    1    2
    1 -42.6  NaN -8.2
    2  -5.0  1.6  4.0
         0    1    2
    0  NaN  3.0  5.0
    1 -4.6  NaN -8.2
    2 -5.0  7.0  4.0
    -----
          0    1    2
    0   NaN  3.0  5.0
    1 -42.6  NaN -8.2
    2  -5.0  1.6  4.0
    


```python
'''
【课程2.18】  去重及替换

.duplicated / .replace
 
'''
```


```python
# 去重 .duplicated

s = pd.Series([1,1,1,1,2,2,2,3,4,5,5,5,5])
print(s.duplicated())
print(s[s.duplicated() == False])
print('-----')
# 判断是否重复
# 通过布尔判断，得到不重复的值

s_re = s.drop_duplicates()
print(s_re)
print('-----')
# drop.duplicates移除重复
# inplace参数：是否替换原值，默认False

df = pd.DataFrame({'key1':['a','a',3,4,5],
                  'key2':['a','a','b','b','c']})
print(df.duplicated())
print(df['key2'].duplicated())
# Dataframe中使用duplicated
```

    0     False
    1      True
    2      True
    3      True
    4     False
    5      True
    6      True
    7     False
    8     False
    9     False
    10     True
    11     True
    12     True
    dtype: bool
    0    1
    4    2
    7    3
    8    4
    9    5
    dtype: int64
    -----
    0    1
    4    2
    7    3
    8    4
    9    5
    dtype: int64
    -----
    0    False
    1     True
    2    False
    3    False
    4    False
    dtype: bool
    0    False
    1     True
    2    False
    3     True
    4    False
    Name: key2, dtype: bool
    


```python
# 替换 .replace

s = pd.Series(list('ascaazsd'))
print(s.replace('a', np.nan))
print(s.replace(['a','s'] ,np.nan))
print(s.replace({'a':'hello world!','s':123}))
# 可一次性替换一个值或多个值
# 可传入列表或字典
```

    0    NaN
    1      s
    2      c
    3    NaN
    4    NaN
    5      z
    6      s
    7      d
    dtype: object
    0    NaN
    1    NaN
    2      c
    3    NaN
    4    NaN
    5      z
    6    NaN
    7      d
    dtype: object
    0    hello world!
    1             123
    2               c
    3    hello world!
    4    hello world!
    5               z
    6             123
    7               d
    dtype: object
    


```python
'''
【课程2.19】  数据分组

分组统计 - groupby功能

① 根据某些条件将数据拆分成组
② 对每个组独立应用函数
③ 将结果合并到一个数据结构中

Dataframe在行（axis=0）或列（axis=1）上进行分组，将一个函数应用到各个分组并产生一个新值，然后函数执行结果被合并到最终的结果对象中。

df.groupby(by=None, axis=0, level=None, as_index=True, sort=True, group_keys=True, squeeze=False, **kwargs)
 
'''
```


```python
# 分组

df = pd.DataFrame({'A' : ['foo', 'bar', 'foo', 'bar','foo', 'bar', 'foo', 'foo'],
                   'B' : ['one', 'one', 'two', 'three', 'two', 'two', 'one', 'three'],
                   'C' : np.random.randn(8),
                   'D' : np.random.randn(8)})
print(df)
print('------')

print(df.groupby('A'), type(df.groupby('A')))
print('------')
# 直接分组得到一个groupby对象，是一个中间数据，没有进行计算

a = df.groupby('A').mean()
b = df.groupby(['A','B']).mean()
c = df.groupby(['A'])['D'].mean()  # 以A分组，算D的平均值
print(a,type(a),'\n',a.columns)
print(b,type(b),'\n',b.columns)
print(c,type(c))
# 通过分组后的计算，得到一个新的dataframe
# 默认axis = 0，以行来分组
# 可单个或多个（[]）列分组
```

         A      B         C         D
    0  foo    one  0.891765 -1.121156
    1  bar    one -1.272769  1.188977
    2  foo    two  0.198131  0.543673
    3  bar  three -0.827655 -1.608699
    4  foo    two -1.114089 -0.696145
    5  bar    two -0.345336  0.718507
    6  foo    one -0.207091 -0.922269
    7  foo  three -0.431760 -0.123696
    ------
    <pandas.core.groupby.DataFrameGroupBy object at 0x0000000004B65E10> <class 'pandas.core.groupby.DataFrameGroupBy'>
    ------
                C         D
    A                      
    bar -0.815253  0.099595
    foo -0.132609 -0.463918 <class 'pandas.core.frame.DataFrame'> 
     Index(['C', 'D'], dtype='object')
                      C         D
    A   B                        
    bar one   -1.272769  1.188977
        three -0.827655 -1.608699
        two   -0.345336  0.718507
    foo one    0.342337 -1.021713
        three -0.431760 -0.123696
        two   -0.457979 -0.076236 <class 'pandas.core.frame.DataFrame'> 
     Index(['C', 'D'], dtype='object')
    A
    bar    0.099595
    foo   -0.463918
    Name: D, dtype: float64 <class 'pandas.core.series.Series'>
    


```python
# 分组 - 可迭代对象

df = pd.DataFrame({'X' : ['A', 'B', 'A', 'B'], 'Y' : [1, 4, 3, 2]})
print(df)
print(df.groupby('X'), type(df.groupby('X')))
print('-----')

print(list(df.groupby('X')), '→ 可迭代对象，直接生成list\n')
print(list(df.groupby('X'))[0], '→ 以元祖形式显示\n')
for n,g in df.groupby('X'):
    print(n)
    print(g)
    print('###')
print('-----')
# n是组名，g是分组后的Dataframe

print(df.groupby(['X']).get_group('A'),'\n')
print(df.groupby(['X']).get_group('B'),'\n')
print('-----')
# .get_group()提取分组后的组

grouped = df.groupby(['X'])
print(grouped.groups)
print(grouped.groups['A'])  # 也可写：df.groupby('X').groups['A']
print('-----')
# .groups：将分组后的groups转为dict
# 可以字典索引方法来查看groups里的元素

sz = grouped.size()
print(sz,type(sz))
print('-----')
# .size()：查看分组后的长度

df = pd.DataFrame({'A' : ['foo', 'bar', 'foo', 'bar','foo', 'bar', 'foo', 'foo'],
                   'B' : ['one', 'one', 'two', 'three', 'two', 'two', 'one', 'three'],
                   'C' : np.random.randn(8),
                   'D' : np.random.randn(8)})
grouped = df.groupby(['A','B']).groups
print(df)
print(grouped)
print(grouped[('foo', 'three')])
# 按照两个列进行分组
```

       X  Y
    0  A  1
    1  B  4
    2  A  3
    3  B  2
    <pandas.core.groupby.DataFrameGroupBy object at 0x00000000091B6F28> <class 'pandas.core.groupby.DataFrameGroupBy'>
    -----
    [('A',    X  Y
    0  A  1
    2  A  3), ('B',    X  Y
    1  B  4
    3  B  2)] → 可迭代对象，直接生成list
    
    ('A',    X  Y
    0  A  1
    2  A  3) → 以元祖形式显示
    
    A
       X  Y
    0  A  1
    2  A  3
    ###
    B
       X  Y
    1  B  4
    3  B  2
    ###
    -----
       X  Y
    0  A  1
    2  A  3 
    
       X  Y
    1  B  4
    3  B  2 
    
    -----
    {'B': [1, 3], 'A': [0, 2]}
    [0, 2]
    -----
    X
    A    2
    B    2
    dtype: int64 <class 'pandas.core.series.Series'>
    -----
         A      B         C         D
    0  foo    one -0.668695  0.247781
    1  bar    one -0.125374  2.259134
    2  foo    two -0.112052  1.618603
    3  bar  three -0.098986  0.150488
    4  foo    two  0.912286 -1.260029
    5  bar    two  1.096757 -0.571223
    6  foo    one -0.090907 -1.671482
    7  foo  three  0.088176 -0.292702
    {('bar', 'two'): [5], ('foo', 'two'): [2, 4], ('bar', 'one'): [1], ('foo', 'three'): [7], ('bar', 'three'): [3], ('foo', 'one'): [0, 6]}
    [7]
    


```python
# 其他轴上的分组

df = pd.DataFrame({'data1':np.random.rand(2),
                  'data2':np.random.rand(2),
                  'key1':['a','b'],
                  'key2':['one','two']})
print(df)
print(df.dtypes)
print('-----')
for n,p in df.groupby(df.dtypes, axis=1):
    print(n)
    print(p)
    print('##')
# 按照值类型分列
```

          data1     data2 key1 key2
    0  0.454580  0.692637    a  one
    1  0.496928  0.214309    b  two
    data1    float64
    data2    float64
    key1      object
    key2      object
    dtype: object
    -----
    float64
          data1     data2
    0  0.454580  0.692637
    1  0.496928  0.214309
    ##
    object
      key1 key2
    0    a  one
    1    b  two
    ##
    


```python
# 通过字典或者Series分组

df = pd.DataFrame(np.arange(16).reshape(4,4),
                  columns = ['a','b','c','d'])
print(df)
print('-----')

mapping = {'a':'one','b':'one','c':'two','d':'two','e':'three'}
by_column = df.groupby(mapping, axis = 1)
print(by_column.sum())
print('-----')
# mapping中，a、b列对应的为one，c、d列对应的为two，以字典来分组

s = pd.Series(mapping)
print(s,'\n')
print(s.groupby(s).count())
# s中，index中a、b对应的为one，c、d对应的为two，以Series来分组
```

        a   b   c   d
    0   0   1   2   3
    1   4   5   6   7
    2   8   9  10  11
    3  12  13  14  15
    -----
       one  two
    0    1    5
    1    9   13
    2   17   21
    3   25   29
    -----
    a      one
    b      one
    c      two
    d      two
    e    three
    dtype: object 
    
    one      2
    three    1
    two      2
    dtype: int64
    


```python
# 通过函数分组

df = pd.DataFrame(np.arange(16).reshape(4,4),
                  columns = ['a','b','c','d'],
                 index = ['abc','bcd','aa','b'])
print(df,'\n')
print(df.groupby(len).sum())
# 按照字母长度分组
```

          a   b   c   d
    abc   0   1   2   3
    bcd   4   5   6   7
    aa    8   9  10  11
    b    12  13  14  15 
    
        a   b   c   d
    1  12  13  14  15
    2   8   9  10  11
    3   4   6   8  10
    


```python
# 分组计算函数方法

s = pd.Series([1, 2, 3, 10, 20, 30], index = [1, 2, 3, 1, 2, 3])
grouped = s.groupby(level=0)  # 唯一索引用.groupby(level=0)，将同一个index的分为一组
print(grouped)
print(grouped.first(),'→ first：非NaN的第一个值\n')
print(grouped.last(),'→ last：非NaN的最后一个值\n')
print(grouped.sum(),'→ sum：非NaN的和\n')
print(grouped.mean(),'→ mean：非NaN的平均值\n')
print(grouped.median(),'→ median：非NaN的算术中位数\n')
print(grouped.count(),'→ count：非NaN的值\n')
print(grouped.min(),'→ min、max：非NaN的最小值、最大值\n')
print(grouped.std(),'→ std，var：非NaN的标准差和方差\n')
print(grouped.prod(),'→ prod：非NaN的积\n')
```

    <pandas.core.groupby.SeriesGroupBy object at 0x00000000091992B0>
    1    1
    2    2
    3    3
    dtype: int64 → first：非NaN的第一个值
    
    1    10
    2    20
    3    30
    dtype: int64 → last：非NaN的最后一个值
    
    1    11
    2    22
    3    33
    dtype: int64 → sum：非NaN的和
    
    1     5.5
    2    11.0
    3    16.5
    dtype: float64 → mean：非NaN的平均值
    
    1     5.5
    2    11.0
    3    16.5
    dtype: float64 → median：非NaN的算术中位数
    
    1    2
    2    2
    3    2
    dtype: int64 → count：非NaN的值
    
    1    1
    2    2
    3    3
    dtype: int64 → min、max：非NaN的最小值、最大值
    
    1     6.363961
    2    12.727922
    3    19.091883
    dtype: float64 → std，var：非NaN的标准差和方差
    
    1    10
    2    40
    3    90
    dtype: int64 → prod：非NaN的积
    
    


```python
# 多函数计算：agg()

df = pd.DataFrame({'a':[1,1,2,2],
                  'b':np.random.rand(4),
                  'c':np.random.rand(4),
                  'd':np.random.rand(4),})
print(df)
print(df.groupby('a').agg(['mean',np.sum]))
print(df.groupby('a')['b'].agg({'result1':np.mean,
                               'result2':np.sum}))
# 函数写法可以用str，或者np.方法
# 可以通过list，dict传入，当用dict时，key名为columns
```

       a         b         c         d
    0  1  0.357911  0.318324  0.627797
    1  1  0.964829  0.500017  0.570063
    2  2  0.116608  0.194164  0.049509
    3  2  0.933123  0.542615  0.718640
              b                   c                   d         
           mean       sum      mean       sum      mean      sum
    a                                                           
    1  0.661370  1.322739  0.409171  0.818341  0.598930  1.19786
    2  0.524865  1.049730  0.368390  0.736780  0.384075  0.76815
        result2   result1
    a                    
    1  1.322739  0.661370
    2  1.049730  0.524865
    

######## 本节课有作业，请查看 “课程作业.docx”  ########


```python
'''
【课程2.20】  分组转换及一般性“拆分-应用-合并”

transform / apply
 
'''
```


```python
# 数据分组转换,transform

df = pd.DataFrame({'data1':np.random.rand(5),
                  'data2':np.random.rand(5),
                  'key1':list('aabba'),
                  'key2':['one','two','one','two','one']})
k_mean = df.groupby('key1').mean()
print(df)
print(k_mean)
print(pd.merge(df,k_mean,left_on='key1',right_index=True).add_prefix('mean_'))  # .add_prefix('mean_')：添加前缀
print('-----')
# 通过分组、合并，得到一个包含均值的Dataframe

print(df.groupby('key2').mean()) # 按照key2分组求均值
print(df.groupby('key2').transform(np.mean))
# data1、data2每个位置元素取对应分组列的均值
# 字符串不能进行计算
```

          data1     data2 key1 key2
    0  0.003727  0.390301    a  one
    1  0.744777  0.130300    a  two
    2  0.887207  0.679309    b  one
    3  0.448585  0.169208    b  two
    4  0.448045  0.993775    a  one
             data1     data2
    key1                    
    a     0.398850  0.504792
    b     0.667896  0.424258
       mean_data1_x  mean_data2_x mean_key1 mean_key2  mean_data1_y  mean_data2_y
    0      0.003727      0.390301         a       one      0.398850      0.504792
    1      0.744777      0.130300         a       two      0.398850      0.504792
    4      0.448045      0.993775         a       one      0.398850      0.504792
    2      0.887207      0.679309         b       one      0.667896      0.424258
    3      0.448585      0.169208         b       two      0.667896      0.424258
    -----
             data1     data2
    key2                    
    one   0.446326  0.687795
    two   0.596681  0.149754
          data1     data2
    0  0.446326  0.687795
    1  0.596681  0.149754
    2  0.446326  0.687795
    3  0.596681  0.149754
    4  0.446326  0.687795
    


```python
# 一般化Groupby方法：apply

df = pd.DataFrame({'data1':np.random.rand(5),
                  'data2':np.random.rand(5),
                  'key1':list('aabba'),
                  'key2':['one','two','one','two','one']})

print(df.groupby('key1').apply(lambda x: x.describe()))
# apply直接运行其中的函数
# 这里为匿名函数，直接描述分组后的统计量

def f_df1(d,n):
    return(d.sort_index()[:n])
def f_df2(d,k1):
    return(d[k1])
print(df.groupby('key1').apply(f_df1,2),'\n')
print(df.groupby('key1').apply(f_df2,'data2'))
print(type(df.groupby('key1').apply(f_df2,'data2')))
# f_df1函数：返回排序后的前n行数据
# f_df2函数：返回分组后表的k1列，结果为Series，层次化索引
# 直接运行f_df函数
# 参数直接写在后面，也可以为.apply(f_df,n = 2))
```

                   data1     data2
    key1                          
    a    count  3.000000  3.000000
         mean   0.561754  0.233470
         std    0.313439  0.337209
         min    0.325604  0.026906
         25%    0.383953  0.038906
         50%    0.442303  0.050906
         75%    0.679829  0.336753
         max    0.917355  0.622599
    b    count  2.000000  2.000000
         mean   0.881906  0.547206
         std    0.079357  0.254051
         min    0.825791  0.367564
         25%    0.853849  0.457385
         50%    0.881906  0.547206
         75%    0.909963  0.637026
         max    0.938020  0.726847
               data1     data2 key1 key2
    key1                                
    a    0  0.325604  0.050906    a  one
         1  0.917355  0.622599    a  two
    b    2  0.825791  0.726847    b  one
         3  0.938020  0.367564    b  two 
    
    key1   
    a     0    0.050906
          1    0.622599
          4    0.026906
    b     2    0.726847
          3    0.367564
    Name: data2, dtype: float64
    <class 'pandas.core.series.Series'>
    

######## 本节课有作业，请查看 “课程作业.docx”  ########


```python
'''
【课程2.21】  透视表及交叉表

类似excel数据透视 - pivot table / crosstab
 
'''
```


```python
# 透视表：pivot_table
# pd.pivot_table(data, values=None, index=None, columns=None, aggfunc='mean', fill_value=None, margins=False, dropna=True, margins_name='All')

date = ['2017-5-1','2017-5-2','2017-5-3']*3
rng = pd.to_datetime(date)
df = pd.DataFrame({'date':rng,
                   'key':list('abcdabcda'),
                  'values':np.random.rand(9)*10})
print(df)
print('-----')

print(pd.pivot_table(df, values = 'values', index = 'date', columns = 'key', aggfunc=np.sum))  # 也可以写 aggfunc='sum'
print('-----')
# data：DataFrame对象
# values：要聚合的列或列的列表
# index：数据透视表的index，从原数据的列中筛选
# columns：数据透视表的columns，从原数据的列中筛选
# aggfunc：用于聚合的函数，默认为numpy.mean，支持numpy计算方法

print(pd.pivot_table(df, values = 'values', index = ['date','key'], aggfunc=len))
print('-----')
# 这里就分别以date、key共同做数据透视，值为values：统计不同（date，key）情况下values的平均值
# aggfunc=len(或者count)：计数
```

            date key    values
    0 2017-05-01   a  5.886424
    1 2017-05-02   b  9.906472
    2 2017-05-03   c  8.617297
    3 2017-05-01   d  8.972318
    4 2017-05-02   a  7.990905
    5 2017-05-03   b  8.131856
    6 2017-05-01   c  2.823731
    7 2017-05-02   d  2.394605
    8 2017-05-03   a  0.667917
    -----
    key                a         b         c         d
    date                                              
    2017-05-01  5.886424       NaN  2.823731  8.972318
    2017-05-02  7.990905  9.906472       NaN  2.394605
    2017-05-03  0.667917  8.131856  8.617297       NaN
    -----
    date        key
    2017-05-01  a      1.0
                c      1.0
                d      1.0
    2017-05-02  a      1.0
                b      1.0
                d      1.0
    2017-05-03  a      1.0
                b      1.0
                c      1.0
    Name: values, dtype: float64
    -----
    


```python
# 交叉表：crosstab
# 默认情况下，crosstab计算因子的频率表，比如用于str的数据透视分析
# pd.crosstab(index, columns, values=None, rownames=None, colnames=None, aggfunc=None, margins=False, dropna=True, normalize=False)

df = pd.DataFrame({'A': [1, 2, 2, 2, 2],
                   'B': [3, 3, 4, 4, 4],
                   'C': [1, 1, np.nan, 1, 1]})
print(df)
print('-----')

print(pd.crosstab(df['A'],df['B']))
print('-----')
# 如果crosstab只接收两个Series，它将提供一个频率表。
# 用A的唯一值，统计B唯一值的出现次数

print(pd.crosstab(df['A'],df['B'],normalize=True))
print('-----')
# normalize：默认False，将所有值除以值的总和进行归一化 → 为True时候显示百分比

print(pd.crosstab(df['A'],df['B'],values=df['C'],aggfunc=np.sum))
print('-----')
# values：可选，根据因子聚合的值数组
# aggfunc：可选，如果未传递values数组，则计算频率表，如果传递数组，则按照指定计算
# 这里相当于以A和B界定分组，计算出每组中第三个系列C的值

print(pd.crosstab(df['A'],df['B'],values=df['C'],aggfunc=np.sum, margins=True))
print('-----')
# margins：布尔值，默认值False，添加行/列边距（小计）
```

       A  B    C
    0  1  3  1.0
    1  2  3  1.0
    2  2  4  NaN
    3  2  4  1.0
    4  2  4  1.0
    -----
    B  3  4
    A      
    1  1  0
    2  1  3
    -----
    B    3    4
    A          
    1  0.2  0.0
    2  0.2  0.6
    -----
    B    3    4
    A          
    1  1.0  NaN
    2  1.0  2.0
    -----
    B      3    4  All
    A                 
    1    1.0  NaN  1.0
    2    1.0  2.0  3.0
    All  2.0  2.0  4.0
    -----
    

######## 本节课有作业，请查看 “课程作业.docx”  ########


```python
'''
【课程2.22】  数据读取

核心：read_table, read_csv, read_excel
 
'''
```


```python
# 读取普通分隔数据：read_table
# 可以读取txt，csv

import os
os.chdir('C:/Users/Hjx/Desktop/')

data1 = pd.read_table('data1.txt', delimiter=',',header = 0, index_col=1)
print(data1)
# delimiter：用于拆分的字符，也可以用sep：sep = ','
# header：用做列名的序号，默认为0（第一行）
# index_col：指定某列为行索引，否则自动索引0, 1, .....

# read_table主要用于读取简单的数据，txt/csv
```

         va1  va3  va4
    va2               
    2      1    3    4
    3      2    4    5
    4      3    5    6
    5      4    6    7
    


```python
# 读取csv数据：read_csv
# 先熟悉一下excel怎么导出csv

data2 = pd.read_csv('data2.csv',engine = 'python')
print(data2.head())
# engine：使用的分析引擎。可以选择C或者是python。C引擎快但是Python引擎功能更加完备。
# encoding：指定字符集类型，即编码，通常指定为'utf-8'

# 大多数情况先将excel导出csv，再读取
```

       省级政区代码 省级政区名称  地市级政区代码 地市级政区名称    年份 党委书记姓名  出生年份  出生月份  籍贯省份代码 籍贯省份名称  \
    0  130000    河北省   130100    石家庄市  2000    陈来立   NaN   NaN     NaN    NaN   
    1  130000    河北省   130100    石家庄市  2001    吴振华   NaN   NaN     NaN    NaN   
    2  130000    河北省   130100    石家庄市  2002    吴振华   NaN   NaN     NaN    NaN   
    3  130000    河北省   130100    石家庄市  2003    吴振华   NaN   NaN     NaN    NaN   
    4  130000    河北省   130100    石家庄市  2004    吴振华   NaN   NaN     NaN    NaN   
    
       ...    民族  教育 是否是党校教育（是=1，否=0） 专业：人文 专业：社科  专业：理工  专业：农科  专业：医科  入党年份  工作年份  
    0  ...   NaN  硕士              1.0   NaN   NaN    NaN    NaN    NaN   NaN   NaN  
    1  ...   NaN  本科              0.0   0.0   0.0    1.0    0.0    0.0   NaN   NaN  
    2  ...   NaN  本科              0.0   0.0   0.0    1.0    0.0    0.0   NaN   NaN  
    3  ...   NaN  本科              0.0   0.0   0.0    1.0    0.0    0.0   NaN   NaN  
    4  ...   NaN  本科              0.0   0.0   0.0    1.0    0.0    0.0   NaN   NaN  
    
    [5 rows x 23 columns]
    


```python
# 读取excel数据：read_excel

data3 = pd.read_excel('地市级党委书记数据库（2000-10）.xlsx',sheetname='中国人民共和国地市级党委书记数据库（2000-10）',header=0)
print(data3)
# io ：文件路径。
# sheetname：返回多表使用sheetname=[0,1],若sheetname=None是返回全表 → ① int/string 返回的是dataframe ②而none和list返回的是dict
# header：指定列名行，默认0，即取第一行
# index_col：指定列为索引列，也可以使用u”strings”
```

          省级政区代码    省级政区名称  地市级政区代码   地市级政区名称    年份 党委书记姓名  出生年份  出生月份  籍贯省份代码  \
    0     130000       河北省   130100      石家庄市  2000    陈来立   NaN   NaN     NaN   
    1     130000       河北省   130100      石家庄市  2001    吴振华   NaN   NaN     NaN   
    2     130000       河北省   130100      石家庄市  2002    吴振华   NaN   NaN     NaN   
    3     130000       河北省   130100      石家庄市  2003    吴振华   NaN   NaN     NaN   
    4     130000       河北省   130100      石家庄市  2004    吴振华   NaN   NaN     NaN   
    5     130000       河北省   130100      石家庄市  2005    吴振华   NaN   NaN     NaN   
    6     130000       河北省   130100      石家庄市  2006    吴振华   NaN   NaN     NaN   
    7     130000       河北省   130100      石家庄市  2007    吴显国   NaN   NaN     NaN   
    8     130000       河北省   130100      石家庄市  2008    吴显国   NaN   NaN     NaN   
    9     130000       河北省   130100      石家庄市  2009     车俊   NaN   NaN     NaN   
    10    130000       河北省   130100      石家庄市  2010    孙瑞彬   NaN   NaN     NaN   
    11    130000       河北省   130200       唐山市  2000    白润璋   NaN   NaN     NaN   
    12    130000       河北省   130200       唐山市  2001    白润璋   NaN   NaN     NaN   
    13    130000       河北省   130200       唐山市  2002    白润璋   NaN   NaN     NaN   
    14    130000       河北省   130200       唐山市  2003     张和   NaN   NaN     NaN   
    15    130000       河北省   130200       唐山市  2004     张和   NaN   NaN     NaN   
    16    130000       河北省   130200       唐山市  2005     张和   NaN   NaN     NaN   
    17    130000       河北省   130200       唐山市  2006     张和   NaN   NaN     NaN   
    18    130000       河北省   130200       唐山市  2007     赵勇   NaN   NaN     NaN   
    19    130000       河北省   130200       唐山市  2008     赵勇   NaN   NaN     NaN   
    20    130000       河北省   130200       唐山市  2009     赵勇   NaN   NaN     NaN   
    21    130000       河北省   130200       唐山市  2010     赵勇   NaN   NaN     NaN   
    22    130000       河北省   130300      秦皇岛市  2000    王建忠   NaN   NaN     NaN   
    23    130000       河北省   130300      秦皇岛市  2001    王建忠   NaN   NaN     NaN   
    24    130000       河北省   130300      秦皇岛市  2002    王建忠   NaN   NaN     NaN   
    25    130000       河北省   130300      秦皇岛市  2003    宋长瑞   NaN   NaN     NaN   
    26    130000       河北省   130300      秦皇岛市  2004    宋长瑞   NaN   NaN     NaN   
    27    130000       河北省   130300      秦皇岛市  2005    宋长瑞   NaN   NaN     NaN   
    28    130000       河北省   130300      秦皇岛市  2006    宋长瑞   NaN   NaN     NaN   
    29    130000       河北省   130300      秦皇岛市  2007    王三堂   NaN   NaN     NaN   
    ...      ...       ...      ...       ...   ...    ...   ...   ...     ...   
    3633  650000  新疆维吾尔自治区   654000  伊犁哈萨克自治州  2003    NaN   NaN   NaN     NaN   
    3634  650000  新疆维吾尔自治区   654000  伊犁哈萨克自治州  2004    NaN   NaN   NaN     NaN   
    3635  650000  新疆维吾尔自治区   654000  伊犁哈萨克自治州  2005    NaN   NaN   NaN     NaN   
    3636  650000  新疆维吾尔自治区   654000  伊犁哈萨克自治州  2006    NaN   NaN   NaN     NaN   
    3637  650000  新疆维吾尔自治区   654000  伊犁哈萨克自治州  2007    NaN   NaN   NaN     NaN   
    3638  650000  新疆维吾尔自治区   654000  伊犁哈萨克自治州  2008    NaN   NaN   NaN     NaN   
    3639  650000  新疆维吾尔自治区   654000  伊犁哈萨克自治州  2009    NaN   NaN   NaN     NaN   
    3640  650000  新疆维吾尔自治区   654000  伊犁哈萨克自治州  2010    NaN   NaN   NaN     NaN   
    3641  650000  新疆维吾尔自治区   654200      塔城地区  2000    NaN   NaN   NaN     NaN   
    3642  650000  新疆维吾尔自治区   654200      塔城地区  2001    NaN   NaN   NaN     NaN   
    3643  650000  新疆维吾尔自治区   654200      塔城地区  2002    NaN   NaN   NaN     NaN   
    3644  650000  新疆维吾尔自治区   654200      塔城地区  2003    NaN   NaN   NaN     NaN   
    3645  650000  新疆维吾尔自治区   654200      塔城地区  2004    NaN   NaN   NaN     NaN   
    3646  650000  新疆维吾尔自治区   654200      塔城地区  2005    NaN   NaN   NaN     NaN   
    3647  650000  新疆维吾尔自治区   654200      塔城地区  2006    NaN   NaN   NaN     NaN   
    3648  650000  新疆维吾尔自治区   654200      塔城地区  2007    NaN   NaN   NaN     NaN   
    3649  650000  新疆维吾尔自治区   654200      塔城地区  2008    NaN   NaN   NaN     NaN   
    3650  650000  新疆维吾尔自治区   654200      塔城地区  2009    NaN   NaN   NaN     NaN   
    3651  650000  新疆维吾尔自治区   654200      塔城地区  2010    NaN   NaN   NaN     NaN   
    3652  650000  新疆维吾尔自治区   654300     阿勒泰地区  2000    NaN   NaN   NaN     NaN   
    3653  650000  新疆维吾尔自治区   654300     阿勒泰地区  2001    NaN   NaN   NaN     NaN   
    3654  650000  新疆维吾尔自治区   654300     阿勒泰地区  2002    NaN   NaN   NaN     NaN   
    3655  650000  新疆维吾尔自治区   654300     阿勒泰地区  2003    NaN   NaN   NaN     NaN   
    3656  650000  新疆维吾尔自治区   654300     阿勒泰地区  2004    NaN   NaN   NaN     NaN   
    3657  650000  新疆维吾尔自治区   654300     阿勒泰地区  2005    NaN   NaN   NaN     NaN   
    3658  650000  新疆维吾尔自治区   654300     阿勒泰地区  2006    NaN   NaN   NaN     NaN   
    3659  650000  新疆维吾尔自治区   654300     阿勒泰地区  2007    NaN   NaN   NaN     NaN   
    3660  650000  新疆维吾尔自治区   654300     阿勒泰地区  2008    NaN   NaN   NaN     NaN   
    3661  650000  新疆维吾尔自治区   654300     阿勒泰地区  2009    NaN   NaN   NaN     NaN   
    3662  650000  新疆维吾尔自治区   654300     阿勒泰地区  2010    NaN   NaN   NaN     NaN   
    
         籍贯省份名称  ...    民族   教育 是否是党校教育（是=1，否=0） 专业：人文 专业：社科  专业：理工  专业：农科  专业：医科  \
    0       NaN  ...   NaN   硕士              1.0   NaN   NaN    NaN    NaN    NaN   
    1       NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    2       NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    3       NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    4       NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    5       NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    6       NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    7       NaN  ...   NaN   硕士              1.0   0.0   1.0    0.0    0.0    0.0   
    8       NaN  ...   NaN   硕士              1.0   0.0   1.0    0.0    0.0    0.0   
    9       NaN  ...   NaN   本科              1.0   0.0   1.0    0.0    0.0    0.0   
    10      NaN  ...   NaN   硕士              1.0   0.0   1.0    0.0    0.0    0.0   
    11      NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    12      NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    13      NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    14      NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    15      NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    16      NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    17      NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    18      NaN  ...   NaN   博士              0.0   0.0   1.0    0.0    0.0    0.0   
    19      NaN  ...   NaN   博士              0.0   0.0   1.0    0.0    0.0    0.0   
    20      NaN  ...   NaN   博士              0.0   0.0   1.0    0.0    0.0    0.0   
    21      NaN  ...   NaN   博士              0.0   0.0   1.0    0.0    0.0    0.0   
    22      NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    23      NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    24      NaN  ...   NaN   本科              0.0   0.0   0.0    1.0    0.0    0.0   
    25      NaN  ...   NaN   硕士              1.0   0.0   1.0    0.0    0.0    0.0   
    26      NaN  ...   NaN   硕士              1.0   0.0   1.0    0.0    0.0    0.0   
    27      NaN  ...   NaN   硕士              1.0   0.0   1.0    0.0    0.0    0.0   
    28      NaN  ...   NaN   硕士              1.0   0.0   1.0    0.0    0.0    0.0   
    29      NaN  ...   NaN   硕士              1.0   0.0   1.0    0.0    0.0    0.0   
    ...     ...  ...   ...  ...              ...   ...   ...    ...    ...    ...   
    3633    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3634    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3635    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3636    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3637    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3638    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3639    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3640    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3641    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3642    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3643    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3644    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3645    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3646    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3647    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3648    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3649    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3650    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3651    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3652    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3653    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3654    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3655    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3656    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3657    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3658    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3659    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3660    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3661    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    3662    NaN  ...   NaN  NaN              NaN   NaN   NaN    NaN    NaN    NaN   
    
          入党年份  工作年份  
    0      NaN   NaN  
    1      NaN   NaN  
    2      NaN   NaN  
    3      NaN   NaN  
    4      NaN   NaN  
    5      NaN   NaN  
    6      NaN   NaN  
    7      NaN   NaN  
    8      NaN   NaN  
    9      NaN   NaN  
    10     NaN   NaN  
    11     NaN   NaN  
    12     NaN   NaN  
    13     NaN   NaN  
    14     NaN   NaN  
    15     NaN   NaN  
    16     NaN   NaN  
    17     NaN   NaN  
    18     NaN   NaN  
    19     NaN   NaN  
    20     NaN   NaN  
    21     NaN   NaN  
    22     NaN   NaN  
    23     NaN   NaN  
    24     NaN   NaN  
    25     NaN   NaN  
    26     NaN   NaN  
    27     NaN   NaN  
    28     NaN   NaN  
    29     NaN   NaN  
    ...    ...   ...  
    3633   NaN   NaN  
    3634   NaN   NaN  
    3635   NaN   NaN  
    3636   NaN   NaN  
    3637   NaN   NaN  
    3638   NaN   NaN  
    3639   NaN   NaN  
    3640   NaN   NaN  
    3641   NaN   NaN  
    3642   NaN   NaN  
    3643   NaN   NaN  
    3644   NaN   NaN  
    3645   NaN   NaN  
    3646   NaN   NaN  
    3647   NaN   NaN  
    3648   NaN   NaN  
    3649   NaN   NaN  
    3650   NaN   NaN  
    3651   NaN   NaN  
    3652   NaN   NaN  
    3653   NaN   NaN  
    3654   NaN   NaN  
    3655   NaN   NaN  
    3656   NaN   NaN  
    3657   NaN   NaN  
    3658   NaN   NaN  
    3659   NaN   NaN  
    3660   NaN   NaN  
    3661   NaN   NaN  
    3662   NaN   NaN  
    
    [3663 rows x 23 columns]
    
