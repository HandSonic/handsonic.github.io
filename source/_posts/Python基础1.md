---
title: Python基础1
date: 2020-05-26 18:25:17
tags: [python, coding]
---
# 0.引言

值和类型

值（value）是程序操作的最基本的东西，如一个字母或者数字

值属于不同的数据类型（type）

Python中的数据类型：

- 基本数据类型

  - 数字（整型（长整型）、浮点型、复数）
   
  - 布尔型

- 容器数据类型　
  
  - 字符串

  - 列表

  - 元组

  - 字典

  - 集合

<!-- more -->
```python
age = 10
height = 150.5
name = 'Tom'
```

# 1.基本数据类型

## 1.1 整型


```python
a = 1031
#可以看出变量a 的值及 a 的类（class）是 int
print(a, type(a))
```

Python 中**万物皆对象（object）**，「整数」也不例外

只要是对象，就有相应的**<u>属性（attributes）</u>**与**<u>方法（methods）</u>**

通过dir(x)和 help(x)可以看出 x 对应的对象里可用的属性和方法


```python
dir(int)
```


```python
help(int)
```


```python
# bit_length函数返回整数对应的二进制值的长度
# a = 1031，对应二进制值为 1000000011，长度为 11
a.bit_length()
```


```python
#长整形（了解）
#在python2中（python3中没有长整形的概念）
'''
num=2L
type(num)
    <type 'long'>
'''
#复数（了解）　　
x=1-2j
print(x.real)
print(x.imag)
```

## 1.2 浮点型


```python
print(1, type(1))
print(1., type(1.))
```

浮点型（float）数就是实数

如果想保留浮点型的小数点后 n 位，可以用 decimal 包里的 Decimal 对象和 getcontext()方法来实现：


```python
import decimal
from decimal import Decimal
# Decimal 对象的默认精度值是28 位
decimal.getcontext()
```


```python
d = Decimal(1) / Decimal(3)
d
```


```python
decimal.getcontext().prec = 4
e = Decimal(1) / Decimal(3)
print(e)
```

内置函数int()与float()

int()函数用于将一个字符串或数字转换为整数

float() 函数用于将整数和字符串转换成浮点数


```python
help(int())
```


```python
x = int(10.5)
print(x)
y = int('101',2)
print(y)
```

## 1.3 布尔型

布尔（boolean）型变量只能取两个值，True 和 False

当把布尔型变量用在数字运算中，用 1 和 0 代表True 和 False


```python
T = True
F = False
print(T + 2)
print(F - 8)
```

除了直接给变量赋值True 和 False，还可以用 bool(x)来创建变量

其中 x 可以是：

*基本类型：整型、浮点型、布尔型

*容器类型：字符、元组、列表、字典和集合



```python
# 基本类型
# bool 作用在基本类型变量：x 只要不是整型 0、浮点型 0.0，bool(x) 就是True，其余就是 False
print(type(0), bool(0), bool(2))
print(type(0.), bool(0.), bool(1.5))
print(type(True), bool(False), bool(True))
```


```python
# 容器类型
# bool 作用在容器类型变量：x 只要不是空的变量，bool(x) 就是 True，其余就是 False
print( type(''), bool( '' ), bool( 'python' ) )
print( type(()), bool( () ), bool( (10,) ) )
print( type([]), bool( [] ), bool( [1,2] ) )
print( type({}), bool( {} ), bool( {'a':1, 'b':2} ) )
print( type(set()), bool( set() ), bool( {1,2} ) )
```

## 1.4 身份运算 

type()方法可以查看一个数据的类型，那么如何判断一个数据是否是某个数据类型呢？Python 提供了身份运算符 is 和 is not。


```python
a = 34
type(a) is int
```


```python
b = 12.5
type(b) is not float
```

注意 is 运算也是比较，is比较的是id，而==比较的是值。

毫无疑问，id若相同则值肯定相同，而值相同id则不一定相同


```python
x = 123
y = 123
#x == y
print(id(x))
print(id(y))
```


```python
m = 1234
n = 1234
m is n
print(id(m))
print(id(n))
```


```python
a = 5
b = a
print(id(a))
print(id(b))
a = 6
print(b)
```

# 2.容器数据类型

整型、浮点型和布尔型都可以看成是单独数据，而这些数据都可以放在一个容器里得到一个「容器类型」的数据，比如：

字符 (str) 是一容器的字节 char，注意 Python 里面没有 char 类型的数据，可以把单字符的 str 当做 char。

元组 (tuple)、列表 (list)、字典 (dict) 和集合 (set) 是一容器的任何类型变量。

## 2.1 字符串

字符串用于处理文本 (text) 数据，用「单引号 ’」和「双引号 “」来定义都可以。


```python
t1 = 'i love python!'
print( t1, type(t1) )
t2 = "I love Python!"
print( t2, type(t2) )
```

### 字符串方法
字符中常见的内置方法 (可以用 dir(str) 来查看) 有：


```python
# capitalize()：大写句首的字母
t1.capitalize()
```


```python
# title()：每个单词首字母大写
t1.title()
```


```python
# upper()：所有字母大写
t1.upper()
```


```python
# lower()：所有字母小写
t2.lower()
```


```python
# split()：拆分字符串（默认用空格拆分）
t1.split()
```


```python
#  find(x)：找到给定词 x 在句中的索引，找不到返回 -1
print( t1.find('love') )
print( t1.find('like') )
```


```python
# replace(x, y)：把句中 x 替代成 y
t3 = t2.replace( 'love Python', 'hate R' )
print(t3)
```


```python
# strip(x)：删除句首或句末含 x 的部分
print( 'http://www.python.org'.strip('htp:/') )
print( 'http://www.python.org'.strip('.org') )
```

### 索引和切片

Python 里面索引和切片有三个特点：

*从 0 开始 (和 C 一样)

*切片通常写成 start:end 这种形式，包括「start 索引」对应的元素，不包括「end索引」对应的元素。

索引值可正可负，正索引从 0 开始，从左往右；负索引从 -1 开始，从右往左。使用负数索引时，会从最后一个元素开始计数。最后一个元素的位置编号是 -1。


```python
s = 'Python'
print(s)
#print( s[2:4] )
print( s[-5:-2] )
print( s[2] )
print( s[-1] )
```

### 成员运算in

Python支持成员运算符，可用于字符串、列表和元组

- in：如果在指定的序列中找到值返回 True，否则返回 False。
- not in：如果在指定的序列中没有找到值返回 True，否则返回 False。


```python
'py' in 'python'
```

### 正则表达式

正则表达式 (regular expression) 主要用于识别字符串中符合某种模式的部分，什么叫模式呢？看下面的例子：



```python
input = """
'06/18/2019 13:00:00', 100, '1st';
'06/18/2019 13:30:00', 110, '2nd';
'06/18/2019 14:00:00', 120, '3rd'
"""
input
```

假如想把上面字符串中的「时间」的模式来抽象的表示出来，对照着具体表达式'06/18/2019 13:00:00' 来看，我们发现该字符串有以下规则：

1.开头和结束都有个单引号 '

2.里面有多个 0-9 数字

3.里面有多个正斜线/ 和冒号 : 

4.还有一个空格

因此我们用下面这样的模式：


```python
import re
pattern = re.compile("'[0-9/:\s]+'")
```

再看这个抽象模式表达式 '[0-9/:\s]+'，里面符号的意思如下：

最外面的两个单引号 ' 代表该模式以它们开始和结束

中括号 [] 用来概括该模式涵盖的所有类型的字节

0-9 代表数字类的字节
/ 代表正斜线

: 代表冒号

\s 代表空格

[ ] 外面的加号 + 代表 [ ] 里面的字节出现至少 1 次

有了模式 pattern，我们来看看是否能把字符串中所有符合 pattern 的日期表达式都找出来。


```python
pattern.findall(input)
```

关于正则表达式的内容可以进一步参考：https://www.cnblogs.com/huxi/archive/2010/07/04/1771073.html

## 2.2 元组

### 创建元组
「元组」定义语法为：

(元素1, 元素2, ..., 元素n)

关键点是「小括号 ()」和「逗号 ,」

小括号把所有元素绑在一起

逗号将每个元素一一分开


```python
t1 = (1, 10.31, 'python')
t2 = 1, 10.31, 'python'
print( t1, type(t1) )
print( t2, type(t2) )
```

创建元组可以用小括号 ()，也可以什么都不用，为了可读性，建议还是用 ()。

此外对于含单个元素的元组，务必记住要多加一个**逗号**：


```python
print( type( ('OK') ) )  # 没有逗号 , 
print( type( ('OK',) ) ) # 有逗号 ,
```

也可以创建二维元组：


```python
nested = (1, 10.31, 'python'), ('data', 11)
nested
```

### 索引和切片

元组中可以用整数来对它进行索引 (indexing) 和切片 (slicing)

不严谨的讲，前者是获取单个元素，后者是获取一组元素。


```python
#((1, 10.31, 'python'), ('data', 11))
# 索引
print(nested[0])
print( nested[0][0], nested[0][1], nested[0][2] )
# 切片
nested[0][0:2]
```

### 不可更改
元组有不可更改 (immutable) 的性质，因此不能**直接**给元组的元素赋值，例如：


```python
t = ('OK', [1, 2], True)
t[2] = False
```

但是只要元组中的元素可更改 (mutable)，那么我们可以直接更改其元素，注意这跟赋值其元素不同。


```python
# t[1] 是列表，其内容可以更改，因此用 append 在列表后加一个值没问题
t[1].append(3)
print(t)
```

### 内置方法
元组大小和内容都不可更改，因此只有 count 和 index 两种方法。


```python
t = (1, 10.31, 'python')
print( t.count('python') )
print( t.index(10.31) )
```

这两个方法返回值都是 1，但意思完全不同

count('python') 是记录在元组 t 中该元素出现几次，显然是 1 次

index(10.31) 是找到该元素在元组 t 的索引，显然是 1

### 元组拼接
元组拼接 (concatenate) 有两种方式，用「加号 +」和「乘号 *」，前者首尾拼接，后者复制拼接。


```python
a = (1, 10.31, 'python') + ('data', 11) + ('OK',)
b = (1, 10.31, 'python') * 2
print(a)
print(b)
```

### 解压元组 
解压 (unpack) 一维元组：有几个元素左边括号定义几个变量


```python
t = (1, 10.31, 'python')
(a, b, c) = t
print( b )
```

解压二维元组：按照元组里的元组结构来定义变量


```python
t = (1, 10.31, ('OK','python'))
(a, b, (c,d)) = t
print( a, b, c, d )
```

如果你只想要元组其中几个元素，用通配符（wildcard）「*」，在计算机语言中代表一个或多个元素。


```python
t = 1, 2, 3, 4, 5
# 把多个元素丢给了 rest 变量
a, b, *rest, c = t
print( a, b, c )
print( rest )
```

如果你根本不在乎 rest 变量，那么就用通配符「*」加上下划线「_」：


```python
a, b, *_ = t
print( a, b )
```

### 元组的优缺点
优点：占内存小，安全，创建遍历速度比列表快，可一赋多值。

缺点：不能添加和更改元素。


```python
%timeit [1, 2, 3, 4, 5]
%timeit (1, 2, 3, 4, 5)
```

## 2.3 列表

### 创建列表
列表」定义语法为 

[元素1, 元素2, ..., 元素n]

关键点是「中括号 [ ]」和「逗号 ,」

- 中括号把所有元素绑在一起

- 逗号将每个元素一一分开



```python
l = [1, 10.31,'python']
print(l, type(l))
```

不像元组，列表内容可更改 (mutable)，因此附加 (append, extend)、插入 (insert)、删除 (remove, pop) 这些操作都可以使用。


```python
# 附加(append, extend)
# append 是追加，把一个东西整体添加在列表后
l.append([4, 3])
print( l )
# extend 是扩展，把一个东西里的所有元素添加在列表后
l.extend([1.5, 2.0, 'OK'])
print( l ) 
```


```python
# 插入
l.insert(1, 'abc') # 在索引位置之前插入内容
l
```


```python
# 删除
# remove指定具体要删除的元素
l.remove('python') 
# pop指定一个索引位置，比如 3，删除 l[3] 并返回出来
p = l.pop(3) 
print( p )
print( l ) 
```

### 索引切片


```python
l = [7, 2, 9, 10, 1, 3, 7, 2, 0, 1]
print(l[1:5])
print(l[-4:])
```

列表可更改，因此可以用切片来赋值。


```python
l[2:4] = [999, 1000]
l
```

切片的通用写法是

start : stop : step

这三个在特定情况下都可以省去，我们来看看四种情况：


```python
# 情况 1 - start :(以 step 为 1 (默认) 从编号 start 往列表尾部切片)
print( l )
print( l[3:] )
print( l[-4:] )
```


```python
# 情况 2 - : stop(以 step 为 1 (默认) 从列表头部往编号 stop 切片)
print( l )
print( l[:6] )
print( l[:-4] )
```


```python
# 情况 3 - start : stop(以 step 为 1 (默认) 从编号 start 往编号 stop 切片)
print( l )
print( l[2:4] )
print( l[-5:-1] )
```


```python
# 情况 4 - start : stop : step(以具体的 step 从编号 start 往编号 stop 切片)
print( l )
print( l[1:5:2] )
print( l[:5:2] )
print( l[1::2] )
print( l[::2] )
print( l[::-1] )
```

### 列表拼接
和元组拼接一样， 列表拼接也有两种方式，用「加号 +」和「乘号 *」，前者首尾拼接，后者复制拼接


```python
a = [1, 10.31, 'python'] + ['data', 11] + ['OK']
b = [1, 10.31, 'python'] * 2
print(a)
print(b)
```

### 列表优缺点
优点：灵活好用，可索引、可切片、可更改、可附加、可插入、可删除。

缺点：相比 tuple 创建和遍历速度慢，占内存。此外查找和插入时间较慢。

### 练习

1.有列表data=[['张三','男',[175.5,71.0]],['李四','女',[165.0,55.5]]]，分别取出列表中的名字，性别，身高、体重值并按如下格式输出：“张三，男，身高175.5cm，体重71.0kg。”，每条数据一行。

2.双色球

先让用户依次选择6个红球（1-32），再选择2个蓝球（1-16），最后打印输出用户选择的球号（按从小到大的顺序）。注意确保用户不能选择重复的，选择的数不能超出范围。


```python
data=[['张三','男',[175.5,71.0]],['李四','女',[165.0,55.5]]]
#for lst in data:
    
print('{}，{}，身高{}cm，体重{}kg。'.format(data[0][0],data[0][1],data[0][2][0],data[0][2][1]))
```

## 2.4 字典

### 创建字典
「字典」定义语法为 

{元素1, 元素2, ..., 元素n}

其中每一个元素是一个「键值对」- 键:值 (key:value)

关键点是「大括号 {}」,「逗号 ,」和「冒号 :」

大括号把所有元素绑在一起

逗号将每个键值对一一分开

冒号将键和值分开


```python
d = {
'Name' : 'Tencent',
'Country' : 'China',
'Industry' : 'Technology',
'Code': '00700.HK',
'Price' : '361 HKD'
}
print( d, type(d) )
```

### 内置方法
字典里最常用的三个内置方法就是 keys(), values() 和 items()，分别是获取字典的键、值、对。


```python
print( list(d.keys()),'\n' )
print( list(d.values()), '\n' )
print( list(d.items()) )
```

在字典上也有添加、获取、更新、删除等操作。


```python
# 添加
d['Headquarter'] = 'Shen Zhen'
d
```


```python
# 获取
# 查看腾讯的股价是多少 (两种方法都可以)
print( d['Price'] )
print( d.get('Price') )
d.get('price')
```


```python
# 更新
#更新腾讯的股价到 359 港币
d['Price'] = '359 HKD'
d
```


```python
# 删除
#去掉股票代码 (code)
del d['Code']
d
```


```python
#或像列表里的 pop() 函数，删除行业 (industry) 并返回出来。
print( d.pop('Industry') )
d
```

### 不可更改键
字典里的键是不可更改的，因此只有那些不可更改的数据类型才能当键，比如整数 (虽然怪怪的)、浮点数 (虽然怪怪的)、布尔 (虽然怪怪的)、字符、元组 (虽然怪怪的)，而列表却不行，因为它可更改。


```python
d = {
2 : 'integer key',
10.31 : 'float key',
True  : 'boolean key',
('OK',3) : 'tuple key'
}
d
```

有个地方要注意下，True其实和整数 1 是一样的，由于键不能重复，当你把 2 该成 1时，你会发现字典只会取其中一个键


```python
d = {
1 : 'integer key',
10.31 : 'float key',
True : 'boolean key',
('OK',3) : 'tuple key'
}
d
```

如何快速判断一个数据类型 X 是不是可更改的呢？两种方法：

麻烦方法：用 id(X) 函数，对 X 进行某种操作，比较操作前后的 id，如果不一样，则 X 不可更改，如果一样，则 X 可更改。

便捷方法：用 hash(X)，只要不报错，证明 X 可被哈希，即不可更改，反过来不可被哈希，即可更改。



```python
i = 1
print( id(i) )
i = i + 2
print( id(i) )
```

整数 i 在加 1 之后的 id 和之前不一样，因此加完之后的这个 i (虽然名字没变)，但是不是加前的那个 i 了，因此整数是不可更改的。


```python
l = [1, 2]
print( id(l) )
l.append('Python')
print( id(l) )
```

列表 l 在附加 'Python' 之后的 id 和之前一样，因此列表是可更改的。

用 hash() 函数的在字符 s，元组 t 和列表 l 上的运行结果：


```python
hash('Name')
```


```python
hash( (1,2,'Python') )
```


```python
hash( [1,2,'Python'] )
```

### 字典优缺点
优点：查找和插入速度快

缺点：占内存大

### 字典的典型应用：计数器

给你一个字符串，请统计每个字母出现的次数。

有几种可能实现的方法：
- 创建 26 个变量，每个变量对应一个字母。然后遍历字符串，对每个字符，增加相应的计数器……
- 创建 一个包含 26 个元素的列表。每个变量对应一个字母……
- ……

使用字典：
- 建立一个字典，以字符作为键，以计数器作为相应的值。
- 遍历字符串，第一次遇到某个字符时，在字典中添加对应的项。


```python
def histogram(s):
    d = dict()
    for c in s:
        if c not in d:
            d[c] = 1 # c:1
        else:
            d[c] += 1
    return d
def main():
    h = input('请输入一个字符串：')
    print(histogram(h))
main()
```

    请输入一个字符串：AAVC
    {'A': 2, 'V': 1, 'C': 1}


优化：
字典的 get 方法接收一个键以及一个默认值，如果键在字典中，get 返回对应的值，否则返回它的默认值。
试试使用get方法优化代码，去掉if语句。


```python
d={'a':1}
d['d']+=d.get('d',1)
d
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-12-e75ddc4596af> in <module>
          1 d={'a':1}
    ----> 2 d['d']+=d.get('d',1)
          3 d


    KeyError: 'd'



```python
def histogram(s):
    d = dict()
    for c in s:
        #if c not in d:
        #    d[c] = 1
        #else:
        #    d[c] += 1
        d[c]=d.get(c,0)+1
    return d
def main():
    h = input('请输入一个字符串：')
    print(histogram(h))
main()
```

    请输入一个字符串：aabc
    {'a': 2, 'b': 1, 'c': 1}


这个程序还有两个问题:
- 同一个字母大小写会被分别统计。
- 输出结果不够友好：乱序、以字典的形式输出。
尝试修改程序，解决以上两个问题。

提示：内置函数sorted可以对字典的键进行排序。



```python
da = {'a':5,'c':3,'b':4}
sorted(da)
```

## 2.5 集合

### 创建集合
「集合」有两种定义语法，第一种是

{元素1, 元素2, ..., 元素n}

关键点是「大括号 {}」和「逗号 ,」

大括号把所有元素绑在一起

逗号将每个元素一一分开

第二种是用 set() 函数，把列表或元组转换成集合。

set( 列表 或 元组 )



```python
A = set(['u', 'd', 'ud', 'du', 'd', 'du'])
B = {'d', 'dd', 'uu', 'u'}
print( A )
print( B )
```

从 A 的结果发现集合的两个特点：无序 (unordered) 和唯一 (unique)。由于 set 存储的是无序集合，所以我们没法通过索引来访问，但是可以判断一个元素是否在集合中。


```python
B[1]
```


```python
set('apple')
```


```python
'u' in B
```

### 内置方法
用 set 的内置方法就把它当成是数学上的集合


```python
# 并集
print( A.union(B) )     # All unique elements in A or B
print( A | B )          # A OR B
```


```python
# 交集
print( A.intersection(B) )   # All elements in both A and B
print( A & B )               # A AND B
```


```python
# 差集
print( A.difference(B) )     # Elements in A but not in B
print( A - B )               # A MINUS B
print( B.difference(A) )     # Elements in B but not in A
print( B - A )               # B MINUS A
```


```python
# 对称差集
print( A.symmetric_difference(B) )   # All elements in either A or B, but not both
print( A ^ B )                       # A XOR B
```

### 集合优缺点
优点：不用判断重复的元素

缺点：不能存储可变对象

### 练习
有如下两个集合，pythons是报名python课程的学员名字集合，linuxs是报名linux课程的学员名字集合

pythons={'alex','egon','yuanhao','wupeiqi','gangdan','biubiu'}

linux={'wupeiqi','oldboy','gangdan'}
  
1. 求出即报名python又报名linux课程的学员名字集合
2. 求出所有报名的学生名字集合
3. 求出只报名python课程的学员名字
4. 求出没有同时这两门课程的学员名字集合

# 3 条件语句与迭代循环

在编写程序时，我们需要：

在不同条件下完成不同动作，条件语句（conditional statement）赋予程序选择的能力。

重复地完成某些动作，迭代循环（iterative loop）赋予程序重复能力。

## 3.1 条件语句
条件语句有以下四种格式：

1.if语句

2.if-else语句

3.if-elif-else语句

4.嵌套（nested）语句

![title](img/if.png)


```python
if x > 0:
    print( 'x is positive' )
```

![title](img/ifelse.png)


```python
if x % 2 == 0:
    print( 'x is even' )
else :
    print( 'x is odd' )
```

![title](img/ifelifelse.png)


```python
if x < y:
    print( 'x is less than y' )
elif x > y:
    print( 'x is greater than y' )
else:
    print( 'x and y are equal' )
```

![title](img/neastedif.png)


```python
if x == y:
    print( 'x and y are equal' )
else:
    if x < y:
        print( 'x is less than y' )
    else:
        print( 'x is greater than y' )
```

## 3.2 迭代循环
Python中有「while循环」和「for循环」。

while循环非常简单，只要条件为True就一直重复。

一般来说，在「while循环」中，迭代的次数事先时不知道的。


```python
n = 5
while n > 0:
    print(n)
    n = n-1
print('I love Python')
```

### break与continue


```python
#break用于退出本层循环
while True:
    print("123")
    break
    print("456")
```


```python
#continue用于退出本次循环
while True:
    print("123")
    continue
    print("456")
```

### while ...else 语句

与其它语言else 一般只与if 搭配不同，在Python 中还有个while ...else 语句，while 后面的else 作用是指，当while 循环正常执行完，中间没有被break 中止的话，就会执行else后面的语句


```python
count = 0
while count <= 5 :
    count += 1
    print("Loop",count)

else:
    print("循环正常执行完啦")
print("-----out of while loop ------")
```


```python
#如果执行过程中被break啦，就不会执行else的语句啦
count = 0
while count <= 5 :
    count += 1
    if count == 3:break
    print("Loop",count)

else:
    print("循环正常执行完啦")
print("-----out of while loop ------")
```

更多时候我们希望事先知道循环的次数，比如在列表、元组、字典等容器类型数据中遍历一遍，在每个元素层面上做点事情。这时候就需要「for循环」了。


```python
language = ['Python', 'R', 'Matlab', 'C++']
for language in language:
    print('I love', language)
print('Done!')
```

「for循环」的通用形式为：

for a in A:

    do somthing with a

其中A是个可迭代数据（str, list, tuple, dic, set），a是A中的每个元素。  


```python

```

在遍历中，还有一个enumerate() 函数需要介绍一下：

enumerate() 函数用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中。

enumerate() 函数的语法如下：

enumerate(sequence, [start=0])


```python
language = ['Python', 'R', 'Matlab', 'C++']
for i,language in enumerate(language):
    print(i,'I love', language)
print('Done!')
```

    0 I love Python
    1 I love R
    2 I love Matlab
    3 I love C++
    Done!



```python
language = ['Python', 'R', 'Matlab', 'C++']
i = 1
for item in language:
    print(i,language[i])
    i += 1
print('Done!')
```

enumerate() 函数应用实例：

要统计文件的行数，可以这样写：

count = len(open(filepath, 'r').readlines())

这种方法简单，但是可能比较慢，当文件比较大时甚至不能工作。

可以利用enumerate()：

count = 0
for index, line in enumerate(open(filepath,'r'))： 
  count += 1

### 练习

1.编写一个程序进行用户登录验证，如果用户名和密码与程序设置一致则提示“登录成功”，否则提示“用户名或密码错误，请重试！”，一共有三次机会重试，超出三次程序结束。

2.打印金字塔，金字塔的层数可以用参数控制
max_level = 5
    @       max_level = 1,空格4（5-n），@1（2n-1）       
   @@@      max_level = 2,空格3，@3 5-2
  @@@@@     max_level = 3,空格2，@5 5-3
 @@@@@@@    max_level = 4,空格1，@7 
@@@@@@@@@   max_level = 5,空格0，@9
