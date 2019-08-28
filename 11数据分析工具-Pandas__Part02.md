

```python
'''
【课程2.8】  时间模块：datetime

datetime模块，主要掌握：datetime.date(), datetime.datetime(), datetime.timedelta()

日期解析方法：parser.parse

'''
```


```python
# datetime.date：date对象

import datetime  # 也可以写 from datetime import date

today = datetime.date.today()
print(today,type(today))
print(str(today),type(str(today)))
# datetime.date.today 返回今日
# 输出格式为 date类

t = datetime.date(2019,6,1)
print(t)
# (年，月，日) → 直接得到当时日期
```

    2019-08-26 <class 'datetime.date'>
    2019-08-26 <class 'str'>
    2019-06-01
    


```python
# datetime.datetime：datetime对象

now = datetime.datetime.now()
print(now,type(now))
print(str(now),type(str(now))) 
# .now()方法，输出当前时间
# 输出格式为 datetime类
# 可通过str()转化为字符串

t1 = datetime.datetime(2019,6,1)
t2 = datetime.datetime(2019,1,1,12,44,33)
print(t1,t2)
# (年，月，日，时，分，秒)，至少输入年月日
t2-t1
print(t2-t1,type(t2-t1))
# 相减得到时间差 —— timedelta
```

    2019-08-26 14:25:11.916052 <class 'datetime.datetime'>
    2019-08-26 14:25:11.916052 <class 'str'>
    2019-06-01 00:00:00 2019-01-01 12:44:33
    -151 days, 12:44:33 <class 'datetime.timedelta'>
    


```python
# datetime.timedelta：时间差

today = datetime.datetime.today()  # datetime.datetime也有today()方法
yestoday = today - datetime.timedelta(1)  # 
print(today)
print(yestoday)
print(today - datetime.timedelta(7))
# 时间差主要用作时间的加减法，相当于可被识别的时间“差值”
```

    2019-08-26 14:27:06.347598
    2019-08-25 14:27:06.347598
    2019-08-19 14:27:06.347598
    


```python
# parser.parse：日期字符串转换

from dateutil.parser import parse

date = '12-21-2017'
t = parse(date)
print(t,type(t))
# 直接将str转化成datetime.datetime

print(parse('2000-1-1'),'\n',
     parse('5/1/2014'),'\n',
     parse('5/1/2014', dayfirst = True),'\n',  # 国际通用格式中，日在月之前，可以通过dayfirst来设置
     parse('22/1/2014'),'\n',
     parse('Jan 31, 1997 10:45 PM'))
# 各种格式可以解析，但无法支持中文
```

    2017-12-21 00:00:00 <class 'datetime.datetime'>
    2000-01-01 00:00:00 
     2014-05-01 00:00:00 
     2014-01-05 00:00:00 
     2014-01-22 00:00:00 
     1997-01-31 22:45:00
    


```python
'''
【课程2.9】  Pandas时刻数据：Timestamp

时刻数据代表时间点，是pandas的数据类型，是将值与时间点相关联的最基本类型的时间序列数据

pandas.Timestamp()

'''
```


```python
# pd.Timestamp()

import numpy as np
import pandas as pd

date1 = datetime.datetime(2018,12,1,12,45,30)  # 创建一个datetime.datetime
date2 = '2019-12-21'  # 创建一个字符串
t1 = pd.Timestamp(date1)
t2 = pd.Timestamp(date2)
print(t1,type(t1))
print(t2)
print(pd.Timestamp('2019-12-21 15:00:22'))
# 直接生成pandas的时刻数据 → 时间戳
# 数据类型为 pandas的Timestamp
```

    2018-12-01 12:45:30 <class 'pandas._libs.tslibs.timestamps.Timestamp'>
    2019-12-21 00:00:00
    2019-12-21 15:00:22
    


```python
# pd.to_datetime

from datetime import datetime

date1 = datetime(2016,12,1,12,45,30)
date2 = '2017-12-21'
t1 = pd.to_datetime(date1)
t2 = pd.to_datetime(date2)
print(t1,type(t1))
print(t2,type(t2))
# pd.to_datetime()：如果是单个时间数据，转换成pandas的时刻数据，数据类型为Timestamp

lst_date = [ '2017-12-21', '2017-12-22', '2017-12-23']
t3 = pd.to_datetime(lst_date)
print(t3,type(t3))
# 多个时间数据，将会转换为pandas的DatetimeIndex
```

    2016-12-01 12:45:30 <class 'pandas._libs.tslibs.timestamps.Timestamp'>
    2017-12-21 00:00:00 <class 'pandas._libs.tslibs.timestamps.Timestamp'>
    DatetimeIndex(['2017-12-21', '2017-12-22', '2017-12-23'], dtype='datetime64[ns]', freq=None) <class 'pandas.core.indexes.datetimes.DatetimeIndex'>
    


```python
# pd.to_datetime → 多个时间数据转换时间戳索引

date1 = [datetime(2015,6,1),datetime(2015,7,1),datetime(2015,8,1),datetime(2015,9,1),datetime(2015,10,1)]
date2 = ['2017-2-1','2017-2-2','2017-2-3','2017-2-4','2017-2-5','2017-2-6']
print(date1)
print(date2)
t1 = pd.to_datetime(date2)
t2 = pd.to_datetime(date2)
print(t1)
print(t2)
# 多个时间数据转换为 DatetimeIndex

date3 = ['2019-2-1','2019-2-2','2019-2-3','hello world!','2019-2-5','2019-2-6']
t3 = pd.to_datetime(date3, errors = 'ignore')
print(t3,type(t3))
# 当一组时间序列中夹杂其他格式数据，可用errors参数返回
# errors = 'ignore':不可解析时返回原始输入，这里就是直接生成一般数组

t4 = pd.to_datetime(date3, errors = 'coerce')
print(t4,type(t4))
# errors = 'coerce':不可扩展，缺失值返回NaT（Not a Time），结果认为DatetimeIndex
```

    [datetime.datetime(2015, 6, 1, 0, 0), datetime.datetime(2015, 7, 1, 0, 0), datetime.datetime(2015, 8, 1, 0, 0), datetime.datetime(2015, 9, 1, 0, 0), datetime.datetime(2015, 10, 1, 0, 0)]
    ['2017-2-1', '2017-2-2', '2017-2-3', '2017-2-4', '2017-2-5', '2017-2-6']
    DatetimeIndex(['2017-02-01', '2017-02-02', '2017-02-03', '2017-02-04',
                   '2017-02-05', '2017-02-06'],
                  dtype='datetime64[ns]', freq=None)
    DatetimeIndex(['2017-02-01', '2017-02-02', '2017-02-03', '2017-02-04',
                   '2017-02-05', '2017-02-06'],
                  dtype='datetime64[ns]', freq=None)
    Index(['2019-2-1', '2019-2-2', '2019-2-3', 'hello world!', '2019-2-5',
           '2019-2-6'],
          dtype='object') <class 'pandas.core.indexes.base.Index'>
    DatetimeIndex(['2019-02-01', '2019-02-02', '2019-02-03', 'NaT', '2019-02-05',
                   '2019-02-06'],
                  dtype='datetime64[ns]', freq=None) <class 'pandas.core.indexes.datetimes.DatetimeIndex'>
    


```python
'''
【课程2.10】  Pandas时间戳索引：DatetimeIndex

核心：pd.date_range()

'''
```


```python
# pd.DatetimeIndex()与TimeSeries时间序列

rng = pd.DatetimeIndex(['12/1/2017','12/2/2017','12/3/2017','12/4/2017','12/5/2017'])
print(rng,type(rng))
print(rng[0],type(rng[0]))
# 直接生成时间戳索引，支持str、datetime.datetime
# 单个时间戳为Timestamp，多个时间戳为DatetimeIndex

st = pd.Series(np.random.rand(len(rng)), index = rng)
print(st,type(st))
print(st.index)
# 以DatetimeIndex为index的Series，为TimeSries，时间序列
```

    DatetimeIndex(['2017-12-01', '2017-12-02', '2017-12-03', '2017-12-04',
                   '2017-12-05'],
                  dtype='datetime64[ns]', freq=None) <class 'pandas.core.indexes.datetimes.DatetimeIndex'>
    2017-12-01 00:00:00 <class 'pandas._libs.tslibs.timestamps.Timestamp'>
    2017-12-01    0.567396
    2017-12-02    0.795321
    2017-12-03    0.414010
    2017-12-04    0.820784
    2017-12-05    0.477153
    dtype: float64 <class 'pandas.core.series.Series'>
    DatetimeIndex(['2017-12-01', '2017-12-02', '2017-12-03', '2017-12-04',
                   '2017-12-05'],
                  dtype='datetime64[ns]', freq=None)
    


```python
# pd.date_range()-日期范围：生成日期范围
# 2种生成方式：①start + end； ②start/end + periods
# 默认频率：day

rng1 = pd.date_range('1/1/2017','1/10/2017', normalize=True)
rng2 = pd.date_range(start = '1/1/2017', periods = 10)
rng3 = pd.date_range(end = '1/30/2017 15:00:00', periods = 10)  # 增加了时、分、秒
print(rng1,type(rng1))
print(rng2)
print(rng3)
print('-------')
# 直接生成DatetimeIndex
# pd.date_range(start=None, end=None, periods=None, freq='D', tz=None, normalize=False, name=None, closed=None, **kwargs)
# start：开始时间
# end：结束时间
# periods：偏移量
# freq：频率，默认天，pd.date_range()默认频率为日历日，pd.bdate_range()默认频率为工作日
# tz：时区

rng4 = pd.date_range(start = '1/1/2017 15:30', periods = 10, name = 'hello world!', normalize = True)
print(rng4)
print('-------')
# normalize：时间参数值正则化到午夜时间戳（这里最后就直接变成0:00:00，并不是15:30:00）
# name：索引对象名称

print(pd.date_range('20170101','20170104'))  # 20170101也可读取
print(pd.date_range('20170101','20170104',closed = 'right'))
print(pd.date_range('20170101','20170104',closed = 'left'))
print('-------')
# closed：默认为None的情况下，左闭右闭，left则左闭右开，right则左开右闭

print(pd.bdate_range('20170101','20170107'))
# pd.bdate_range()默认频率为工作日

print(list(pd.date_range(start = '1/1/2017', periods = 10)))
# 直接转化为list，元素为Timestamp
```

    DatetimeIndex(['2017-01-01', '2017-01-02', '2017-01-03', '2017-01-04',
                   '2017-01-05', '2017-01-06', '2017-01-07', '2017-01-08',
                   '2017-01-09', '2017-01-10'],
                  dtype='datetime64[ns]', freq='D') <class 'pandas.core.indexes.datetimes.DatetimeIndex'>
    DatetimeIndex(['2017-01-01', '2017-01-02', '2017-01-03', '2017-01-04',
                   '2017-01-05', '2017-01-06', '2017-01-07', '2017-01-08',
                   '2017-01-09', '2017-01-10'],
                  dtype='datetime64[ns]', freq='D')
    DatetimeIndex(['2017-01-21 15:00:00', '2017-01-22 15:00:00',
                   '2017-01-23 15:00:00', '2017-01-24 15:00:00',
                   '2017-01-25 15:00:00', '2017-01-26 15:00:00',
                   '2017-01-27 15:00:00', '2017-01-28 15:00:00',
                   '2017-01-29 15:00:00', '2017-01-30 15:00:00'],
                  dtype='datetime64[ns]', freq='D')
    -------
    DatetimeIndex(['2017-01-01', '2017-01-02', '2017-01-03', '2017-01-04',
                   '2017-01-05', '2017-01-06', '2017-01-07', '2017-01-08',
                   '2017-01-09', '2017-01-10'],
                  dtype='datetime64[ns]', name='hello world!', freq='D')
    -------
    DatetimeIndex(['2017-01-01', '2017-01-02', '2017-01-03', '2017-01-04'], dtype='datetime64[ns]', freq='D')
    DatetimeIndex(['2017-01-02', '2017-01-03', '2017-01-04'], dtype='datetime64[ns]', freq='D')
    DatetimeIndex(['2017-01-01', '2017-01-02', '2017-01-03'], dtype='datetime64[ns]', freq='D')
    -------
    DatetimeIndex(['2017-01-02', '2017-01-03', '2017-01-04', '2017-01-05',
                   '2017-01-06'],
                  dtype='datetime64[ns]', freq='B')
    [Timestamp('2017-01-01 00:00:00', freq='D'), Timestamp('2017-01-02 00:00:00', freq='D'), Timestamp('2017-01-03 00:00:00', freq='D'), Timestamp('2017-01-04 00:00:00', freq='D'), Timestamp('2017-01-05 00:00:00', freq='D'), Timestamp('2017-01-06 00:00:00', freq='D'), Timestamp('2017-01-07 00:00:00', freq='D'), Timestamp('2017-01-08 00:00:00', freq='D'), Timestamp('2017-01-09 00:00:00', freq='D'), Timestamp('2017-01-10 00:00:00', freq='D')]
    


```python
# pd.date_range()-日期范围：频率(1)

print(pd.date_range('2017/1/1','2017/1/4'))  # 默认freq = 'D'：每日历日
print(pd.date_range('2017/1/1','2017/1/4', freq = 'B'))  # B：每工作日
print(pd.date_range('2017/1/1','2017/1/2', freq = 'H'))  # H：每小时
print(pd.date_range('2017/1/1 12:00','2017/1/1 12:10', freq = 'T'))  # T/MIN：每分
print(pd.date_range('2017/1/1 12:00:00','2017/1/1 12:00:10', freq = 'S'))  # S：每秒
print(pd.date_range('2017/1/1 12:00:00','2017/1/1 12:00:10', freq = 'L'))  # L：每毫秒（千分之一秒）
print(pd.date_range('2017/1/1 12:00:00','2017/1/1 12:00:10', freq = 'U'))  # U：每微秒（百万分之一秒）

print(pd.date_range('2017/1/1','2017/2/1', freq = 'W-MON'))  
# W-MON：从指定星期几开始算起，每周
# 星期几缩写：MON/TUE/WED/THU/FRI/SAT/SUN

print(pd.date_range('2017/1/1','2017/5/1', freq = 'WOM-2MON'))  
# WOM-2MON：每月的第几个星期几开始算，这里是每月第二个星期一
```

    DatetimeIndex(['2017-01-01', '2017-01-02', '2017-01-03', '2017-01-04'], dtype='datetime64[ns]', freq='D')
    DatetimeIndex(['2017-01-02', '2017-01-03', '2017-01-04'], dtype='datetime64[ns]', freq='B')
    DatetimeIndex(['2017-01-01 00:00:00', '2017-01-01 01:00:00',
                   '2017-01-01 02:00:00', '2017-01-01 03:00:00',
                   '2017-01-01 04:00:00', '2017-01-01 05:00:00',
                   '2017-01-01 06:00:00', '2017-01-01 07:00:00',
                   '2017-01-01 08:00:00', '2017-01-01 09:00:00',
                   '2017-01-01 10:00:00', '2017-01-01 11:00:00',
                   '2017-01-01 12:00:00', '2017-01-01 13:00:00',
                   '2017-01-01 14:00:00', '2017-01-01 15:00:00',
                   '2017-01-01 16:00:00', '2017-01-01 17:00:00',
                   '2017-01-01 18:00:00', '2017-01-01 19:00:00',
                   '2017-01-01 20:00:00', '2017-01-01 21:00:00',
                   '2017-01-01 22:00:00', '2017-01-01 23:00:00',
                   '2017-01-02 00:00:00'],
                  dtype='datetime64[ns]', freq='H')
    DatetimeIndex(['2017-01-01 12:00:00', '2017-01-01 12:01:00',
                   '2017-01-01 12:02:00', '2017-01-01 12:03:00',
                   '2017-01-01 12:04:00', '2017-01-01 12:05:00',
                   '2017-01-01 12:06:00', '2017-01-01 12:07:00',
                   '2017-01-01 12:08:00', '2017-01-01 12:09:00',
                   '2017-01-01 12:10:00'],
                  dtype='datetime64[ns]', freq='T')
    DatetimeIndex(['2017-01-01 12:00:00', '2017-01-01 12:00:01',
                   '2017-01-01 12:00:02', '2017-01-01 12:00:03',
                   '2017-01-01 12:00:04', '2017-01-01 12:00:05',
                   '2017-01-01 12:00:06', '2017-01-01 12:00:07',
                   '2017-01-01 12:00:08', '2017-01-01 12:00:09',
                   '2017-01-01 12:00:10'],
                  dtype='datetime64[ns]', freq='S')
    DatetimeIndex([       '2017-01-01 12:00:00', '2017-01-01 12:00:00.001000',
                   '2017-01-01 12:00:00.002000', '2017-01-01 12:00:00.003000',
                   '2017-01-01 12:00:00.004000', '2017-01-01 12:00:00.005000',
                   '2017-01-01 12:00:00.006000', '2017-01-01 12:00:00.007000',
                   '2017-01-01 12:00:00.008000', '2017-01-01 12:00:00.009000',
                   ...
                   '2017-01-01 12:00:09.991000', '2017-01-01 12:00:09.992000',
                   '2017-01-01 12:00:09.993000', '2017-01-01 12:00:09.994000',
                   '2017-01-01 12:00:09.995000', '2017-01-01 12:00:09.996000',
                   '2017-01-01 12:00:09.997000', '2017-01-01 12:00:09.998000',
                   '2017-01-01 12:00:09.999000',        '2017-01-01 12:00:10'],
                  dtype='datetime64[ns]', length=10001, freq='L')
    DatetimeIndex([       '2017-01-01 12:00:00', '2017-01-01 12:00:00.000001',
                   '2017-01-01 12:00:00.000002', '2017-01-01 12:00:00.000003',
                   '2017-01-01 12:00:00.000004', '2017-01-01 12:00:00.000005',
                   '2017-01-01 12:00:00.000006', '2017-01-01 12:00:00.000007',
                   '2017-01-01 12:00:00.000008', '2017-01-01 12:00:00.000009',
                   ...
                   '2017-01-01 12:00:09.999991', '2017-01-01 12:00:09.999992',
                   '2017-01-01 12:00:09.999993', '2017-01-01 12:00:09.999994',
                   '2017-01-01 12:00:09.999995', '2017-01-01 12:00:09.999996',
                   '2017-01-01 12:00:09.999997', '2017-01-01 12:00:09.999998',
                   '2017-01-01 12:00:09.999999',        '2017-01-01 12:00:10'],
                  dtype='datetime64[ns]', length=10000001, freq='U')
    DatetimeIndex(['2017-01-02', '2017-01-09', '2017-01-16', '2017-01-23',
                   '2017-01-30'],
                  dtype='datetime64[ns]', freq='W-MON')
    DatetimeIndex(['2017-01-09', '2017-02-13', '2017-03-13', '2017-04-10'], dtype='datetime64[ns]', freq='WOM-2MON')
    


```python
# pd.date_range()-日期范围：频率(2)

print(pd.date_range('2017','2018', freq = 'M'))  
print(pd.date_range('2017','2020', freq = 'Q-DEC'))  
print(pd.date_range('2017','2020', freq = 'A-DEC')) 
print('------')
# M：每月最后一个日历日
# Q-月：指定月为季度末，每个季度末最后一月的最后一个日历日
# A-月：每年指定月份的最后一个日历日
# 月缩写：JAN/FEB/MAR/APR/MAY/JUN/JUL/AUG/SEP/OCT/NOV/DEC
# 所以Q-月只有三种情况：1-4-7-10,2-5-8-11,3-6-9-12

print(pd.date_range('2017','2018', freq = 'BM'))  
print(pd.date_range('2017','2020', freq = 'BQ-DEC'))  
print(pd.date_range('2017','2020', freq = 'BA-DEC')) 
print('------')
# BM：每月最后一个工作日
# BQ-月：指定月为季度末，每个季度末最后一月的最后一个工作日
# BA-月：每年指定月份的最后一个工作日

print(pd.date_range('2017','2018', freq = 'MS'))  
print(pd.date_range('2017','2020', freq = 'QS-DEC'))  
print(pd.date_range('2017','2020', freq = 'AS-DEC')) 
print('------')
# M：每月第一个日历日
# Q-月：指定月为季度末，每个季度末最后一月的第一个日历日
# A-月：每年指定月份的第一个日历日

print(pd.date_range('2017','2018', freq = 'BMS'))  
print(pd.date_range('2017','2020', freq = 'BQS-DEC'))  
print(pd.date_range('2017','2020', freq = 'BAS-DEC')) 
print('------')
# BM：每月第一个工作日
# BQ-月：指定月为季度末，每个季度末最后一月的第一个工作日
# BA-月：每年指定月份的第一个工作日
```

    DatetimeIndex(['2017-01-31', '2017-02-28', '2017-03-31', '2017-04-30',
                   '2017-05-31', '2017-06-30', '2017-07-31', '2017-08-31',
                   '2017-09-30', '2017-10-31', '2017-11-30', '2017-12-31'],
                  dtype='datetime64[ns]', freq='M')
    DatetimeIndex(['2017-03-31', '2017-06-30', '2017-09-30', '2017-12-31',
                   '2018-03-31', '2018-06-30', '2018-09-30', '2018-12-31',
                   '2019-03-31', '2019-06-30', '2019-09-30', '2019-12-31'],
                  dtype='datetime64[ns]', freq='Q-DEC')
    DatetimeIndex(['2017-12-31', '2018-12-31', '2019-12-31'], dtype='datetime64[ns]', freq='A-DEC')
    ------
    DatetimeIndex(['2017-01-31', '2017-02-28', '2017-03-31', '2017-04-28',
                   '2017-05-31', '2017-06-30', '2017-07-31', '2017-08-31',
                   '2017-09-29', '2017-10-31', '2017-11-30', '2017-12-29'],
                  dtype='datetime64[ns]', freq='BM')
    DatetimeIndex(['2017-03-31', '2017-06-30', '2017-09-29', '2017-12-29',
                   '2018-03-30', '2018-06-29', '2018-09-28', '2018-12-31',
                   '2019-03-29', '2019-06-28', '2019-09-30', '2019-12-31'],
                  dtype='datetime64[ns]', freq='BQ-DEC')
    DatetimeIndex(['2017-12-29', '2018-12-31', '2019-12-31'], dtype='datetime64[ns]', freq='BA-DEC')
    ------
    DatetimeIndex(['2017-01-01', '2017-02-01', '2017-03-01', '2017-04-01',
                   '2017-05-01', '2017-06-01', '2017-07-01', '2017-08-01',
                   '2017-09-01', '2017-10-01', '2017-11-01', '2017-12-01',
                   '2018-01-01'],
                  dtype='datetime64[ns]', freq='MS')
    DatetimeIndex(['2017-03-01', '2017-06-01', '2017-09-01', '2017-12-01',
                   '2018-03-01', '2018-06-01', '2018-09-01', '2018-12-01',
                   '2019-03-01', '2019-06-01', '2019-09-01', '2019-12-01'],
                  dtype='datetime64[ns]', freq='QS-DEC')
    DatetimeIndex(['2017-12-01', '2018-12-01', '2019-12-01'], dtype='datetime64[ns]', freq='AS-DEC')
    ------
    DatetimeIndex(['2017-01-02', '2017-02-01', '2017-03-01', '2017-04-03',
                   '2017-05-01', '2017-06-01', '2017-07-03', '2017-08-01',
                   '2017-09-01', '2017-10-02', '2017-11-01', '2017-12-01',
                   '2018-01-01'],
                  dtype='datetime64[ns]', freq='BMS')
    DatetimeIndex(['2017-03-01', '2017-06-01', '2017-09-01', '2017-12-01',
                   '2018-03-01', '2018-06-01', '2018-09-03', '2018-12-03',
                   '2019-03-01', '2019-06-03', '2019-09-02', '2019-12-02'],
                  dtype='datetime64[ns]', freq='BQS-DEC')
    DatetimeIndex(['2017-12-01', '2018-12-03', '2019-12-02'], dtype='datetime64[ns]', freq='BAS-DEC')
    ------
    


```python
# pd.date_range()-日期范围：复合频率

print(pd.date_range('2017/1/1','2017/2/1', freq = '7D'))  # 7天
print(pd.date_range('2017/1/1','2017/1/2', freq = '2h30min'))  # 2小时30分钟
print(pd.date_range('2017','2018', freq = '2M'))  # 2月，每月最后一个日历日
print(pd.date_range('2017','2018', freq = '2MS')) # 工作日
```

    DatetimeIndex(['2017-01-01', '2017-01-08', '2017-01-15', '2017-01-22',
                   '2017-01-29'],
                  dtype='datetime64[ns]', freq='7D')
    DatetimeIndex(['2017-01-01 00:00:00', '2017-01-01 02:30:00',
                   '2017-01-01 05:00:00', '2017-01-01 07:30:00',
                   '2017-01-01 10:00:00', '2017-01-01 12:30:00',
                   '2017-01-01 15:00:00', '2017-01-01 17:30:00',
                   '2017-01-01 20:00:00', '2017-01-01 22:30:00'],
                  dtype='datetime64[ns]', freq='150T')
    DatetimeIndex(['2017-01-31', '2017-03-31', '2017-05-31', '2017-07-31',
                   '2017-09-30', '2017-11-30'],
                  dtype='datetime64[ns]', freq='2M')
    DatetimeIndex(['2017-01-01', '2017-03-01', '2017-05-01', '2017-07-01',
                   '2017-09-01', '2017-11-01', '2018-01-01'],
                  dtype='datetime64[ns]', freq='2MS')
    


```python
# asfreq：时期频率转换

ts = pd.Series(np.random.rand(4),
              index = pd.date_range('20170101','20170104'))
print(ts)
print(ts.asfreq('4H',method = 'ffill'))
# 改变频率，这里是D改为4H
# method：插值模式，None不插值，ffill用之前值填充，bfill用之后值填充
```

    2017-01-01    0.945391
    2017-01-02    0.656020
    2017-01-03    0.295795
    2017-01-04    0.318078
    Freq: D, dtype: float64
    2017-01-01 00:00:00    0.945391
    2017-01-01 04:00:00    0.945391
    2017-01-01 08:00:00    0.945391
    2017-01-01 12:00:00    0.945391
    2017-01-01 16:00:00    0.945391
    2017-01-01 20:00:00    0.945391
    2017-01-02 00:00:00    0.656020
    2017-01-02 04:00:00    0.656020
    2017-01-02 08:00:00    0.656020
    2017-01-02 12:00:00    0.656020
    2017-01-02 16:00:00    0.656020
    2017-01-02 20:00:00    0.656020
    2017-01-03 00:00:00    0.295795
    2017-01-03 04:00:00    0.295795
    2017-01-03 08:00:00    0.295795
    2017-01-03 12:00:00    0.295795
    2017-01-03 16:00:00    0.295795
    2017-01-03 20:00:00    0.295795
    2017-01-04 00:00:00    0.318078
    Freq: 4H, dtype: float64
    


```python
# pd.date_range()-日期范围：超前/滞后数据

ts = pd.Series(np.random.rand(4),
              index = pd.date_range('20170101','20170104'))
print(ts)

print(ts.shift(2))
print(ts.shift(-2))
print('------')
# 正数：数值后移（滞后）；负数：数值前移（超前）

per = ts/ts.shift(1) - 1
print(per)
print('------')
# 计算变化百分比，这里计算：该时间戳与上一个时间戳相比，变化百分比

print(ts.shift(2, freq = 'D'))
print(ts.shift(2, freq = 'T'))
# 加上freq参数：对时间戳进行位移，而不是对数值进行位移
```

    2017-01-01    0.603490
    2017-01-02    0.284396
    2017-01-03    0.711357
    2017-01-04    0.522265
    Freq: D, dtype: float64
    2017-01-01         NaN
    2017-01-02         NaN
    2017-01-03    0.603490
    2017-01-04    0.284396
    Freq: D, dtype: float64
    2017-01-01    0.711357
    2017-01-02    0.522265
    2017-01-03         NaN
    2017-01-04         NaN
    Freq: D, dtype: float64
    ------
    2017-01-01         NaN
    2017-01-02   -0.528747
    2017-01-03    1.501290
    2017-01-04   -0.265819
    Freq: D, dtype: float64
    ------
    2017-01-03    0.603490
    2017-01-04    0.284396
    2017-01-05    0.711357
    2017-01-06    0.522265
    Freq: D, dtype: float64
    2017-01-01 00:02:00    0.603490
    2017-01-02 00:02:00    0.284396
    2017-01-03 00:02:00    0.711357
    2017-01-04 00:02:00    0.522265
    Freq: D, dtype: float64
    


```python
'''
【课程2.11】  Pandas时期：Period

核心：pd.Period()

'''
```


```python
# pd.Period()创建时期

p = pd.Period('2017', freq = 'M')
print(p, type(p))
# 生成一个以2017-01开始，月为频率的时间构造器
# pd.Period()参数：一个时间戳 + freq 参数 → freq 用于指明该 period 的长度，时间戳则说明该 period 在时间轴上的位置

print(p + 1)
print(p - 2)
print(pd.Period('2012', freq = 'A-DEC') - 1)
# 通过加减整数，将周期整体移动
# 这里是按照 月、年 移动
```

    2017-01 <class 'pandas._period.Period'>
    2017-02
    2016-11
    2011
    


```python
# pd.period_range()创建时期范围

prng = pd.period_range('1/1/2011', '1/1/2012', freq='M')
print(prng,type(prng))
print(prng[0],type(prng[0]))
# 数据格式为PeriodIndex，单个数值为Period

ts = pd.Series(np.random.rand(len(prng)), index = prng)
print(ts,type(ts))
print(ts.index)
# 时间序列

# Period('2011', freq = 'A-DEC')可以看成多个时间期的时间段中的游标
# Timestamp表示一个时间戳，是一个时间截面；Period是一个时期，是一个时间段！！但两者作为index时区别不大
```

    PeriodIndex(['2011-01', '2011-02', '2011-03', '2011-04', '2011-05', '2011-06',
                 '2011-07', '2011-08', '2011-09', '2011-10', '2011-11', '2011-12',
                 '2012-01'],
                dtype='int64', freq='M') <class 'pandas.tseries.period.PeriodIndex'>
    2011-01 <class 'pandas._period.Period'>
    2011-01    0.342571
    2011-02    0.826151
    2011-03    0.370505
    2011-04    0.137151
    2011-05    0.679976
    2011-06    0.265928
    2011-07    0.416502
    2011-08    0.874078
    2011-09    0.112801
    2011-10    0.112504
    2011-11    0.448408
    2011-12    0.851046
    2012-01    0.370605
    Freq: M, dtype: float64 <class 'pandas.core.series.Series'>
    PeriodIndex(['2011-01', '2011-02', '2011-03', '2011-04', '2011-05', '2011-06',
                 '2011-07', '2011-08', '2011-09', '2011-10', '2011-11', '2011-12',
                 '2012-01'],
                dtype='int64', freq='M')
    


```python
# asfreq：频率转换

p = pd.Period('2017','A-DEC')
print(p)
print(p.asfreq('M', how = 'start'))  # 也可写 how = 's'
print(p.asfreq('D', how = 'end'))  # 也可写 how = 'e'
# 通过.asfreq(freq, method=None, how=None)方法转换成别的频率

prng = pd.period_range('2017','2018',freq = 'M')
ts1 = pd.Series(np.random.rand(len(prng)), index = prng)
ts2 = pd.Series(np.random.rand(len(prng)), index = prng.asfreq('D', how = 'start'))
print(ts1.head(10),len(ts1))
print(ts2.head(),len(ts2))
# asfreq也可以转换TIMESeries的index
```

    2017
    2017-01
    2017-12-31
    2017-01    0.778442
    2017-02    0.216384
    2017-03    0.550383
    2017-04    0.756000
    2017-05    0.497717
    2017-06    0.471157
    2017-07    0.471012
    2017-08    0.837969
    2017-09    0.853519
    2017-10    0.383256
    Freq: M, dtype: float64 13
    2017-01-01    0.480776
    2017-02-01    0.253036
    2017-03-01    0.622906
    2017-04-01    0.766904
    2017-05-01    0.849050
    Freq: D, dtype: float64 13
    


```python
# 时间戳与时期之间的转换：pd.to_period()、pd.to_timestamp()

rng = pd.date_range('2017/1/1', periods = 10, freq = 'M')
prng = pd.period_range('2017','2018', freq = 'M')

ts1 = pd.Series(np.random.rand(len(rng)), index = rng)
print(ts1.head())
print(ts1.to_period().head())
# 每月最后一日，转化为每月

ts2 = pd.Series(np.random.rand(len(prng)), index = prng)
print(ts2.head())
print(ts2.to_timestamp().head())
# 每月，转化为每月第一天
```

    2017-01-31    0.125288
    2017-02-28    0.497174
    2017-03-31    0.573114
    2017-04-30    0.665665
    2017-05-31    0.263561
    Freq: M, dtype: float64
    2017-01    0.125288
    2017-02    0.497174
    2017-03    0.573114
    2017-04    0.665665
    2017-05    0.263561
    Freq: M, dtype: float64
    2017-01    0.748661
    2017-02    0.095891
    2017-03    0.280341
    2017-04    0.569813
    2017-05    0.067677
    Freq: M, dtype: float64
    2017-01-01    0.748661
    2017-02-01    0.095891
    2017-03-01    0.280341
    2017-04-01    0.569813
    2017-05-01    0.067677
    Freq: MS, dtype: float64
    


```python
'''
【课程2.12】  时间序列 - 索引及切片

TimeSeries是Series的一个子类，所以Series索引及数据选取方面的方法基本一样

同时TimeSeries通过时间序列有更便捷的方法做索引和切片
 
'''
```


```python
# 索引
import pandas as pd
import numpy as np
from datetime import datetime

rng = pd.date_range('2017/1','2017/3')
ts = pd.Series(np.random.rand(len(rng)), index = rng)
print(ts.head())

print(ts[0])
print(ts[:2])
print('-----')
# 基本下标位置索引

print(ts['2017/1/2'])
print(ts['20170103'])
print(ts['1/10/2017'])
print(ts[datetime(2017,1,20)])
print('-----')
# 时间序列标签索引，支持各种时间字符串，以及datetime.datetime

# 时间序列由于按照时间先后排序，故不用考虑顺序问题
# 索引方法同样适用于Dataframe   .loc .iloc
```

    2017-01-01    0.550144
    2017-01-02    0.590197
    2017-01-03    0.696595
    2017-01-04    0.012560
    2017-01-05    0.539697
    Freq: D, dtype: float64
    0.5501435575774801
    2017-01-01    0.550144
    2017-01-02    0.590197
    Freq: D, dtype: float64
    -----
    0.5901965799252412
    0.6965949048146604
    0.08791713429913361
    0.3624791400966191
    -----
    


```python
# 切片

rng = pd.date_range('2017/1','2017/3',freq = '12H')
ts = pd.Series(np.random.rand(len(rng)), index = rng)

print(ts['2017/1/5':'2017/1/10'])
print('-----')
# 和Series按照index索引原理一样，也是末端包含

print(ts['2017/2'].head())
# 传入月，直接得到一个切片
```

    2017-01-05 00:00:00    0.462085
    2017-01-05 12:00:00    0.778637
    2017-01-06 00:00:00    0.356306
    2017-01-06 12:00:00    0.667964
    2017-01-07 00:00:00    0.246857
    2017-01-07 12:00:00    0.386956
    2017-01-08 00:00:00    0.328203
    2017-01-08 12:00:00    0.260853
    2017-01-09 00:00:00    0.224920
    2017-01-09 12:00:00    0.397457
    2017-01-10 00:00:00    0.158729
    2017-01-10 12:00:00    0.501266
    Freq: 12H, dtype: float64
    -----
    2017-02-01 00:00:00    0.243932
    2017-02-01 12:00:00    0.220830
    2017-02-02 00:00:00    0.896107
    2017-02-02 12:00:00    0.476584
    2017-02-03 00:00:00    0.515817
    Freq: 12H, dtype: float64
    


```python
# 重复索引的时间序列

dates = pd.DatetimeIndex(['1/1/2015','1/2/2015','1/3/2015','1/4/2015','1/1/2015','1/2/2015'])
ts = pd.Series(np.random.rand(6), index = dates)
print(ts)
print(ts.is_unique,ts.index.is_unique)
print('-----')
# index有重复，is_unique检查 → values唯一，index不唯一

print(ts['20150101'],type(ts['20150101']))
print(ts['20150104'],type(ts['20150104']))
print('-----')
# index有重复的将返回多个值

print(ts.groupby(level = 0).mean())
# 通过groupby做分组，重复的值这里用平均值处理
```

    2015-01-01    0.300286
    2015-01-02    0.603865
    2015-01-03    0.017949
    2015-01-04    0.026621
    2015-01-01    0.791441
    2015-01-02    0.526622
    dtype: float64
    True False
    -----
    2015-01-01    0.300286
    2015-01-01    0.791441
    dtype: float64 <class 'pandas.core.series.Series'>
    2015-01-04    0.026621
    dtype: float64 <class 'pandas.core.series.Series'>
    -----
    2015-01-01    0.545863
    2015-01-02    0.565244
    2015-01-03    0.017949
    2015-01-04    0.026621
    dtype: float64
    


```python
'''
【课程2.13】  时间序列 - 重采样

将时间序列从一个频率转换为另一个频率的过程，且会有数据的结合

降采样：高频数据 → 低频数据，eg.以天为频率的数据转为以月为频率的数据
升采样：低频数据 → 高频数据，eg.以年为频率的数据转为以月为频率的数据
 
'''
```


```python
# 重采样：.resample()
# 创建一个以天为频率的TimeSeries，重采样为按2天为频率

rng = pd.date_range('20170101', periods = 12)
ts = pd.Series(np.arange(12), index = rng)
print(ts)

ts_re = ts.resample('5D')
ts_re2 = ts.resample('5D').sum()
print(ts_re, type(ts_re))
print(ts_re2, type(ts_re2))
print('-----')
# ts.resample('5D')：得到一个重采样构建器，频率改为5天
# ts.resample('5D').sum():得到一个新的聚合后的Series，聚合方式为求和
# freq：重采样频率 → ts.resample('5D')
# .sum()：聚合方法

print(ts.resample('5D').mean(),'→ 求平均值\n')
print(ts.resample('5D').max(),'→ 求最大值\n')
print(ts.resample('5D').min(),'→ 求最小值\n')
print(ts.resample('5D').median(),'→ 求中值\n')
print(ts.resample('5D').first(),'→ 返回第一个值\n')
print(ts.resample('5D').last(),'→ 返回最后一个值\n')
print(ts.resample('5D').ohlc(),'→ OHLC重采样\n')
# OHLC:金融领域的时间序列聚合方式 → open开盘、high最大值、low最小值、close收盘
```

    2017-01-01     0
    2017-01-02     1
    2017-01-03     2
    2017-01-04     3
    2017-01-05     4
    2017-01-06     5
    2017-01-07     6
    2017-01-08     7
    2017-01-09     8
    2017-01-10     9
    2017-01-11    10
    2017-01-12    11
    Freq: D, dtype: int32
    DatetimeIndexResampler [freq=<5 * Days>, axis=0, closed=left, label=left, convention=start, base=0] <class 'pandas.tseries.resample.DatetimeIndexResampler'>
    2017-01-01    10
    2017-01-06    35
    2017-01-11    21
    Freq: 5D, dtype: int32 <class 'pandas.core.series.Series'>
    -----
    2017-01-01     2.0
    2017-01-06     7.0
    2017-01-11    10.5
    Freq: 5D, dtype: float64 → 求平均值
    
    2017-01-01     4
    2017-01-06     9
    2017-01-11    11
    Freq: 5D, dtype: int32 → 求最大值
    
    2017-01-01     0
    2017-01-06     5
    2017-01-11    10
    Freq: 5D, dtype: int32 → 求最小值
    
    2017-01-01     2.0
    2017-01-06     7.0
    2017-01-11    10.5
    Freq: 5D, dtype: float64 → 求中值
    
    2017-01-01     0
    2017-01-06     5
    2017-01-11    10
    Freq: 5D, dtype: int32 → 返回第一个值
    
    2017-01-01     4
    2017-01-06     9
    2017-01-11    11
    Freq: 5D, dtype: int32 → 返回最后一个值
    
                open  high  low  close
    2017-01-01     0     4    0      4
    2017-01-06     5     9    5      9
    2017-01-11    10    11   10     11 → OHLC重采样
    
    


```python
# 降采样

rng = pd.date_range('20170101', periods = 12)
ts = pd.Series(np.arange(1,13), index = rng)
print(ts)

print(ts.resample('5D').sum(),'→ 默认\n')
print(ts.resample('5D', closed = 'left').sum(),'→ left\n')
print(ts.resample('5D', closed = 'right').sum(),'→ right\n')
print('-----')
# closed：各时间段哪一端是闭合（即包含）的，默认 左闭右闭
# 详解：这里values为0-11，按照5D重采样 → [1,2,3,4,5],[6,7,8,9,10],[11,12]
# left指定间隔左边为结束 → [1,2,3,4,5],[6,7,8,9,10],[11,12]
# right指定间隔右边为结束 → [1],[2,3,4,5,6],[7,8,9,10,11],[12]

print(ts.resample('5D', label = 'left').sum(),'→ leftlabel\n')
print(ts.resample('5D', label = 'right').sum(),'→ rightlabel\n')
# label：聚合值的index，默认为取左
# 值采样认为默认（这里closed默认）
```

    2017-01-01     1
    2017-01-02     2
    2017-01-03     3
    2017-01-04     4
    2017-01-05     5
    2017-01-06     6
    2017-01-07     7
    2017-01-08     8
    2017-01-09     9
    2017-01-10    10
    2017-01-11    11
    2017-01-12    12
    Freq: D, dtype: int32
    2017-01-01    15
    2017-01-06    40
    2017-01-11    23
    Freq: 5D, dtype: int32 → 默认
    
    2017-01-01    15
    2017-01-06    40
    2017-01-11    23
    Freq: 5D, dtype: int32 → left
    
    2016-12-27     1
    2017-01-01    20
    2017-01-06    45
    2017-01-11    12
    Freq: 5D, dtype: int32 → right
    
    -----
    2017-01-01    15
    2017-01-06    40
    2017-01-11    23
    Freq: 5D, dtype: int32 → leftlabel
    
    2017-01-06    15
    2017-01-11    40
    2017-01-16    23
    Freq: 5D, dtype: int32 → rightlabel
    
    


```python
# 升采样及插值

rng = pd.date_range('2017/1/1 0:0:0', periods = 5, freq = 'H')
ts = pd.DataFrame(np.arange(15).reshape(5,3),
                  index = rng,
                  columns = ['a','b','c'])
print(ts)

print(ts.resample('15T').asfreq())
print(ts.resample('15T').ffill())
print(ts.resample('15T').bfill())
# 低频转高频，主要是如何插值
# .asfreq()：不做填充，返回Nan
# .ffill()：向上填充
# .bfill()：向下填充
```

                          a   b   c
    2017-01-01 00:00:00   0   1   2
    2017-01-01 01:00:00   3   4   5
    2017-01-01 02:00:00   6   7   8
    2017-01-01 03:00:00   9  10  11
    2017-01-01 04:00:00  12  13  14
                            a     b     c
    2017-01-01 00:00:00   0.0   1.0   2.0
    2017-01-01 00:15:00   NaN   NaN   NaN
    2017-01-01 00:30:00   NaN   NaN   NaN
    2017-01-01 00:45:00   NaN   NaN   NaN
    2017-01-01 01:00:00   3.0   4.0   5.0
    2017-01-01 01:15:00   NaN   NaN   NaN
    2017-01-01 01:30:00   NaN   NaN   NaN
    2017-01-01 01:45:00   NaN   NaN   NaN
    2017-01-01 02:00:00   6.0   7.0   8.0
    2017-01-01 02:15:00   NaN   NaN   NaN
    2017-01-01 02:30:00   NaN   NaN   NaN
    2017-01-01 02:45:00   NaN   NaN   NaN
    2017-01-01 03:00:00   9.0  10.0  11.0
    2017-01-01 03:15:00   NaN   NaN   NaN
    2017-01-01 03:30:00   NaN   NaN   NaN
    2017-01-01 03:45:00   NaN   NaN   NaN
    2017-01-01 04:00:00  12.0  13.0  14.0
                          a   b   c
    2017-01-01 00:00:00   0   1   2
    2017-01-01 00:15:00   0   1   2
    2017-01-01 00:30:00   0   1   2
    2017-01-01 00:45:00   0   1   2
    2017-01-01 01:00:00   3   4   5
    2017-01-01 01:15:00   3   4   5
    2017-01-01 01:30:00   3   4   5
    2017-01-01 01:45:00   3   4   5
    2017-01-01 02:00:00   6   7   8
    2017-01-01 02:15:00   6   7   8
    2017-01-01 02:30:00   6   7   8
    2017-01-01 02:45:00   6   7   8
    2017-01-01 03:00:00   9  10  11
    2017-01-01 03:15:00   9  10  11
    2017-01-01 03:30:00   9  10  11
    2017-01-01 03:45:00   9  10  11
    2017-01-01 04:00:00  12  13  14
                          a   b   c
    2017-01-01 00:00:00   0   1   2
    2017-01-01 00:15:00   3   4   5
    2017-01-01 00:30:00   3   4   5
    2017-01-01 00:45:00   3   4   5
    2017-01-01 01:00:00   3   4   5
    2017-01-01 01:15:00   6   7   8
    2017-01-01 01:30:00   6   7   8
    2017-01-01 01:45:00   6   7   8
    2017-01-01 02:00:00   6   7   8
    2017-01-01 02:15:00   9  10  11
    2017-01-01 02:30:00   9  10  11
    2017-01-01 02:45:00   9  10  11
    2017-01-01 03:00:00   9  10  11
    2017-01-01 03:15:00  12  13  14
    2017-01-01 03:30:00  12  13  14
    2017-01-01 03:45:00  12  13  14
    2017-01-01 04:00:00  12  13  14
    


```python
# 时期重采样 - Period

prng = pd.period_range('2016','2017',freq = 'M')
ts = pd.Series(np.arange(len(prng)), index = prng)
print(ts)

print(ts.resample('3M').sum())  # 降采样
print(ts.resample('15D').ffill())  # 升采样
```

    2016-01     0
    2016-02     1
    2016-03     2
    2016-04     3
    2016-05     4
    2016-06     5
    2016-07     6
    2016-08     7
    2016-09     8
    2016-10     9
    2016-11    10
    2016-12    11
    2017-01    12
    Freq: M, dtype: int32
    2016-01-31     0
    2016-04-30     6
    2016-07-31    15
    2016-10-31    24
    2017-01-31    33
    Freq: 3M, dtype: int32
    2016-01-01     0
    2016-01-16     0
    2016-01-31     0
    2016-02-15     1
    2016-03-01     2
    2016-03-16     2
    2016-03-31     2
    2016-04-15     3
    2016-04-30     3
    2016-05-15     4
    2016-05-30     4
    2016-06-14     5
    2016-06-29     5
    2016-07-14     6
    2016-07-29     6
    2016-08-13     7
    2016-08-28     7
    2016-09-12     8
    2016-09-27     8
    2016-10-12     9
    2016-10-27     9
    2016-11-11    10
    2016-11-26    10
    2016-12-11    11
    2016-12-26    11
    Freq: 15D, dtype: int32
    
