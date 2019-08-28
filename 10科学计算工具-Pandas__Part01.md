

```python
'''
【课程2.2】  Pandas数据结构Series：基本概念及创建

"一维数组"Serise

'''
```




    '\n【课程2.2】  Pandas数据结构Series：基本概念及创建\n\n"一维数组"Serise\n\n'




```python
# Series 数据结构
# Series 是带有标签的一维数组，可以保存任何数据类型（整数，字符串，浮点数，Python对象等）,轴标签统称为索引

import numpy as np
import pandas as pd  
# 导入numpy、pandas模块

s = pd.Series(np.random.rand(5))
print(s)
print(type(s))
# 查看数据、数据类型

print(s.index,type(s.index))
print(s.values,type(s.values))
# .index查看series索引，类型为rangeindex
# .values查看series值，类型是ndarray

# 核心：series相比于ndarray，是一个自带索引index的数组 → 一维数组 + 对应索引
# 所以当只看series的值的时候，就是一个ndarray
# series和ndarray较相似，索引切片功能差别不大
# series和dict相比，series更像一个有顺序的字典（dict本身不存在顺序），其索引原理与字典相似（一个用key，一个用index）
```

    0    0.273072
    1    0.747787
    2    0.979715
    3    0.697411
    4    0.761611
    dtype: float64
    <class 'pandas.core.series.Series'>
    RangeIndex(start=0, stop=5, step=1) <class 'pandas.core.indexes.range.RangeIndex'>
    [0.27307225 0.74778711 0.97971524 0.6974109  0.76161082] <class 'numpy.ndarray'>
    


```python
# Series 创建方法一：由字典创建，字典的key就是index，values就是values

dic = {'a':1 ,'b':2 , 'c':3, '4':4, '5':5}
s = pd.Series(dic)
print(s)
# 注意：key肯定是字符串，假如values类型不止一个会怎么样？ → dic = {'a':1 ,'b':'hello' , 'c':3, '4':4, '5':5}
```

    a    1
    b    2
    c    3
    4    4
    5    5
    dtype: int64
    


```python
# Series 创建方法二：由数组创建(一维数组)

arr = np.random.randn(5)
s = pd.Series(arr)
print(arr)
print(s)
# 默认index是从0开始，步长为1的数字

s = pd.Series(arr, index = ['a','b','c','d','e'],dtype = np.object)
print(s)
# index参数：设置index，长度保持一致
# dtype参数：设置数值类型
```

    [ 0.11206121  0.1324684   0.59930544  0.34707543 -0.15652941]
    0    0.112061
    1    0.132468
    2    0.599305
    3    0.347075
    4   -0.156529
    dtype: float64
    a    0.112061
    b    0.132468
    c    0.599305
    d    0.347075
    e   -0.156529
    dtype: object
    


```python
# Series 创建方法三：由标量创建

s = pd.Series(10, index = range(4))
s = pd.Series()
print(s)
# 如果data是标量值，则必须提供索引。该值会重复，来匹配索引的长度
```

    0    10
    1    10
    2    10
    3    10
    dtype: int64
    


```python
# Series 名称属性：name

s1 = pd.Series(np.random.randn(5))
print(s1)
print('-----')
s2 = pd.Series(np.random.randn(5),name = 'test')
print(s2)
print(s1.name, s2.name,type(s2.name))
# name为Series的一个参数，创建一个数组的 名称
# .name方法：输出数组的名称，输出格式为str，如果没用定义输出名称，输出为None

s3 = s2.rename('hehehe')
print(s3)
print(s3.name, s2.name)
# .rename()重命名一个数组的名称，并且新指向一个数组，原数组不变
```

    0   -0.403084
    1    1.369383
    2    1.134319
    3   -0.635050
    4    1.680211
    dtype: float64
    -----
    0   -0.120014
    1    1.967648
    2    1.142626
    3    0.234079
    4    0.761357
    Name: test, dtype: float64
    None test <class 'str'>
    0   -0.120014
    1    1.967648
    2    1.142626
    3    0.234079
    4    0.761357
    Name: hehehe, dtype: float64
    hehehe test
    


```python
'''
【课程2.3】  Pandas数据结构Series：索引

位置下标 / 标签索引 / 切片索引 / 布尔型索引

'''
```


```python
# 位置下标，类似序列

s = pd.Series(np.random.rand(5))
print(s)
print(s[0],type(s[0]),s[0].dtype)
print(float(s[0]),type(float(s[0])))
#print(s[-1])
# 位置下标从0开始
# 输出结果为numpy.float格式，
# 可以通过float()函数转换为python float格式
# numpy.float与float占用字节不同
# s[-1]结果如何？
```

    0    0.924575
    1    0.988654
    2    0.426333
    3    0.216504
    4    0.453570
    dtype: float64
    0.924575004833 <class 'numpy.float64'> float64
    0.9245750048328816 <class 'float'>
    


```python
# 标签索引

s = pd.Series(np.random.rand(5), index = ['a','b','c','d','e'])
print(s)
print(s['a'],type(s['a']),s['a'].dtype)
# 方法类似下标索引，用[]表示，内写上index，注意index是字符串

sci = s[['b','a','e']]
print(sci,type(sci))
# 如果需要选择多个标签的值，用[[]]来表示（相当于[]中包含一个列表）
# 多标签索引结果是新的数组
```

    a    0.891103
    b    0.478374
    c    0.344993
    d    0.949257
    e    0.321771
    dtype: float64
    0.8911028081180662 <class 'numpy.float64'> float64
    b    0.478374
    a    0.891103
    e    0.321771
    dtype: float64 <class 'pandas.core.series.Series'>
    


```python
# 切片索引

s1 = pd.Series(np.random.rand(5))
s2 = pd.Series(np.random.rand(5), index = ['a','b','c','d','e'])
print(s1[1:4],s1[4])
print(s2['a':'c'],s2['c'])
print(s2[0:3],s2[3])
print('-----')
# 注意：用index做切片是末端包含

print(s2[:-1])
print(s2[::2])  # 步进
# 下标索引做切片，和list写法一样
```

    1    0.209102
    2    0.217480
    3    0.544522
    dtype: float64 0.6472536119996961
    a    0.195037
    b    0.360075
    c    0.261531
    dtype: float64 0.26153129067273595
    a    0.195037
    b    0.360075
    c    0.261531
    dtype: float64 0.8622643195595027
    -----
    a    0.195037
    b    0.360075
    c    0.261531
    d    0.862264
    dtype: float64
    a    0.195037
    c    0.261531
    e    0.302644
    dtype: float64
    


```python
# 布尔型索引

s = pd.Series(np.random.rand(3)*100)
s[4] = None  # 添加一个空值
print(s)
bs1 = s > 50
bs2 = s.isnull()
bs3 = s.notnull()
print(bs1, type(bs1), bs1.dtype)
print(bs2, type(bs2), bs2.dtype)
print(bs3, type(bs3), bs3.dtype)
print('-----')
# 数组做判断之后，返回的是一个由布尔值组成的新的数组
# .isnull() / .notnull() 判断是否为空值 (None代表空值，NaN代表有问题的数值，两个都会识别为空值)

print(s[s > 50])
print(s[bs3])
# 布尔型索引方法：用[判断条件]表示，其中判断条件可以是 一个语句，或者是 一个布尔型数组！
```

    0    2.03802
    1    40.3989
    2    25.2001
    4       None
    dtype: object
    0    False
    1    False
    2    False
    4    False
    dtype: bool <class 'pandas.core.series.Series'> bool
    0    False
    1    False
    2    False
    4     True
    dtype: bool <class 'pandas.core.series.Series'> bool
    0     True
    1     True
    2     True
    4    False
    dtype: bool <class 'pandas.core.series.Series'> bool
    -----
    Series([], dtype: object)
    0    2.03802
    1    40.3989
    2    25.2001
    dtype: object
    


```python
'''
【课程2.4】  Pandas数据结构Series：基本技巧

数据查看 / 重新索引 / 对齐 / 添加、修改、删除值

'''
```


```python
# 数据查看

s = pd.Series(np.random.rand(50))
print(s.head(10))
print(s.tail())
# .head()查看头部数据
# .tail()查看尾部数据
# 默认查看5条
```

    0    0.730540
    1    0.116711
    2    0.787693
    3    0.969764
    4    0.324540
    5    0.061827
    6    0.377060
    7    0.820383
    8    0.964477
    9    0.451936
    dtype: float64
    45    0.899540
    46    0.237008
    47    0.298762
    48    0.848487
    49    0.829858
    dtype: float64
    


```python
# 重新索引reindex
# .reindex将会根据索引重新排序，如果当前索引不存在，则引入缺失值

s = pd.Series(np.random.rand(3), index = ['a','b','c'])
print(s)
s1 = s.reindex(['c','b','a','d'])
print(s1)
# .reindex()中也是写列表
# 这里'd'索引不存在，所以值为NaN

s2 = s.reindex(['c','b','a','d'], fill_value = 0)
print(s2)
# fill_value参数：填充缺失值的值
```

    a    0.343718
    b    0.322228
    c    0.746720
    dtype: float64
    c    0.746720
    b    0.322228
    a    0.343718
    d         NaN
    dtype: float64
    c    0.746720
    b    0.322228
    a    0.343718
    d    0.000000
    dtype: float64
    


```python
# Series对齐

s1 = pd.Series(np.random.rand(3), index = ['Jack','Marry','Tom'])
s2 = pd.Series(np.random.rand(3), index = ['Wang','Jack','Marry'])
print(s1)
print(s2)
print(s1+s2)
# Series 和 ndarray 之间的主要区别是，Series 上的操作会根据标签自动对齐
# index顺序不会影响数值计算，以标签来计算
# 空值和任何值计算结果扔为空值
```

    Jack     0.753732
    Marry    0.180223
    Tom      0.283704
    dtype: float64
    Wang     0.309128
    Jack     0.533997
    Marry    0.626126
    dtype: float64
    Jack     1.287729
    Marry    0.806349
    Tom           NaN
    Wang          NaN
    dtype: float64
    


```python
# 删除：.drop

s = pd.Series(np.random.rand(5), index = list('ngjur'))
print(s)
s1 = s.drop('n')
s2 = s.drop(['g','j'])
print(s1)
print(s2)
print(s)
# drop 删除元素之后返回副本(inplace=False)
```

    n    0.876587
    g    0.594053
    j    0.628232
    u    0.360634
    r    0.454483
    dtype: float64
    g    0.594053
    j    0.628232
    u    0.360634
    r    0.454483
    dtype: float64
    n    0.876587
    u    0.360634
    r    0.454483
    dtype: float64
    n    0.876587
    g    0.594053
    j    0.628232
    u    0.360634
    r    0.454483
    dtype: float64
    


```python
# 添加

s1 = pd.Series(np.random.rand(5))
s2 = pd.Series(np.random.rand(5), index = list('ngjur'))
print(s1)
print(s2)
s1[5] = 100
s2['a'] = 100
print(s1)
print(s2)
print('-----')
# 直接通过下标索引/标签index添加值

s3 = s1.append(s2)
print(s3)
print(s1)
# 通过.append方法，直接添加一个数组
# .append方法生成一个新的数组，不改变之前的数组
```

    0    0.516447
    1    0.699382
    2    0.469513
    3    0.589821
    4    0.402188
    dtype: float64
    n    0.615641
    g    0.451192
    j    0.022328
    u    0.977568
    r    0.902041
    dtype: float64
    0      0.516447
    1      0.699382
    2      0.469513
    3      0.589821
    4      0.402188
    5    100.000000
    dtype: float64
    n      0.615641
    g      0.451192
    j      0.022328
    u      0.977568
    r      0.902041
    a    100.000000
    dtype: float64
    -----
    0      0.516447
    1      0.699382
    2      0.469513
    3      0.589821
    4      0.402188
    5    100.000000
    n      0.615641
    g      0.451192
    j      0.022328
    u      0.977568
    r      0.902041
    a    100.000000
    dtype: float64
    0      0.516447
    1      0.699382
    2      0.469513
    3      0.589821
    4      0.402188
    5    100.000000
    dtype: float64
    


```python
# 修改

s = pd.Series(np.random.rand(3), index = ['a','b','c'])
print(s)
s['a'] = 100
s[['b','c']] = 200
print(s)
# 通过索引直接修改，类似序列
```

    a    0.873604
    b    0.244707
    c    0.888685
    dtype: float64
    a    100.0
    b    200.0
    c    200.0
    dtype: float64
    


```python
'''
【课程2.5】  Pandas数据结构Dataframe：基本概念及创建

"二维数组"Dataframe：是一个表格型的数据结构，包含一组有序的列，其列的值类型可以是数值、字符串、布尔值等。

Dataframe中的数据以一个或多个二维块存放，不是列表、字典或一维数组结构。

'''
```


```python
# Dataframe 数据结构
# Dataframe是一个表格型的数据结构，“带有标签的二维数组”。
# Dataframe带有index（行标签）和columns（列标签）

data = {'name':['Jack','Tom','Mary'],
        'age':[18,19,20],
       'gender':['m','m','w']}
frame = pd.DataFrame(data)
print(frame)  
print(type(frame))
print(frame.index,'\n该数据类型为：',type(frame.index))
print(frame.columns,'\n该数据类型为：',type(frame.columns))
print(frame.values,'\n该数据类型为：',type(frame.values))
# 查看数据，数据类型为dataframe
# .index查看行标签
# .columns查看列标签
# .values查看值，数据类型为ndarray
```

       age gender  name
    0   18      m  Jack
    1   19      m   Tom
    2   20      w  Mary
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex(start=0, stop=3, step=1) 
    该数据类型为： <class 'pandas.indexes.range.RangeIndex'>
    Index(['age', 'gender', 'name'], dtype='object') 
    该数据类型为： <class 'pandas.indexes.base.Index'>
    [[18 'm' 'Jack']
     [19 'm' 'Tom']
     [20 'w' 'Mary']] 
    该数据类型为： <class 'numpy.ndarray'>
    


```python
# Dataframe 创建方法一：由数组/list组成的字典
# 创建方法:pandas.Dataframe()

data1 = {'a':[1,2,3],
        'b':[3,4,5],
        'c':[5,6,7]}
data2 = {'one':np.random.rand(3),
        'two':np.random.rand(3)}   # 这里如果尝试  'two':np.random.rand(4) 会怎么样？
print(data1)
print(data2)
df1 = pd.DataFrame(data1)
df2 = pd.DataFrame(data2)
print(df1)
print(df2)
# 由数组/list组成的字典 创建Dataframe，columns为字典key，index为默认数字标签
# 字典的值的长度必须保持一致！

df1 = pd.DataFrame(data1, columns = ['b','c','a','d'])
print(df1)
df1 = pd.DataFrame(data1, columns = ['b','c'])
print(df1)
# columns参数：可以重新指定列的顺序，格式为list，如果现有数据中没有该列（比如'd'），则产生NaN值
# 如果columns重新指定时候，列的数量可以少于原数据

df2 = pd.DataFrame(data2, index = ['f1','f2','f3'])  # 这里如果尝试  index = ['f1','f2','f3','f4'] 会怎么样？
print(df2)
# index参数：重新定义index，格式为list，长度必须保持一致
```

    {'a': [1, 2, 3], 'c': [5, 6, 7], 'b': [3, 4, 5]}
    {'one': array([ 0.00101091,  0.08807153,  0.58345056]), 'two': array([ 0.49774634,  0.16782565,  0.76443489])}
       a  b  c
    0  1  3  5
    1  2  4  6
    2  3  5  7
            one       two
    0  0.001011  0.497746
    1  0.088072  0.167826
    2  0.583451  0.764435
       b  c  a    d
    0  3  5  1  NaN
    1  4  6  2  NaN
    2  5  7  3  NaN
       b  c
    0  3  5
    1  4  6
    2  5  7
             one       two
    f1  0.001011  0.497746
    f2  0.088072  0.167826
    f3  0.583451  0.764435
    


```python
# Dataframe 创建方法二：由Series组成的字典

data1 = {'one':pd.Series(np.random.rand(2)),
        'two':pd.Series(np.random.rand(3))}  # 没有设置index的Series
data2 = {'one':pd.Series(np.random.rand(2), index = ['a','b']),
        'two':pd.Series(np.random.rand(3),index = ['a','b','c'])}  # 设置了index的Series
print(data1)
print(data2)
df1 = pd.DataFrame(data1)
df2 = pd.DataFrame(data2)
print(df1)
print(df2)
# 由Seris组成的字典 创建Dataframe，columns为字典key，index为Series的标签（如果Series没有指定标签，则是默认数字标签）
# Series可以长度不一样，生成的Dataframe会出现NaN值
```

    {'one': 0    0.892580
    1    0.834076
    dtype: float64, 'two': 0    0.301309
    1    0.977709
    2    0.489000
    dtype: float64}
    {'one': a    0.470947
    b    0.584577
    dtype: float64, 'two': a    0.122659
    b    0.136429
    c    0.396825
    dtype: float64}
            one       two
    0  0.892580  0.301309
    1  0.834076  0.977709
    2       NaN  0.489000
            one       two
    a  0.470947  0.122659
    b  0.584577  0.136429
    c       NaN  0.396825
    


```python
# Dataframe 创建方法三：通过二维数组直接创建

ar = np.random.rand(9).reshape(3,3)
print(ar)
df1 = pd.DataFrame(ar)
df2 = pd.DataFrame(ar, index = ['a', 'b', 'c'], columns = ['one','two','three'])  # 可以尝试一下index或columns长度不等于已有数组的情况
print(df1)
print(df2)
# 通过二维数组直接创建Dataframe，得到一样形状的结果数据，如果不指定index和columns，两者均返回默认数字格式
# index和colunms指定长度与原数组保持一致
```

    [[ 0.54492282  0.28956161  0.46592269]
     [ 0.30480674  0.12917132  0.38757672]
     [ 0.2518185   0.13544544  0.13930429]]
              0         1         2
    0  0.544923  0.289562  0.465923
    1  0.304807  0.129171  0.387577
    2  0.251819  0.135445  0.139304
            one       two     three
    a  0.544923  0.289562  0.465923
    b  0.304807  0.129171  0.387577
    c  0.251819  0.135445  0.139304
    


```python
# Dataframe 创建方法四：由字典组成的列表

data = [{'one': 1, 'two': 2}, {'one': 5, 'two': 10, 'three': 20}]
print(data)
df1 = pd.DataFrame(data)
df2 = pd.DataFrame(data, index = ['a','b'])
df3 = pd.DataFrame(data, columns = ['one','two'])
print(df1)
print(df2)
print(df3)
# 由字典组成的列表创建Dataframe，columns为字典的key，index不做指定则为默认数组标签
# colunms和index参数分别重新指定相应列及行标签
```

    [{'one': 1, 'two': 2}, {'one': 5, 'three': 20, 'two': 10}]
       one  three  two
    0    1    NaN    2
    1    5   20.0   10
       one  three  two
    a    1    NaN    2
    b    5   20.0   10
       one  two
    0    1    2
    1    5   10
    


```python
# Dataframe 创建方法五：由字典组成的字典

data = {'Jack':{'math':90,'english':89,'art':78},
       'Marry':{'math':82,'english':95,'art':92},
       'Tom':{'math':78,'english':67}}
df1 = pd.DataFrame(data)
print(df1)
# 由字典组成的字典创建Dataframe，columns为字典的key，index为子字典的key

df2 = pd.DataFrame(data, columns = ['Jack','Tom','Bob'])
df3 = pd.DataFrame(data, index = ['a','b','c'])
print(df2)
print(df3)
# columns参数可以增加和减少现有列，如出现新的列，值为NaN
# index在这里和之前不同，并不能改变原有index，如果指向新的标签，值为NaN （非常重要！）
```

             Jack  Marry   Tom
    art        78     92   NaN
    english    89     95  67.0
    math       90     82  78.0
             Jack   Tom  Bob
    art        78   NaN  NaN
    english    89  67.0  NaN
    math       90  78.0  NaN
       Jack  Marry  Tom
    a   NaN    NaN  NaN
    b   NaN    NaN  NaN
    c   NaN    NaN  NaN
    


```python
'''
【课程2.6】  Pandas数据结构Dataframe：索引

Dataframe既有行索引也有列索引，可以被看做由Series组成的字典（共用一个索引）

选择列 / 选择行 / 切片 / 布尔判断

'''
```


```python
# 选择行与列

df = pd.DataFrame(np.random.rand(12).reshape(3,4)*100,
                   index = ['one','two','three'],
                   columns = ['a','b','c','d'])
print(df)

data1 = df['a']
data2 = df[['a','c']]
print(data1,type(data1))
print(data2,type(data2))
print('-----')
# 按照列名选择列，只选择一列输出Series，选择多列输出Dataframe

data3 = df.loc['one']
data4 = df.loc[['one','two']]
print(data3,type(data3))
print(data4,type(data4))
# 按照index选择行，只选择一行输出Series，选择多行输出Dataframe
```

                   a          b          c          d
    one    43.579528  99.163486  58.494452   5.669287
    two    69.610557  28.983281  84.545821  69.265340
    three  85.186545  77.176972  42.879501  99.398105
    one      43.579528
    two      69.610557
    three    85.186545
    Name: a, dtype: float64 <class 'pandas.core.series.Series'>
                   a          c
    one    43.579528  58.494452
    two    69.610557  84.545821
    three  85.186545  42.879501 <class 'pandas.core.frame.DataFrame'>
    -----
    a    43.579528
    b    99.163486
    c    58.494452
    d     5.669287
    Name: one, dtype: float64 <class 'pandas.core.series.Series'>
                 a          b          c          d
    one  43.579528  99.163486  58.494452   5.669287
    two  69.610557  28.983281  84.545821  69.265340 <class 'pandas.core.frame.DataFrame'>
    


```python
# df[] - 选择列
# 一般用于选择列，也可以选择行

df = pd.DataFrame(np.random.rand(12).reshape(3,4)*100,
                   index = ['one','two','three'],
                   columns = ['a','b','c','d'])
print(df)
print('-----')

data1 = df['a']
data2 = df[['b','c']]  # 尝试输入 data2 = df[['b','c','e']]
print(data1)
print(data2)
# df[]默认选择列，[]中写列名（所以一般数据colunms都会单独制定，不会用默认数字列名，以免和index冲突）
# 单选列为Series，print结果为Series格式
# 多选列为Dataframe，print结果为Dataframe格式

data3 = df[:1]
#data3 = df[0]
#data3 = df['one']
print(data3,type(data3))
# df[]中为数字时，默认选择行，且只能进行切片的选择，不能单独选择（df[0]）
# 输出结果为Dataframe，即便只选择一行
# df[]不能通过索引标签名来选择行(df['one'])

# 核心笔记：df[col]一般用于选择列，[]中写列名
```

                   a          b          c          d
    one    88.490183  93.588825   1.605172  74.610087
    two    45.905361  49.257001  87.852426  97.490521
    three  95.801001  97.991028  74.451954  64.290587
    -----
    one      88.490183
    two      45.905361
    three    95.801001
    Name: a, dtype: float64
                   b          c
    one    93.588825   1.605172
    two    49.257001  87.852426
    three  97.991028  74.451954
                 a          b         c          d
    one  88.490183  93.588825  1.605172  74.610087 <class 'pandas.core.frame.DataFrame'>
    


```python
# df.loc[] - 按index选择行

df1 = pd.DataFrame(np.random.rand(16).reshape(4,4)*100,
                   index = ['one','two','three','four'],
                   columns = ['a','b','c','d'])
df2 = pd.DataFrame(np.random.rand(16).reshape(4,4)*100,
                   columns = ['a','b','c','d'])
print(df1)
print(df2)
print('-----')

data1 = df1.loc['one']
data2 = df2.loc[1]
print(data1)
print(data2)
print('单标签索引\n-----')
# 单个标签索引，返回Series

data3 = df1.loc[['two','three','five']]
data4 = df2.loc[[3,2,1]]
print(data3)
print(data4)
print('多标签索引\n-----')
# 多个标签索引，如果标签不存在，则返回NaN
# 顺序可变

data5 = df1.loc['one':'three']
data6 = df2.loc[1:3]
print(data5)
print(data6)
print('切片索引')
# 可以做切片对象
# 末端包含

# 核心笔记：df.loc[label]主要针对index选择行，同时支持指定index，及默认数字index
```

                   a          b          c          d
    one    73.070679   7.169884  80.820532  62.299367
    two    34.025462  77.849955  96.160170  55.159017
    three  27.897582  39.595687  69.280955  49.477429
    four   76.723039  44.995970  22.408450  23.273089
               a          b          c          d
    0  93.871055  28.031989  57.093181  34.695293
    1  22.882809  47.499852  86.466393  86.140909
    2  80.840336  98.120735  84.495414   8.413039
    3  59.695834   1.478707  15.069485  48.775008
    -----
    a    73.070679
    b     7.169884
    c    80.820532
    d    62.299367
    Name: one, dtype: float64
    a    22.882809
    b    47.499852
    c    86.466393
    d    86.140909
    Name: 1, dtype: float64
    单标签索引
    -----
                   a          b          c          d
    two    34.025462  77.849955  96.160170  55.159017
    three  27.897582  39.595687  69.280955  49.477429
    five         NaN        NaN        NaN        NaN
               a          b          c          d
    3  59.695834   1.478707  15.069485  48.775008
    2  80.840336  98.120735  84.495414   8.413039
    1  22.882809  47.499852  86.466393  86.140909
    多标签索引
    -----
                   a          b          c          d
    one    73.070679   7.169884  80.820532  62.299367
    two    34.025462  77.849955  96.160170  55.159017
    three  27.897582  39.595687  69.280955  49.477429
               a          b          c          d
    1  22.882809  47.499852  86.466393  86.140909
    2  80.840336  98.120735  84.495414   8.413039
    3  59.695834   1.478707  15.069485  48.775008
    切片索引
    


```python
# df.iloc[] - 按照整数位置（从轴的0到length-1）选择行
# 类似list的索引，其顺序就是dataframe的整数位置，从0开始计

df = pd.DataFrame(np.random.rand(16).reshape(4,4)*100,
                   index = ['one','two','three','four'],
                   columns = ['a','b','c','d'])
print(df)
print('------')

print(df.iloc[0])
print(df.iloc[-1])
#print(df.iloc[4])
print('单位置索引\n-----')
# 单位置索引
# 和loc索引不同，不能索引超出数据行数的整数位置

print(df.iloc[[0,2]])
print(df.iloc[[3,2,1]])
print('多位置索引\n-----')
# 多位置索引
# 顺序可变

print(df.iloc[1:3])
print(df.iloc[::2])
print('切片索引')
# 切片索引
# 末端不包含
```

                   a          b          c          d
    one    21.848926   2.482328  17.338355  73.014166
    two    99.092794   0.601173  18.598736  61.166478
    three  87.183015  85.973426  48.839267  99.930097
    four   75.007726  84.208576  69.445779  75.546038
    ------
    a    21.848926
    b     2.482328
    c    17.338355
    d    73.014166
    Name: one, dtype: float64
    a    75.007726
    b    84.208576
    c    69.445779
    d    75.546038
    Name: four, dtype: float64
    单位置索引
    -----
                   a          b          c          d
    one    21.848926   2.482328  17.338355  73.014166
    three  87.183015  85.973426  48.839267  99.930097
                   a          b          c          d
    four   75.007726  84.208576  69.445779  75.546038
    three  87.183015  85.973426  48.839267  99.930097
    two    99.092794   0.601173  18.598736  61.166478
    多位置索引
    -----
                   a          b          c          d
    two    99.092794   0.601173  18.598736  61.166478
    three  87.183015  85.973426  48.839267  99.930097
                   a          b          c          d
    one    21.848926   2.482328  17.338355  73.014166
    three  87.183015  85.973426  48.839267  99.930097
    切片索引
    


```python
# 布尔型索引
# 和Series原理相同

df = pd.DataFrame(np.random.rand(16).reshape(4,4)*100,
                   index = ['one','two','three','four'],
                   columns = ['a','b','c','d'])
print(df)
print('------')

b1 = df < 20
print(b1,type(b1))
print(df[b1])  # 也可以书写为 df[df < 20]
print('------')
# 不做索引则会对数据每个值进行判断
# 索引结果保留 所有数据：True返回原数据，False返回值为NaN

b2 = df['a'] > 50
print(b2,type(b2))
print(df[b2])  # 也可以书写为 df[df['a'] > 50]
print('------')
# 单列做判断
# 索引结果保留 单列 判断为True的行数据，包括其他列

b3 = df[['a','b']] > 50
print(b3,type(b3))
print(df[b3])  # 也可以书写为 df[df[['a','b']] > 50]
print('------')
# 多列做判断
# 索引结果保留 所有数据：True返回原数据，False返回值为NaN

b4 = df.loc[['one','three']] < 50
print(b4,type(b4))
print(df[b4])  # 也可以书写为 df[df.loc[['one','three']] < 50]
print('------')
# 多行做判断
# 索引结果保留 所有数据：True返回原数据，False返回值为NaN
```

                   a          b          c          d
    one    19.185849  20.303217  21.800384  45.189534
    two    50.105112  28.478878  93.669529  90.029489
    three  35.496053  19.248457  74.811841  20.711431
    four   24.604478  57.731456  49.682717  82.132866
    ------
               a      b      c      d
    one     True  False  False  False
    two    False  False  False  False
    three  False   True  False  False
    four   False  False  False  False <class 'pandas.core.frame.DataFrame'>
                   a          b   c   d
    one    19.185849        NaN NaN NaN
    two          NaN        NaN NaN NaN
    three        NaN  19.248457 NaN NaN
    four         NaN        NaN NaN NaN
    ------
    one      False
    two       True
    three    False
    four     False
    Name: a, dtype: bool <class 'pandas.core.series.Series'>
                 a          b          c          d
    two  50.105112  28.478878  93.669529  90.029489
    ------
               a      b
    one    False  False
    two     True  False
    three  False  False
    four   False   True <class 'pandas.core.frame.DataFrame'>
                   a          b   c   d
    one          NaN        NaN NaN NaN
    two    50.105112        NaN NaN NaN
    three        NaN        NaN NaN NaN
    four         NaN  57.731456 NaN NaN
    ------
              a     b      c     d
    one    True  True   True  True
    three  True  True  False  True <class 'pandas.core.frame.DataFrame'>
                   a          b          c          d
    one    19.185849  20.303217  21.800384  45.189534
    two          NaN        NaN        NaN        NaN
    three  35.496053  19.248457        NaN  20.711431
    four         NaN        NaN        NaN        NaN
    ------
    


```python
# 多重索引：比如同时索引行和列
# 先选择列再选择行 —— 相当于对于一个数据，先筛选字段，再选择数据量

df = pd.DataFrame(np.random.rand(16).reshape(4,4)*100,
                   index = ['one','two','three','four'],
                   columns = ['a','b','c','d'])
print(df)
print('------')

print(df['a'].loc[['one','three']])   # 选择a列的one，three行
print(df[['b','c','d']].iloc[::2])   # 选择b，c，d列的one，three行
print(df[df['a'] < 50].iloc[:2])   # 选择满足判断索引的前两行数据
```

                   a          b          c          d
    one    50.660904  89.827374  51.096827   3.844736
    two    70.699721  78.750014  52.988276  48.833037
    three  33.653032  27.225202  24.864712  29.662736
    four   21.792339  26.450939   6.122134  52.323963
    ------
    one      50.660904
    three    33.653032
    Name: a, dtype: float64
                   b          c          d
    one    89.827374  51.096827   3.844736
    three  27.225202  24.864712  29.662736
                   a          b          c          d
    three  33.653032  27.225202  24.864712  29.662736
    four   21.792339  26.450939   6.122134  52.323963
    


```python
'''
【课程2.7】  Pandas数据结构Dataframe：基本技巧

数据查看、转置 / 添加、修改、删除值 / 对齐 / 排序

'''
```


```python
# 数据查看、转置

df = pd.DataFrame(np.random.rand(16).reshape(8,2)*100,
                   columns = ['a','b'])
print(df.head(2))
print(df.tail())
# .head()查看头部数据
# .tail()查看尾部数据
# 默认查看5条

print(df.T)
# .T 转置
```

               a          b
    0   5.777208  18.374283
    1  85.961515  55.120036
               a          b
    3  21.236577  15.902872
    4  46.137564  29.350647
    5  70.157709  58.972728
    6   8.368292  42.011356
    7  29.824574  87.062295
               0          1          2          3          4          5  \
    a   5.777208  85.961515  11.005284  21.236577  46.137564  70.157709   
    b  18.374283  55.120036  35.595598  15.902872  29.350647  58.972728   
    
               6          7  
    a   8.368292  29.824574  
    b  42.011356  87.062295  
    


```python
# 添加与修改

df = pd.DataFrame(np.random.rand(16).reshape(4,4)*100,
                   columns = ['a','b','c','d'])
print(df)

df['e'] = 10
df.loc[4] = 20
print(df)
# 新增列/行并赋值

df['e'] = 20
df[['a','c']] = 100
print(df)
# 索引后直接修改值
```

               a          b          c          d
    0  17.148791  73.833921  39.069417   5.675815
    1  91.572695  66.851601  60.320698  92.071097
    2  79.377105  24.314520  44.406357  57.313429
    3  84.599206  61.310945   3.916679  30.076458
               a          b          c          d   e
    0  17.148791  73.833921  39.069417   5.675815  10
    1  91.572695  66.851601  60.320698  92.071097  10
    2  79.377105  24.314520  44.406357  57.313429  10
    3  84.599206  61.310945   3.916679  30.076458  10
    4  20.000000  20.000000  20.000000  20.000000  20
         a          b    c          d   e
    0  100  73.833921  100   5.675815  20
    1  100  66.851601  100  92.071097  20
    2  100  24.314520  100  57.313429  20
    3  100  61.310945  100  30.076458  20
    4  100  20.000000  100  20.000000  20
    


```python
# 删除  del / drop()

df = pd.DataFrame(np.random.rand(16).reshape(4,4)*100,
                   columns = ['a','b','c','d'])
print(df)

del df['a']
print(df)
print('-----')
# del语句 - 删除列

print(df.drop(0))
print(df.drop([1,2]))
print(df)
print('-----')
# drop()删除行，inplace=False → 删除后生成新的数据，不改变原数据

print(df.drop(['d'], axis = 1))
print(df)
# drop()删除列，需要加上axis = 1，inplace=False → 删除后生成新的数据，不改变原数据
```

               a          b          c          d
    0  91.866806  88.753655  18.469852  71.651277
    1  64.835568  33.844967   6.391246  54.916094
    2  75.930985  19.169862  91.042457  43.648258
    3  15.863853  24.788866  10.625684  82.135316
               b          c          d
    0  88.753655  18.469852  71.651277
    1  33.844967   6.391246  54.916094
    2  19.169862  91.042457  43.648258
    3  24.788866  10.625684  82.135316
    -----
               b          c          d
    1  33.844967   6.391246  54.916094
    2  19.169862  91.042457  43.648258
    3  24.788866  10.625684  82.135316
               b          c          d
    0  88.753655  18.469852  71.651277
    3  24.788866  10.625684  82.135316
               b          c          d
    0  88.753655  18.469852  71.651277
    1  33.844967   6.391246  54.916094
    2  19.169862  91.042457  43.648258
    3  24.788866  10.625684  82.135316
    -----
               b          c
    0  88.753655  18.469852
    1  33.844967   6.391246
    2  19.169862  91.042457
    3  24.788866  10.625684
               b          c          d
    0  88.753655  18.469852  71.651277
    1  33.844967   6.391246  54.916094
    2  19.169862  91.042457  43.648258
    3  24.788866  10.625684  82.135316
    


```python
# 对齐

df1 = pd.DataFrame(np.random.randn(10, 4), columns=['A', 'B', 'C', 'D'])
df2 = pd.DataFrame(np.random.randn(7, 3), columns=['A', 'B', 'C'])
print(df1 + df2)
# DataFrame对象之间的数据自动按照列和索引（行标签）对齐
```

              A         B         C   D
    0 -0.281123 -2.529461  1.325663 NaN
    1 -0.310514 -0.408225 -0.760986 NaN
    2 -0.172169 -2.355042  1.521342 NaN
    3  1.113505  0.325933  3.689586 NaN
    4  0.107513 -0.503907 -1.010349 NaN
    5 -0.845676 -2.410537 -1.406071 NaN
    6  1.682854 -0.576620 -0.981622 NaN
    7       NaN       NaN       NaN NaN
    8       NaN       NaN       NaN NaN
    9       NaN       NaN       NaN NaN
    


```python
# 排序1 - 按值排序 .sort_values
# 同样适用于Series

df1 = pd.DataFrame(np.random.rand(16).reshape(4,4)*100,
                   columns = ['a','b','c','d'])
print(df1)
print(df1.sort_values(['a'], ascending = True))  # 升序
print(df1.sort_values(['a'], ascending = False))  # 降序
print('------')
# ascending参数：设置升序降序，默认升序
# 单列排序

df2 = pd.DataFrame({'a':[1,1,1,1,2,2,2,2],
                  'b':list(range(8)),
                  'c':list(range(8,0,-1))})
print(df2)
print(df2.sort_values(['a','c']))
# 多列排序，按列顺序排序
```

               a          b          c          d
    0  16.519099  19.601879  35.464189  58.866972
    1  34.506472  97.106578  96.308244  54.049359
    2  87.177828  47.253416  92.098847  19.672678
    3  66.673226  51.969534  71.789055  14.504191
               a          b          c          d
    0  16.519099  19.601879  35.464189  58.866972
    1  34.506472  97.106578  96.308244  54.049359
    3  66.673226  51.969534  71.789055  14.504191
    2  87.177828  47.253416  92.098847  19.672678
               a          b          c          d
    2  87.177828  47.253416  92.098847  19.672678
    3  66.673226  51.969534  71.789055  14.504191
    1  34.506472  97.106578  96.308244  54.049359
    0  16.519099  19.601879  35.464189  58.866972
    ------
       a  b  c
    0  1  0  8
    1  1  1  7
    2  1  2  6
    3  1  3  5
    4  2  4  4
    5  2  5  3
    6  2  6  2
    7  2  7  1
       a  b  c
    3  1  3  5
    2  1  2  6
    1  1  1  7
    0  1  0  8
    7  2  7  1
    6  2  6  2
    5  2  5  3
    4  2  4  4
    


```python
# 排序2 - 索引排序 .sort_index

df1 = pd.DataFrame(np.random.rand(16).reshape(4,4)*100,
                  index = [5,4,3,2],
                   columns = ['a','b','c','d'])
df2 = pd.DataFrame(np.random.rand(16).reshape(4,4)*100,
                  index = ['h','s','x','g'],
                   columns = ['a','b','c','d'])
print(df1)
print(df1.sort_index())
print(df2)
print(df2.sort_index())
# 按照index排序
# 默认 ascending=True, inplace=False
```

               a          b          c          d
    5  57.327269  87.623119  93.655538   5.859571
    4  69.739134  80.084366  89.005538  56.825475
    3  88.148296   6.211556  68.938504  41.542563
    2  29.248036  72.005306  57.855365  45.931715
               a          b          c          d
    2  29.248036  72.005306  57.855365  45.931715
    3  88.148296   6.211556  68.938504  41.542563
    4  69.739134  80.084366  89.005538  56.825475
    5  57.327269  87.623119  93.655538   5.859571
               a          b          c          d
    h  50.579469  80.239138  24.085110  39.443600
    s  30.906725  39.175302  11.161542  81.010205
    x  19.900056  18.421110   4.995141  12.605395
    g  67.760755  72.573568  33.507090  69.854906
               a          b          c          d
    g  67.760755  72.573568  33.507090  69.854906
    h  50.579469  80.239138  24.085110  39.443600
    s  30.906725  39.175302  11.161542  81.010205
    x  19.900056  18.421110   4.995141  12.605395
    
