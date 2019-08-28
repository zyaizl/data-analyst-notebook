

```python
'''
【课程3.13】  表格样式创建

表格视觉样式：Dataframe.style → 返回pandas.Styler对象的属性，具有格式化和显示Dataframe的有用方法

样式创建：
① Styler.applymap：elementwise → 按元素方式处理Dataframe
② Styler.apply：column- / row- / table-wise → 按行/列处理Dataframe
 
'''
```


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
% matplotlib inline
```


```python
# 样式

df = pd.DataFrame(np.random.randn(10,4),columns=['a','b','c','d'])
sty = df.style
print(sty,type(sty))
# 查看样式类型

sty
# 显示样式
```

    <pandas.formats.style.Styler object at 0x0000000009789CF8> <class 'pandas.formats.style.Styler'>
    





        <style  type="text/css" >
        
        
        </style>

        <table id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810d" None>
        

        <thead>
            
            <tr>
                
                <th class="blank">
                
                <th class="col_heading level0 col0">a
                
                <th class="col_heading level0 col1">b
                
                <th class="col_heading level0 col2">c
                
                <th class="col_heading level0 col3">d
                
            </tr>
            
        </thead>
        <tbody>
            
            <tr>
                
                <th id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810d" class="row_heading level3 row0">
                    0
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow0_col0" class="data row0 col0">
                    1.1215
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow0_col1" class="data row0 col1">
                    -1.38757
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow0_col2" class="data row0 col2">
                    -0.694214
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow0_col3" class="data row0 col3">
                    -0.887584
                
            </tr>
            
            <tr>
                
                <th id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810d" class="row_heading level3 row1">
                    1
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow1_col0" class="data row1 col0">
                    0.254148
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow1_col1" class="data row1 col1">
                    -0.578241
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow1_col2" class="data row1 col2">
                    0.336016
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow1_col3" class="data row1 col3">
                    -2.05696
                
            </tr>
            
            <tr>
                
                <th id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810d" class="row_heading level3 row2">
                    2
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow2_col0" class="data row2 col0">
                    1.80943
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow2_col1" class="data row2 col1">
                    -0.524478
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow2_col2" class="data row2 col2">
                    0.24831
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow2_col3" class="data row2 col3">
                    -1.01775
                
            </tr>
            
            <tr>
                
                <th id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810d" class="row_heading level3 row3">
                    3
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow3_col0" class="data row3 col0">
                    0.585044
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow3_col1" class="data row3 col1">
                    0.944626
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow3_col2" class="data row3 col2">
                    0.650761
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow3_col3" class="data row3 col3">
                    0.270653
                
            </tr>
            
            <tr>
                
                <th id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810d" class="row_heading level3 row4">
                    4
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow4_col0" class="data row4 col0">
                    1.93673
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow4_col1" class="data row4 col1">
                    -0.125753
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow4_col2" class="data row4 col2">
                    -0.0392093
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow4_col3" class="data row4 col3">
                    -0.0418587
                
            </tr>
            
            <tr>
                
                <th id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810d" class="row_heading level3 row5">
                    5
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow5_col0" class="data row5 col0">
                    -0.508527
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow5_col1" class="data row5 col1">
                    0.468058
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow5_col2" class="data row5 col2">
                    -0.475535
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow5_col3" class="data row5 col3">
                    -0.0566373
                
            </tr>
            
            <tr>
                
                <th id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810d" class="row_heading level3 row6">
                    6
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow6_col0" class="data row6 col0">
                    1.18967
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow6_col1" class="data row6 col1">
                    0.0861624
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow6_col2" class="data row6 col2">
                    0.509731
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow6_col3" class="data row6 col3">
                    0.107588
                
            </tr>
            
            <tr>
                
                <th id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810d" class="row_heading level3 row7">
                    7
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow7_col0" class="data row7 col0">
                    0.251497
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow7_col1" class="data row7 col1">
                    -2.65956
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow7_col2" class="data row7 col2">
                    0.803005
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow7_col3" class="data row7 col3">
                    -0.0121781
                
            </tr>
            
            <tr>
                
                <th id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810d" class="row_heading level3 row8">
                    8
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow8_col0" class="data row8 col0">
                    1.96226
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow8_col1" class="data row8 col1">
                    -1.22001
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow8_col2" class="data row8 col2">
                    -1.02514
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow8_col3" class="data row8 col3">
                    -0.922657
                
            </tr>
            
            <tr>
                
                <th id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810d" class="row_heading level3 row9">
                    9
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow9_col0" class="data row9 col0">
                    0.706176
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow9_col1" class="data row9 col1">
                    -1.28399
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow9_col2" class="data row9 col2">
                    0.323935
                
                <td id="T_ff6badd2_f2f8_11e7_a3ad_240a64de810drow9_col3" class="data row9 col3">
                    -1.03275
                
            </tr>
            
        </tbody>
        </table>
        




```python
# 按元素处理样式：style.applymap()

def color_neg_red(val):
    if val < 0:
        color = 'red'
    else:
        color = 'black'
    return('color:%s' % color)
df.style.applymap(color_neg_red)
# 创建样式方法，使得小于0的数变成红色
# style.applymap() → 自动调用其中的函数
```





        <style  type="text/css" >
        
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow0_col0 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow0_col1 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow0_col2 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow0_col3 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow1_col0 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow1_col1 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow1_col2 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow1_col3 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow2_col0 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow2_col1 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow2_col2 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow2_col3 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow3_col0 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow3_col1 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow3_col2 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow3_col3 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow4_col0 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow4_col1 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow4_col2 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow4_col3 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow5_col0 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow5_col1 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow5_col2 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow5_col3 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow6_col0 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow6_col1 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow6_col2 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow6_col3 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow7_col0 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow7_col1 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow7_col2 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow7_col3 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow8_col0 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow8_col1 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow8_col2 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow8_col3 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow9_col0 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow9_col1 {
            
                color: red;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow9_col2 {
            
                color: black;
            
            }
        
            #T_004436ae_f2f9_11e7_8c7b_240a64de810drow9_col3 {
            
                color: red;
            
            }
        
        </style>

        <table id="T_004436ae_f2f9_11e7_8c7b_240a64de810d" None>
        

        <thead>
            
            <tr>
                
                <th class="blank">
                
                <th class="col_heading level0 col0">a
                
                <th class="col_heading level0 col1">b
                
                <th class="col_heading level0 col2">c
                
                <th class="col_heading level0 col3">d
                
            </tr>
            
        </thead>
        <tbody>
            
            <tr>
                
                <th id="T_004436ae_f2f9_11e7_8c7b_240a64de810d" class="row_heading level3 row0">
                    0
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow0_col0" class="data row0 col0">
                    1.1215
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow0_col1" class="data row0 col1">
                    -1.38757
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow0_col2" class="data row0 col2">
                    -0.694214
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow0_col3" class="data row0 col3">
                    -0.887584
                
            </tr>
            
            <tr>
                
                <th id="T_004436ae_f2f9_11e7_8c7b_240a64de810d" class="row_heading level3 row1">
                    1
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow1_col0" class="data row1 col0">
                    0.254148
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow1_col1" class="data row1 col1">
                    -0.578241
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow1_col2" class="data row1 col2">
                    0.336016
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow1_col3" class="data row1 col3">
                    -2.05696
                
            </tr>
            
            <tr>
                
                <th id="T_004436ae_f2f9_11e7_8c7b_240a64de810d" class="row_heading level3 row2">
                    2
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow2_col0" class="data row2 col0">
                    1.80943
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow2_col1" class="data row2 col1">
                    -0.524478
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow2_col2" class="data row2 col2">
                    0.24831
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow2_col3" class="data row2 col3">
                    -1.01775
                
            </tr>
            
            <tr>
                
                <th id="T_004436ae_f2f9_11e7_8c7b_240a64de810d" class="row_heading level3 row3">
                    3
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow3_col0" class="data row3 col0">
                    0.585044
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow3_col1" class="data row3 col1">
                    0.944626
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow3_col2" class="data row3 col2">
                    0.650761
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow3_col3" class="data row3 col3">
                    0.270653
                
            </tr>
            
            <tr>
                
                <th id="T_004436ae_f2f9_11e7_8c7b_240a64de810d" class="row_heading level3 row4">
                    4
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow4_col0" class="data row4 col0">
                    1.93673
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow4_col1" class="data row4 col1">
                    -0.125753
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow4_col2" class="data row4 col2">
                    -0.0392093
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow4_col3" class="data row4 col3">
                    -0.0418587
                
            </tr>
            
            <tr>
                
                <th id="T_004436ae_f2f9_11e7_8c7b_240a64de810d" class="row_heading level3 row5">
                    5
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow5_col0" class="data row5 col0">
                    -0.508527
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow5_col1" class="data row5 col1">
                    0.468058
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow5_col2" class="data row5 col2">
                    -0.475535
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow5_col3" class="data row5 col3">
                    -0.0566373
                
            </tr>
            
            <tr>
                
                <th id="T_004436ae_f2f9_11e7_8c7b_240a64de810d" class="row_heading level3 row6">
                    6
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow6_col0" class="data row6 col0">
                    1.18967
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow6_col1" class="data row6 col1">
                    0.0861624
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow6_col2" class="data row6 col2">
                    0.509731
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow6_col3" class="data row6 col3">
                    0.107588
                
            </tr>
            
            <tr>
                
                <th id="T_004436ae_f2f9_11e7_8c7b_240a64de810d" class="row_heading level3 row7">
                    7
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow7_col0" class="data row7 col0">
                    0.251497
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow7_col1" class="data row7 col1">
                    -2.65956
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow7_col2" class="data row7 col2">
                    0.803005
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow7_col3" class="data row7 col3">
                    -0.0121781
                
            </tr>
            
            <tr>
                
                <th id="T_004436ae_f2f9_11e7_8c7b_240a64de810d" class="row_heading level3 row8">
                    8
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow8_col0" class="data row8 col0">
                    1.96226
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow8_col1" class="data row8 col1">
                    -1.22001
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow8_col2" class="data row8 col2">
                    -1.02514
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow8_col3" class="data row8 col3">
                    -0.922657
                
            </tr>
            
            <tr>
                
                <th id="T_004436ae_f2f9_11e7_8c7b_240a64de810d" class="row_heading level3 row9">
                    9
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow9_col0" class="data row9 col0">
                    0.706176
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow9_col1" class="data row9 col1">
                    -1.28399
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow9_col2" class="data row9 col2">
                    0.323935
                
                <td id="T_004436ae_f2f9_11e7_8c7b_240a64de810drow9_col3" class="data row9 col3">
                    -1.03275
                
            </tr>
            
        </tbody>
        </table>
        




```python
# 按行/列处理样式：style.apply()

def highlight_max(s):
    is_max = s == s.max()
    #print(is_max)
    lst = []
    for v in is_max:
        if v:
            lst.append('background-color: yellow')
        else:
            lst.append('')
    return(lst)
df.style.apply(highlight_max, axis = 0, subset = ['b','c'])
# 创建样式方法，每列最大值填充黄色
# axis：0为列，1为行，默认为0
# subset：索引
```





        <style  type="text/css" >
        
        
            #T_0104ca62_f2f9_11e7_ab63_240a64de810drow3_col1 {
            
                background-color:  yellow;
            
            }
        
            #T_0104ca62_f2f9_11e7_ab63_240a64de810drow7_col2 {
            
                background-color:  yellow;
            
            }
        
        </style>

        <table id="T_0104ca62_f2f9_11e7_ab63_240a64de810d" None>
        

        <thead>
            
            <tr>
                
                <th class="blank">
                
                <th class="col_heading level0 col0">a
                
                <th class="col_heading level0 col1">b
                
                <th class="col_heading level0 col2">c
                
                <th class="col_heading level0 col3">d
                
            </tr>
            
        </thead>
        <tbody>
            
            <tr>
                
                <th id="T_0104ca62_f2f9_11e7_ab63_240a64de810d" class="row_heading level3 row0">
                    0
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow0_col0" class="data row0 col0">
                    1.1215
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow0_col1" class="data row0 col1">
                    -1.38757
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow0_col2" class="data row0 col2">
                    -0.694214
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow0_col3" class="data row0 col3">
                    -0.887584
                
            </tr>
            
            <tr>
                
                <th id="T_0104ca62_f2f9_11e7_ab63_240a64de810d" class="row_heading level3 row1">
                    1
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow1_col0" class="data row1 col0">
                    0.254148
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow1_col1" class="data row1 col1">
                    -0.578241
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow1_col2" class="data row1 col2">
                    0.336016
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow1_col3" class="data row1 col3">
                    -2.05696
                
            </tr>
            
            <tr>
                
                <th id="T_0104ca62_f2f9_11e7_ab63_240a64de810d" class="row_heading level3 row2">
                    2
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow2_col0" class="data row2 col0">
                    1.80943
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow2_col1" class="data row2 col1">
                    -0.524478
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow2_col2" class="data row2 col2">
                    0.24831
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow2_col3" class="data row2 col3">
                    -1.01775
                
            </tr>
            
            <tr>
                
                <th id="T_0104ca62_f2f9_11e7_ab63_240a64de810d" class="row_heading level3 row3">
                    3
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow3_col0" class="data row3 col0">
                    0.585044
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow3_col1" class="data row3 col1">
                    0.944626
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow3_col2" class="data row3 col2">
                    0.650761
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow3_col3" class="data row3 col3">
                    0.270653
                
            </tr>
            
            <tr>
                
                <th id="T_0104ca62_f2f9_11e7_ab63_240a64de810d" class="row_heading level3 row4">
                    4
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow4_col0" class="data row4 col0">
                    1.93673
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow4_col1" class="data row4 col1">
                    -0.125753
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow4_col2" class="data row4 col2">
                    -0.0392093
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow4_col3" class="data row4 col3">
                    -0.0418587
                
            </tr>
            
            <tr>
                
                <th id="T_0104ca62_f2f9_11e7_ab63_240a64de810d" class="row_heading level3 row5">
                    5
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow5_col0" class="data row5 col0">
                    -0.508527
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow5_col1" class="data row5 col1">
                    0.468058
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow5_col2" class="data row5 col2">
                    -0.475535
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow5_col3" class="data row5 col3">
                    -0.0566373
                
            </tr>
            
            <tr>
                
                <th id="T_0104ca62_f2f9_11e7_ab63_240a64de810d" class="row_heading level3 row6">
                    6
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow6_col0" class="data row6 col0">
                    1.18967
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow6_col1" class="data row6 col1">
                    0.0861624
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow6_col2" class="data row6 col2">
                    0.509731
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow6_col3" class="data row6 col3">
                    0.107588
                
            </tr>
            
            <tr>
                
                <th id="T_0104ca62_f2f9_11e7_ab63_240a64de810d" class="row_heading level3 row7">
                    7
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow7_col0" class="data row7 col0">
                    0.251497
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow7_col1" class="data row7 col1">
                    -2.65956
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow7_col2" class="data row7 col2">
                    0.803005
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow7_col3" class="data row7 col3">
                    -0.0121781
                
            </tr>
            
            <tr>
                
                <th id="T_0104ca62_f2f9_11e7_ab63_240a64de810d" class="row_heading level3 row8">
                    8
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow8_col0" class="data row8 col0">
                    1.96226
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow8_col1" class="data row8 col1">
                    -1.22001
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow8_col2" class="data row8 col2">
                    -1.02514
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow8_col3" class="data row8 col3">
                    -0.922657
                
            </tr>
            
            <tr>
                
                <th id="T_0104ca62_f2f9_11e7_ab63_240a64de810d" class="row_heading level3 row9">
                    9
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow9_col0" class="data row9 col0">
                    0.706176
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow9_col1" class="data row9 col1">
                    -1.28399
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow9_col2" class="data row9 col2">
                    0.323935
                
                <td id="T_0104ca62_f2f9_11e7_ab63_240a64de810drow9_col3" class="data row9 col3">
                    -1.03275
                
            </tr>
            
        </tbody>
        </table>
        




```python
# 样式索引、切片

df.style.apply(highlight_max, axis = 1, 
               subset = pd.IndexSlice[2:5,['b', 'd']])
# 通过pd.IndexSlice[]调用切片
# 也可：df[2:5].style.apply(highlight_max, subset = ['b', 'd']) → 先索引行再做样式
```





        <style  type="text/css" >
        
        
            #T_01e5429a_f2f9_11e7_bfc9_240a64de810drow2_col1 {
            
                background-color:  yellow;
            
            }
        
            #T_01e5429a_f2f9_11e7_bfc9_240a64de810drow3_col1 {
            
                background-color:  yellow;
            
            }
        
            #T_01e5429a_f2f9_11e7_bfc9_240a64de810drow4_col3 {
            
                background-color:  yellow;
            
            }
        
            #T_01e5429a_f2f9_11e7_bfc9_240a64de810drow5_col1 {
            
                background-color:  yellow;
            
            }
        
        </style>

        <table id="T_01e5429a_f2f9_11e7_bfc9_240a64de810d" None>
        

        <thead>
            
            <tr>
                
                <th class="blank">
                
                <th class="col_heading level0 col0">a
                
                <th class="col_heading level0 col1">b
                
                <th class="col_heading level0 col2">c
                
                <th class="col_heading level0 col3">d
                
            </tr>
            
        </thead>
        <tbody>
            
            <tr>
                
                <th id="T_01e5429a_f2f9_11e7_bfc9_240a64de810d" class="row_heading level3 row0">
                    0
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow0_col0" class="data row0 col0">
                    1.1215
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow0_col1" class="data row0 col1">
                    -1.38757
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow0_col2" class="data row0 col2">
                    -0.694214
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow0_col3" class="data row0 col3">
                    -0.887584
                
            </tr>
            
            <tr>
                
                <th id="T_01e5429a_f2f9_11e7_bfc9_240a64de810d" class="row_heading level3 row1">
                    1
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow1_col0" class="data row1 col0">
                    0.254148
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow1_col1" class="data row1 col1">
                    -0.578241
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow1_col2" class="data row1 col2">
                    0.336016
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow1_col3" class="data row1 col3">
                    -2.05696
                
            </tr>
            
            <tr>
                
                <th id="T_01e5429a_f2f9_11e7_bfc9_240a64de810d" class="row_heading level3 row2">
                    2
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow2_col0" class="data row2 col0">
                    1.80943
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow2_col1" class="data row2 col1">
                    -0.524478
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow2_col2" class="data row2 col2">
                    0.24831
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow2_col3" class="data row2 col3">
                    -1.01775
                
            </tr>
            
            <tr>
                
                <th id="T_01e5429a_f2f9_11e7_bfc9_240a64de810d" class="row_heading level3 row3">
                    3
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow3_col0" class="data row3 col0">
                    0.585044
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow3_col1" class="data row3 col1">
                    0.944626
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow3_col2" class="data row3 col2">
                    0.650761
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow3_col3" class="data row3 col3">
                    0.270653
                
            </tr>
            
            <tr>
                
                <th id="T_01e5429a_f2f9_11e7_bfc9_240a64de810d" class="row_heading level3 row4">
                    4
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow4_col0" class="data row4 col0">
                    1.93673
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow4_col1" class="data row4 col1">
                    -0.125753
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow4_col2" class="data row4 col2">
                    -0.0392093
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow4_col3" class="data row4 col3">
                    -0.0418587
                
            </tr>
            
            <tr>
                
                <th id="T_01e5429a_f2f9_11e7_bfc9_240a64de810d" class="row_heading level3 row5">
                    5
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow5_col0" class="data row5 col0">
                    -0.508527
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow5_col1" class="data row5 col1">
                    0.468058
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow5_col2" class="data row5 col2">
                    -0.475535
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow5_col3" class="data row5 col3">
                    -0.0566373
                
            </tr>
            
            <tr>
                
                <th id="T_01e5429a_f2f9_11e7_bfc9_240a64de810d" class="row_heading level3 row6">
                    6
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow6_col0" class="data row6 col0">
                    1.18967
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow6_col1" class="data row6 col1">
                    0.0861624
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow6_col2" class="data row6 col2">
                    0.509731
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow6_col3" class="data row6 col3">
                    0.107588
                
            </tr>
            
            <tr>
                
                <th id="T_01e5429a_f2f9_11e7_bfc9_240a64de810d" class="row_heading level3 row7">
                    7
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow7_col0" class="data row7 col0">
                    0.251497
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow7_col1" class="data row7 col1">
                    -2.65956
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow7_col2" class="data row7 col2">
                    0.803005
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow7_col3" class="data row7 col3">
                    -0.0121781
                
            </tr>
            
            <tr>
                
                <th id="T_01e5429a_f2f9_11e7_bfc9_240a64de810d" class="row_heading level3 row8">
                    8
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow8_col0" class="data row8 col0">
                    1.96226
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow8_col1" class="data row8 col1">
                    -1.22001
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow8_col2" class="data row8 col2">
                    -1.02514
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow8_col3" class="data row8 col3">
                    -0.922657
                
            </tr>
            
            <tr>
                
                <th id="T_01e5429a_f2f9_11e7_bfc9_240a64de810d" class="row_heading level3 row9">
                    9
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow9_col0" class="data row9 col0">
                    0.706176
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow9_col1" class="data row9 col1">
                    -1.28399
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow9_col2" class="data row9 col2">
                    0.323935
                
                <td id="T_01e5429a_f2f9_11e7_bfc9_240a64de810drow9_col3" class="data row9 col3">
                    -1.03275
                
            </tr>
            
        </tbody>
        </table>
        




```python
'''
【课程3.14】  表格显示控制

df.style.format()
 
'''
```


```python
# 按照百分数显示

df = pd.DataFrame(np.random.randn(10,4),columns=['a','b','c','d'])
print(df.head())
df.head().style.format("{:.2%}")
```

              a         b         c         d
    0 -1.458644 -0.655620  0.134962  0.487259
    1  0.921098  0.631805  0.943667 -0.669659
    2  1.162486 -1.362738  0.015851  0.720793
    3  1.250515  2.166381  0.222424  1.696663
    4 -0.655765 -0.768403 -1.802734  0.087619
    





        <style  type="text/css" >
        
        
        </style>

        <table id="T_02a7f934_f2f9_11e7_8581_240a64de810d" None>
        

        <thead>
            
            <tr>
                
                <th class="blank">
                
                <th class="col_heading level0 col0">a
                
                <th class="col_heading level0 col1">b
                
                <th class="col_heading level0 col2">c
                
                <th class="col_heading level0 col3">d
                
            </tr>
            
        </thead>
        <tbody>
            
            <tr>
                
                <th id="T_02a7f934_f2f9_11e7_8581_240a64de810d" class="row_heading level3 row0">
                    0
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow0_col0" class="data row0 col0">
                    -145.86%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow0_col1" class="data row0 col1">
                    -65.56%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow0_col2" class="data row0 col2">
                    13.50%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow0_col3" class="data row0 col3">
                    48.73%
                
            </tr>
            
            <tr>
                
                <th id="T_02a7f934_f2f9_11e7_8581_240a64de810d" class="row_heading level3 row1">
                    1
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow1_col0" class="data row1 col0">
                    92.11%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow1_col1" class="data row1 col1">
                    63.18%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow1_col2" class="data row1 col2">
                    94.37%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow1_col3" class="data row1 col3">
                    -66.97%
                
            </tr>
            
            <tr>
                
                <th id="T_02a7f934_f2f9_11e7_8581_240a64de810d" class="row_heading level3 row2">
                    2
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow2_col0" class="data row2 col0">
                    116.25%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow2_col1" class="data row2 col1">
                    -136.27%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow2_col2" class="data row2 col2">
                    1.59%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow2_col3" class="data row2 col3">
                    72.08%
                
            </tr>
            
            <tr>
                
                <th id="T_02a7f934_f2f9_11e7_8581_240a64de810d" class="row_heading level3 row3">
                    3
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow3_col0" class="data row3 col0">
                    125.05%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow3_col1" class="data row3 col1">
                    216.64%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow3_col2" class="data row3 col2">
                    22.24%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow3_col3" class="data row3 col3">
                    169.67%
                
            </tr>
            
            <tr>
                
                <th id="T_02a7f934_f2f9_11e7_8581_240a64de810d" class="row_heading level3 row4">
                    4
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow4_col0" class="data row4 col0">
                    -65.58%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow4_col1" class="data row4 col1">
                    -76.84%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow4_col2" class="data row4 col2">
                    -180.27%
                
                <td id="T_02a7f934_f2f9_11e7_8581_240a64de810drow4_col3" class="data row4 col3">
                    8.76%
                
            </tr>
            
        </tbody>
        </table>
        




```python
# 显示小数点数

df.head().style.format("{:.4f}")
```





        <style  type="text/css" >
        
        
        </style>

        <table id="T_03b7233a_f2f9_11e7_9343_240a64de810d" None>
        

        <thead>
            
            <tr>
                
                <th class="blank">
                
                <th class="col_heading level0 col0">a
                
                <th class="col_heading level0 col1">b
                
                <th class="col_heading level0 col2">c
                
                <th class="col_heading level0 col3">d
                
            </tr>
            
        </thead>
        <tbody>
            
            <tr>
                
                <th id="T_03b7233a_f2f9_11e7_9343_240a64de810d" class="row_heading level3 row0">
                    0
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow0_col0" class="data row0 col0">
                    -1.4586
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow0_col1" class="data row0 col1">
                    -0.6556
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow0_col2" class="data row0 col2">
                    0.1350
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow0_col3" class="data row0 col3">
                    0.4873
                
            </tr>
            
            <tr>
                
                <th id="T_03b7233a_f2f9_11e7_9343_240a64de810d" class="row_heading level3 row1">
                    1
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow1_col0" class="data row1 col0">
                    0.9211
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow1_col1" class="data row1 col1">
                    0.6318
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow1_col2" class="data row1 col2">
                    0.9437
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow1_col3" class="data row1 col3">
                    -0.6697
                
            </tr>
            
            <tr>
                
                <th id="T_03b7233a_f2f9_11e7_9343_240a64de810d" class="row_heading level3 row2">
                    2
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow2_col0" class="data row2 col0">
                    1.1625
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow2_col1" class="data row2 col1">
                    -1.3627
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow2_col2" class="data row2 col2">
                    0.0159
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow2_col3" class="data row2 col3">
                    0.7208
                
            </tr>
            
            <tr>
                
                <th id="T_03b7233a_f2f9_11e7_9343_240a64de810d" class="row_heading level3 row3">
                    3
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow3_col0" class="data row3 col0">
                    1.2505
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow3_col1" class="data row3 col1">
                    2.1664
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow3_col2" class="data row3 col2">
                    0.2224
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow3_col3" class="data row3 col3">
                    1.6967
                
            </tr>
            
            <tr>
                
                <th id="T_03b7233a_f2f9_11e7_9343_240a64de810d" class="row_heading level3 row4">
                    4
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow4_col0" class="data row4 col0">
                    -0.6558
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow4_col1" class="data row4 col1">
                    -0.7684
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow4_col2" class="data row4 col2">
                    -1.8027
                
                <td id="T_03b7233a_f2f9_11e7_9343_240a64de810drow4_col3" class="data row4 col3">
                    0.0876
                
            </tr>
            
        </tbody>
        </table>
        




```python
# 显示正负数

df.head().style.format("{:+.2f}")
```





        <style  type="text/css" >
        
        
        </style>

        <table id="T_04642ea4_f2f9_11e7_b387_240a64de810d" None>
        

        <thead>
            
            <tr>
                
                <th class="blank">
                
                <th class="col_heading level0 col0">a
                
                <th class="col_heading level0 col1">b
                
                <th class="col_heading level0 col2">c
                
                <th class="col_heading level0 col3">d
                
            </tr>
            
        </thead>
        <tbody>
            
            <tr>
                
                <th id="T_04642ea4_f2f9_11e7_b387_240a64de810d" class="row_heading level3 row0">
                    0
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow0_col0" class="data row0 col0">
                    -1.46
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow0_col1" class="data row0 col1">
                    -0.66
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow0_col2" class="data row0 col2">
                    +0.13
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow0_col3" class="data row0 col3">
                    +0.49
                
            </tr>
            
            <tr>
                
                <th id="T_04642ea4_f2f9_11e7_b387_240a64de810d" class="row_heading level3 row1">
                    1
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow1_col0" class="data row1 col0">
                    +0.92
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow1_col1" class="data row1 col1">
                    +0.63
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow1_col2" class="data row1 col2">
                    +0.94
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow1_col3" class="data row1 col3">
                    -0.67
                
            </tr>
            
            <tr>
                
                <th id="T_04642ea4_f2f9_11e7_b387_240a64de810d" class="row_heading level3 row2">
                    2
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow2_col0" class="data row2 col0">
                    +1.16
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow2_col1" class="data row2 col1">
                    -1.36
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow2_col2" class="data row2 col2">
                    +0.02
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow2_col3" class="data row2 col3">
                    +0.72
                
            </tr>
            
            <tr>
                
                <th id="T_04642ea4_f2f9_11e7_b387_240a64de810d" class="row_heading level3 row3">
                    3
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow3_col0" class="data row3 col0">
                    +1.25
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow3_col1" class="data row3 col1">
                    +2.17
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow3_col2" class="data row3 col2">
                    +0.22
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow3_col3" class="data row3 col3">
                    +1.70
                
            </tr>
            
            <tr>
                
                <th id="T_04642ea4_f2f9_11e7_b387_240a64de810d" class="row_heading level3 row4">
                    4
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow4_col0" class="data row4 col0">
                    -0.66
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow4_col1" class="data row4 col1">
                    -0.77
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow4_col2" class="data row4 col2">
                    -1.80
                
                <td id="T_04642ea4_f2f9_11e7_b387_240a64de810drow4_col3" class="data row4 col3">
                    +0.09
                
            </tr>
            
        </tbody>
        </table>
        




```python
# 分列显示

df.head().style.format({'b':"{:.2%}", 'c':"{:+.3f}", 'd':"{:.3f}"})
```





        <style  type="text/css" >
        
        
        </style>

        <table id="T_053c906e_f2f9_11e7_b49d_240a64de810d" None>
        

        <thead>
            
            <tr>
                
                <th class="blank">
                
                <th class="col_heading level0 col0">a
                
                <th class="col_heading level0 col1">b
                
                <th class="col_heading level0 col2">c
                
                <th class="col_heading level0 col3">d
                
            </tr>
            
        </thead>
        <tbody>
            
            <tr>
                
                <th id="T_053c906e_f2f9_11e7_b49d_240a64de810d" class="row_heading level3 row0">
                    0
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow0_col0" class="data row0 col0">
                    -1.45864
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow0_col1" class="data row0 col1">
                    -65.56%
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow0_col2" class="data row0 col2">
                    +0.135
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow0_col3" class="data row0 col3">
                    0.487
                
            </tr>
            
            <tr>
                
                <th id="T_053c906e_f2f9_11e7_b49d_240a64de810d" class="row_heading level3 row1">
                    1
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow1_col0" class="data row1 col0">
                    0.921098
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow1_col1" class="data row1 col1">
                    63.18%
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow1_col2" class="data row1 col2">
                    +0.944
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow1_col3" class="data row1 col3">
                    -0.670
                
            </tr>
            
            <tr>
                
                <th id="T_053c906e_f2f9_11e7_b49d_240a64de810d" class="row_heading level3 row2">
                    2
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow2_col0" class="data row2 col0">
                    1.16249
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow2_col1" class="data row2 col1">
                    -136.27%
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow2_col2" class="data row2 col2">
                    +0.016
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow2_col3" class="data row2 col3">
                    0.721
                
            </tr>
            
            <tr>
                
                <th id="T_053c906e_f2f9_11e7_b49d_240a64de810d" class="row_heading level3 row3">
                    3
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow3_col0" class="data row3 col0">
                    1.25052
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow3_col1" class="data row3 col1">
                    216.64%
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow3_col2" class="data row3 col2">
                    +0.222
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow3_col3" class="data row3 col3">
                    1.697
                
            </tr>
            
            <tr>
                
                <th id="T_053c906e_f2f9_11e7_b49d_240a64de810d" class="row_heading level3 row4">
                    4
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow4_col0" class="data row4 col0">
                    -0.655765
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow4_col1" class="data row4 col1">
                    -76.84%
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow4_col2" class="data row4 col2">
                    -1.803
                
                <td id="T_053c906e_f2f9_11e7_b49d_240a64de810drow4_col3" class="data row4 col3">
                    0.088
                
            </tr>
            
        </tbody>
        </table>
        




```python
'''
【课程3.15】  表格样式调用

Styler内置样式调用
 
'''
```


```python
# 定位空值

df = pd.DataFrame(np.random.rand(5,4),columns = list('ABCD'))
df['A'][2] = np.nan
df.style.highlight_null(null_color='red')
```





        <style  type="text/css" >
        
        
            #T_0603dafa_f2f9_11e7_b220_240a64de810drow2_col0 {
            
                background-color:  red;
            
            }
        
        </style>

        <table id="T_0603dafa_f2f9_11e7_b220_240a64de810d" None>
        

        <thead>
            
            <tr>
                
                <th class="blank">
                
                <th class="col_heading level0 col0">A
                
                <th class="col_heading level0 col1">B
                
                <th class="col_heading level0 col2">C
                
                <th class="col_heading level0 col3">D
                
            </tr>
            
        </thead>
        <tbody>
            
            <tr>
                
                <th id="T_0603dafa_f2f9_11e7_b220_240a64de810d" class="row_heading level3 row0">
                    0
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow0_col0" class="data row0 col0">
                    0.714752
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow0_col1" class="data row0 col1">
                    0.244419
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow0_col2" class="data row0 col2">
                    0.757845
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow0_col3" class="data row0 col3">
                    0.166515
                
            </tr>
            
            <tr>
                
                <th id="T_0603dafa_f2f9_11e7_b220_240a64de810d" class="row_heading level3 row1">
                    1
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow1_col0" class="data row1 col0">
                    0.299022
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow1_col1" class="data row1 col1">
                    0.669106
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow1_col2" class="data row1 col2">
                    0.866447
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow1_col3" class="data row1 col3">
                    0.798063
                
            </tr>
            
            <tr>
                
                <th id="T_0603dafa_f2f9_11e7_b220_240a64de810d" class="row_heading level3 row2">
                    2
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow2_col0" class="data row2 col0">
                    nan
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow2_col1" class="data row2 col1">
                    0.333066
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow2_col2" class="data row2 col2">
                    0.552096
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow2_col3" class="data row2 col3">
                    0.625966
                
            </tr>
            
            <tr>
                
                <th id="T_0603dafa_f2f9_11e7_b220_240a64de810d" class="row_heading level3 row3">
                    3
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow3_col0" class="data row3 col0">
                    0.745323
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow3_col1" class="data row3 col1">
                    0.284294
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow3_col2" class="data row3 col2">
                    0.961832
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow3_col3" class="data row3 col3">
                    0.84158
                
            </tr>
            
            <tr>
                
                <th id="T_0603dafa_f2f9_11e7_b220_240a64de810d" class="row_heading level3 row4">
                    4
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow4_col0" class="data row4 col0">
                    0.373925
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow4_col1" class="data row4 col1">
                    0.314152
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow4_col2" class="data row4 col2">
                    0.61255
                
                <td id="T_0603dafa_f2f9_11e7_b220_240a64de810drow4_col3" class="data row4 col3">
                    0.173583
                
            </tr>
            
        </tbody>
        </table>
        




```python
# 色彩映射

df = pd.DataFrame(np.random.rand(10,4),columns = list('ABCD'))
df.style.background_gradient(cmap='Greens',axis =1,low=0,high=1)
# cmap：颜色
# axis：映射参考，0为行，1以列
```





        <style  type="text/css" >
        
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow0_col0 {
            
                background-color:  #e5f5e0;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow0_col1 {
            
                background-color:  #a9dca3;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow0_col2 {
            
                background-color:  #f7fcf5;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow0_col3 {
            
                background-color:  #73c476;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow1_col0 {
            
                background-color:  #8dd08a;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow1_col1 {
            
                background-color:  #d2edcc;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow1_col2 {
            
                background-color:  #73c476;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow1_col3 {
            
                background-color:  #f7fcf5;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow2_col0 {
            
                background-color:  #9bd696;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow2_col1 {
            
                background-color:  #f7fcf5;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow2_col2 {
            
                background-color:  #75c477;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow2_col3 {
            
                background-color:  #90d18d;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow3_col0 {
            
                background-color:  #73c476;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow3_col1 {
            
                background-color:  #f7fcf5;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow3_col2 {
            
                background-color:  #c1e6ba;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow3_col3 {
            
                background-color:  #e7f6e2;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow4_col0 {
            
                background-color:  #73c476;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow4_col1 {
            
                background-color:  #e7f6e2;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow4_col2 {
            
                background-color:  #c0e6b9;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow4_col3 {
            
                background-color:  #f7fcf5;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow5_col0 {
            
                background-color:  #f7fcf5;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow5_col1 {
            
                background-color:  #73c476;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow5_col2 {
            
                background-color:  #f5fbf2;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow5_col3 {
            
                background-color:  #94d390;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow6_col0 {
            
                background-color:  #73c476;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow6_col1 {
            
                background-color:  #a9dca3;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow6_col2 {
            
                background-color:  #c3e7bc;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow6_col3 {
            
                background-color:  #f7fcf5;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow7_col0 {
            
                background-color:  #eff9ec;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow7_col1 {
            
                background-color:  #aedea7;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow7_col2 {
            
                background-color:  #73c476;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow7_col3 {
            
                background-color:  #f7fcf5;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow8_col0 {
            
                background-color:  #f7fcf5;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow8_col1 {
            
                background-color:  #73c476;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow8_col2 {
            
                background-color:  #afdfa8;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow8_col3 {
            
                background-color:  #acdea6;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow9_col0 {
            
                background-color:  #f7fcf5;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow9_col1 {
            
                background-color:  #73c476;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow9_col2 {
            
                background-color:  #eef8ea;
            
            }
        
            #T_06c04fee_f2f9_11e7_aba0_240a64de810drow9_col3 {
            
                background-color:  #e8f6e3;
            
            }
        
        </style>

        <table id="T_06c04fee_f2f9_11e7_aba0_240a64de810d" None>
        

        <thead>
            
            <tr>
                
                <th class="blank">
                
                <th class="col_heading level0 col0">A
                
                <th class="col_heading level0 col1">B
                
                <th class="col_heading level0 col2">C
                
                <th class="col_heading level0 col3">D
                
            </tr>
            
        </thead>
        <tbody>
            
            <tr>
                
                <th id="T_06c04fee_f2f9_11e7_aba0_240a64de810d" class="row_heading level3 row0">
                    0
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow0_col0" class="data row0 col0">
                    0.35589
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow0_col1" class="data row0 col1">
                    0.705106
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow0_col2" class="data row0 col2">
                    0.156272
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow0_col3" class="data row0 col3">
                    0.94045
                
            </tr>
            
            <tr>
                
                <th id="T_06c04fee_f2f9_11e7_aba0_240a64de810d" class="row_heading level3 row1">
                    1
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow1_col0" class="data row1 col0">
                    0.782459
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow1_col1" class="data row1 col1">
                    0.475351
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow1_col2" class="data row1 col2">
                    0.874163
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow1_col3" class="data row1 col3">
                    0.198793
                
            </tr>
            
            <tr>
                
                <th id="T_06c04fee_f2f9_11e7_aba0_240a64de810d" class="row_heading level3 row2">
                    2
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow2_col0" class="data row2 col0">
                    0.678382
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow2_col1" class="data row2 col1">
                    0.0927048
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow2_col2" class="data row2 col2">
                    0.83857
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow2_col3" class="data row2 col3">
                    0.723829
                
            </tr>
            
            <tr>
                
                <th id="T_06c04fee_f2f9_11e7_aba0_240a64de810d" class="row_heading level3 row3">
                    3
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow3_col0" class="data row3 col0">
                    0.686543
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow3_col1" class="data row3 col1">
                    0.210492
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow3_col2" class="data row3 col2">
                    0.467397
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow3_col3" class="data row3 col3">
                    0.321684
                
            </tr>
            
            <tr>
                
                <th id="T_06c04fee_f2f9_11e7_aba0_240a64de810d" class="row_heading level3 row4">
                    4
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow4_col0" class="data row4 col0">
                    0.920856
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow4_col1" class="data row4 col1">
                    0.507327
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow4_col2" class="data row4 col2">
                    0.678301
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow4_col3" class="data row4 col3">
                    0.383717
                
            </tr>
            
            <tr>
                
                <th id="T_06c04fee_f2f9_11e7_aba0_240a64de810d" class="row_heading level3 row5">
                    5
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow5_col0" class="data row5 col0">
                    0.138504
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow5_col1" class="data row5 col1">
                    0.784922
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow5_col2" class="data row5 col2">
                    0.16161
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow5_col3" class="data row5 col3">
                    0.670962
                
            </tr>
            
            <tr>
                
                <th id="T_06c04fee_f2f9_11e7_aba0_240a64de810d" class="row_heading level3 row6">
                    6
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow6_col0" class="data row6 col0">
                    0.999699
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow6_col1" class="data row6 col1">
                    0.808968
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow6_col2" class="data row6 col2">
                    0.700415
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow6_col3" class="data row6 col3">
                    0.366371
                
            </tr>
            
            <tr>
                
                <th id="T_06c04fee_f2f9_11e7_aba0_240a64de810d" class="row_heading level3 row7">
                    7
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow7_col0" class="data row7 col0">
                    0.116142
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow7_col1" class="data row7 col1">
                    0.568436
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow7_col2" class="data row7 col2">
                    0.842027
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow7_col3" class="data row7 col3">
                    0.0226978
                
            </tr>
            
            <tr>
                
                <th id="T_06c04fee_f2f9_11e7_aba0_240a64de810d" class="row_heading level3 row8">
                    8
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow8_col0" class="data row8 col0">
                    0.0213556
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow8_col1" class="data row8 col1">
                    0.865117
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow8_col2" class="data row8 col2">
                    0.57514
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow8_col3" class="data row8 col3">
                    0.592521
                
            </tr>
            
            <tr>
                
                <th id="T_06c04fee_f2f9_11e7_aba0_240a64de810d" class="row_heading level3 row9">
                    9
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow9_col0" class="data row9 col0">
                    0.0454253
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow9_col1" class="data row9 col1">
                    0.884987
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow9_col2" class="data row9 col2">
                    0.154658
                
                <td id="T_06c04fee_f2f9_11e7_aba0_240a64de810drow9_col3" class="data row9 col3">
                    0.227973
                
            </tr>
            
        </tbody>
        </table>
        




```python
# 条形图

df = pd.DataFrame(np.random.rand(10,4),columns = list('ABCD'))
df.style.bar(subset=['A', 'B'], color='#d65f5f', width=100)
# width：最长长度在格子的占比
```





        <style  type="text/css" >
        
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow0_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 31.133706771146144%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow0_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 100.0%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow1_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 94.5026674204524%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow1_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 68.94723774983602%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow2_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 99.99999999999999%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow2_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 83.10037919419648%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow3_col0 {
            
                width:  10em;
            
                 height:  80%;
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow3_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 75.27604676187504%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow4_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 88.36565326972516%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow4_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 67.81286959276436%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow5_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 81.62965518202888%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow5_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 33.37909161873769%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow6_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 32.933658596540035%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow6_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 20.098325885802932%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow7_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 75.7679924265326%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow7_col1 {
            
                width:  10em;
            
                 height:  80%;
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow8_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 50.75230928415844%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow8_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 75.78536160751887%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow9_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 66.54120707047383%, transparent 0%);
            
            }
        
            #T_077c76be_f2f9_11e7_9818_240a64de810drow9_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 75.71107245148563%, transparent 0%);
            
            }
        
        </style>

        <table id="T_077c76be_f2f9_11e7_9818_240a64de810d" None>
        

        <thead>
            
            <tr>
                
                <th class="blank">
                
                <th class="col_heading level0 col0">A
                
                <th class="col_heading level0 col1">B
                
                <th class="col_heading level0 col2">C
                
                <th class="col_heading level0 col3">D
                
            </tr>
            
        </thead>
        <tbody>
            
            <tr>
                
                <th id="T_077c76be_f2f9_11e7_9818_240a64de810d" class="row_heading level3 row0">
                    0
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow0_col0" class="data row0 col0">
                    0.432267
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow0_col1" class="data row0 col1">
                    0.92718
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow0_col2" class="data row0 col2">
                    0.28735
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow0_col3" class="data row0 col3">
                    0.641502
                
            </tr>
            
            <tr>
                
                <th id="T_077c76be_f2f9_11e7_9818_240a64de810d" class="row_heading level3 row1">
                    1
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow1_col0" class="data row1 col0">
                    0.839107
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow1_col1" class="data row1 col1">
                    0.672681
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow1_col2" class="data row1 col2">
                    0.0782057
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow1_col3" class="data row1 col3">
                    0.247411
                
            </tr>
            
            <tr>
                
                <th id="T_077c76be_f2f9_11e7_9818_240a64de810d" class="row_heading level3 row2">
                    2
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow2_col0" class="data row2 col0">
                    0.874401
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow2_col1" class="data row2 col1">
                    0.788676
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow2_col2" class="data row2 col2">
                    0.496212
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow2_col3" class="data row2 col3">
                    0.253429
                
            </tr>
            
            <tr>
                
                <th id="T_077c76be_f2f9_11e7_9818_240a64de810d" class="row_heading level3 row3">
                    3
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow3_col0" class="data row3 col0">
                    0.232383
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow3_col1" class="data row3 col1">
                    0.72455
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow3_col2" class="data row3 col2">
                    0.75625
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow3_col3" class="data row3 col3">
                    0.230091
                
            </tr>
            
            <tr>
                
                <th id="T_077c76be_f2f9_11e7_9818_240a64de810d" class="row_heading level3 row4">
                    4
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow4_col0" class="data row4 col0">
                    0.799707
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow4_col1" class="data row4 col1">
                    0.663384
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow4_col2" class="data row4 col2">
                    0.351766
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow4_col3" class="data row4 col3">
                    0.425221
                
            </tr>
            
            <tr>
                
                <th id="T_077c76be_f2f9_11e7_9818_240a64de810d" class="row_heading level3 row5">
                    5
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow5_col0" class="data row5 col0">
                    0.75646
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow5_col1" class="data row5 col1">
                    0.381174
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow5_col2" class="data row5 col2">
                    0.922843
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow5_col3" class="data row5 col3">
                    0.0317737
                
            </tr>
            
            <tr>
                
                <th id="T_077c76be_f2f9_11e7_9818_240a64de810d" class="row_heading level3 row6">
                    6
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow6_col0" class="data row6 col0">
                    0.443823
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow6_col1" class="data row6 col1">
                    0.272329
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow6_col2" class="data row6 col2">
                    0.102859
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow6_col3" class="data row6 col3">
                    0.214509
                
            </tr>
            
            <tr>
                
                <th id="T_077c76be_f2f9_11e7_9818_240a64de810d" class="row_heading level3 row7">
                    7
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow7_col0" class="data row7 col0">
                    0.718827
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow7_col1" class="data row7 col1">
                    0.107608
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow7_col2" class="data row7 col2">
                    0.285968
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow7_col3" class="data row7 col3">
                    0.0385898
                
            </tr>
            
            <tr>
                
                <th id="T_077c76be_f2f9_11e7_9818_240a64de810d" class="row_heading level3 row8">
                    8
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow8_col0" class="data row8 col0">
                    0.558222
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow8_col1" class="data row8 col1">
                    0.728724
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow8_col2" class="data row8 col2">
                    0.253244
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow8_col3" class="data row8 col3">
                    0.366764
                
            </tr>
            
            <tr>
                
                <th id="T_077c76be_f2f9_11e7_9818_240a64de810d" class="row_heading level3 row9">
                    9
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow9_col0" class="data row9 col0">
                    0.65959
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow9_col1" class="data row9 col1">
                    0.728115
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow9_col2" class="data row9 col2">
                    0.64533
                
                <td id="T_077c76be_f2f9_11e7_9818_240a64de810drow9_col3" class="data row9 col3">
                    0.475732
                
            </tr>
            
        </tbody>
        </table>
        




```python
# 分段式构建样式

df = pd.DataFrame(np.random.rand(10,4),columns = list('ABCD'))
df['A'][[3,2]] = np.nan
df.style.\
    bar(subset=['A', 'B'], color='#d65f5f', width=100).\
    highlight_null(null_color='yellow')
```





        <style  type="text/css" >
        
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow0_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 69.23569529384095%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow0_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 53.02872303856184%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow1_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow1_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 15.952968401363195%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow2_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f nan%, transparent 0%);
            
                background-color:  yellow;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow2_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 83.91322721082197%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow3_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f nan%, transparent 0%);
            
                background-color:  yellow;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow3_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 75.00425537490163%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow4_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 50.42948320509824%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow4_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 54.44483277408722%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow5_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 1.048823137417722%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow5_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 100.0%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow6_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 62.91320734451104%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow6_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 76.32240418395574%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow7_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 96.95201846864457%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow7_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 5.41059535996635%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow8_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 59.48230743956116%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow8_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 18.711807256455675%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow9_col0 {
            
                width:  10em;
            
                 height:  80%;
            
                background:  linear-gradient(90deg,#d65f5f 100.0%, transparent 0%);
            
                : ;
            
            }
        
            #T_08541536_f2f9_11e7_8ac7_240a64de810drow9_col1 {
            
                width:  10em;
            
                 height:  80%;
            
                : ;
            
            }
        
        </style>

        <table id="T_08541536_f2f9_11e7_8ac7_240a64de810d" None>
        

        <thead>
            
            <tr>
                
                <th class="blank">
                
                <th class="col_heading level0 col0">A
                
                <th class="col_heading level0 col1">B
                
                <th class="col_heading level0 col2">C
                
                <th class="col_heading level0 col3">D
                
            </tr>
            
        </thead>
        <tbody>
            
            <tr>
                
                <th id="T_08541536_f2f9_11e7_8ac7_240a64de810d" class="row_heading level3 row0">
                    0
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow0_col0" class="data row0 col0">
                    0.685636
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow0_col1" class="data row0 col1">
                    0.557271
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow0_col2" class="data row0 col2">
                    0.128983
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow0_col3" class="data row0 col3">
                    0.493455
                
            </tr>
            
            <tr>
                
                <th id="T_08541536_f2f9_11e7_8ac7_240a64de810d" class="row_heading level3 row1">
                    1
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow1_col0" class="data row1 col0">
                    0.0286531
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow1_col1" class="data row1 col1">
                    0.219964
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow1_col2" class="data row1 col2">
                    0.0394714
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow1_col3" class="data row1 col3">
                    0.657113
                
            </tr>
            
            <tr>
                
                <th id="T_08541536_f2f9_11e7_8ac7_240a64de810d" class="row_heading level3 row2">
                    2
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow2_col0" class="data row2 col0">
                    nan
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow2_col1" class="data row2 col1">
                    0.838251
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow2_col2" class="data row2 col2">
                    0.0598857
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow2_col3" class="data row2 col3">
                    0.548219
                
            </tr>
            
            <tr>
                
                <th id="T_08541536_f2f9_11e7_8ac7_240a64de810d" class="row_heading level3 row3">
                    3
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow3_col0" class="data row3 col0">
                    nan
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow3_col1" class="data row3 col1">
                    0.757199
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow3_col2" class="data row3 col2">
                    0.169712
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow3_col3" class="data row3 col3">
                    0.973893
                
            </tr>
            
            <tr>
                
                <th id="T_08541536_f2f9_11e7_8ac7_240a64de810d" class="row_heading level3 row4">
                    4
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow4_col0" class="data row4 col0">
                    0.507182
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow4_col1" class="data row4 col1">
                    0.570154
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow4_col2" class="data row4 col2">
                    0.360712
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow4_col3" class="data row4 col3">
                    0.166776
                
            </tr>
            
            <tr>
                
                <th id="T_08541536_f2f9_11e7_8ac7_240a64de810d" class="row_heading level3 row5">
                    5
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow5_col0" class="data row5 col0">
                    0.0386054
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow5_col1" class="data row5 col1">
                    0.984605
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow5_col2" class="data row5 col2">
                    0.775698
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow5_col3" class="data row5 col3">
                    0.309116
                
            </tr>
            
            <tr>
                
                <th id="T_08541536_f2f9_11e7_8ac7_240a64de810d" class="row_heading level3 row6">
                    6
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow6_col0" class="data row6 col0">
                    0.625641
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow6_col1" class="data row6 col1">
                    0.769192
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow6_col2" class="data row6 col2">
                    0.717468
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow6_col3" class="data row6 col3">
                    0.354582
                
            </tr>
            
            <tr>
                
                <th id="T_08541536_f2f9_11e7_8ac7_240a64de810d" class="row_heading level3 row7">
                    7
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow7_col0" class="data row7 col0">
                    0.948638
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow7_col1" class="data row7 col1">
                    0.124052
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow7_col2" class="data row7 col2">
                    0.525165
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow7_col3" class="data row7 col3">
                    0.050235
                
            </tr>
            
            <tr>
                
                <th id="T_08541536_f2f9_11e7_8ac7_240a64de810d" class="row_heading level3 row8">
                    8
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow8_col0" class="data row8 col0">
                    0.593085
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow8_col1" class="data row8 col1">
                    0.245063
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow8_col2" class="data row8 col2">
                    0.578993
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow8_col3" class="data row8 col3">
                    0.0695989
                
            </tr>
            
            <tr>
                
                <th id="T_08541536_f2f9_11e7_8ac7_240a64de810d" class="row_heading level3 row9">
                    9
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow9_col0" class="data row9 col0">
                    0.97756
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow9_col1" class="data row9 col1">
                    0.0748271
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow9_col2" class="data row9 col2">
                    0.616208
                
                <td id="T_08541536_f2f9_11e7_8ac7_240a64de810drow9_col3" class="data row9 col3">
                    0.630743
                
            </tr>
            
        </tbody>
        </table>
        


