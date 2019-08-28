

```python
'''
【项目02】  基于Python的算法函数创建

作业要求：
根据不同题目，完成代码书写并成功运行

'''
```




    '\n【项目02】  基于Python的算法函数创建\n\n作业要求：\n根据不同题目，完成代码书写并成功运行\n\n'




```python
# 题目1：有1、2、3、4个数字，能组成多少个互不相同且无重复数字的两位数？都是多少？
# 该题目不用创建函数
```


```python
n = 0
for i in range(1,5):
    for j in range(1,5):
        if i != j:
            n +=1
            a = i*10+j
            print('第%d数字为%d' %(n,a))
```

    第1数字为12
    第2数字为13
    第3数字为14
    第4数字为21
    第5数字为23
    第6数字为24
    第7数字为31
    第8数字为32
    第9数字为34
    第10数字为41
    第11数字为42
    第12数字为43
    


```python
# 题目2：输入三个整数x,y,z，请把这三个数由小到大输出，可调用input()。（需要加判断：判断输入数据是否为数字）
# 提示：判断是否为数字：.isdigit()
# 该题目需要创建函数
```


```python
def f(x):
    a = []
    for i in range(1,x+1):
        y = input('请输入第%i个数字：'%i)
        while y.isdigit() == False:
            y = input('请重新输入第%i个数字：'%i)
        else:
            a.append(float(y))
    return(sorted(a))
f(3)
```

    请输入第1个数字：329.2
    


```python
# 题目3：输入一行字符，分别统计出其中英文字母、空格、数字和其它字符的个数。
# 提示：利用while语句,条件为输入的字符不为'\n'.
# 该题目不需要创建函数
```


```python
st = input('请输入一行字符：\n')
letters = 0
space = 0
digit = 0
others = 0
for c in st:
    if c.isalpha():
        letters += 1
    elif c.isspace():
        space += 1
    elif c.isdigit():
        digit += 1
    else:
        others += 1
print ('char = %d,space = %d,digit = %d,others = %d' % (letters,space,digit,others))
```

    请输入一行字符：
    fgsfgs sfgs we324543gtv  frdv
    char = 19,space = 4,digit = 6,others = 0
    


```python
# 题目4：猴子吃桃问题
# 猴子第一天摘下若干个桃子，当即吃了一半，还不瘾，又多吃了一个,
# 第二天早上又将剩下的桃子吃掉一半，又多吃了一个。
# 以后每天早上都吃了前一天剩下的一半零一个。到第10天早上想再吃时，见只剩下一个桃子了。求第一天共摘了多少?
# 提示：采取逆向思维的方法，从后往前推断。
# 该题目不需要创建函数
```


```python
n = 1
for i in range(9):
    n =(n+1)*2
print(n)
```

    1534
    


```python
# 题目5：猜数字问题，要求如下：
# ① 随机生成一个整数
# ② 猜一个数字并输入
# ③ 判断是大是小，直到猜正确
# ④ 判断时间
# 提示：需要用time模块、random模块
# 该题目不需要创建函数
```


```python
import time
import random
    
play_it = input('do you want to play it.(\'y\' or \'n\')')   # 询问是否参与游戏
while play_it == 'y':
    c = input('input a character:\n')   # 输入参与游戏人物
    i = random.randint(0,100)
    print( 'please input number you guess:\n')
    a = time.time()  # 记录开始时间
    guess = int(input('input your guess:\n'))
    while guess != i:
        if guess > i:
            print( 'please input a little smaller')
            guess = int(input('input your guess:\n'))
        else:
            print( 'please input a little bigger')
            guess = int(input('input your guess:\n'))
    b = time.time()  # 记录结束时间
    usedtime = b - a
    print( 'It took you %.2f seconds' % usedtime)
    if usedtime < 15:
        print( 'you are very clever!')
    elif usedtime < 25:
        print( 'you are normal!')
    else:
        print( 'you are stupid!')
    print( 'Congradulations')
    print( 'The number you guess is %d' % i)
    break
else:
    print('hehe')
```

    do you want to play it.('y' or 'n')y
    input a character:
    1
    please input number you guess:
    
    input your guess:
    50
    please input a little smaller
    input your guess:
    85
    please input a little smaller
    input your guess:
    25
    It took you 20.78 seconds
    you are normal!
    Congradulations
    The number you guess is 25
    


```python

```
