---
title: Python基础2
date: 2020-05-26 18:25:17
tags: [python, coding]
---
# 函数

1 什么是函数？

2 为什么要用函数？

3 函数的分类：内置函数与自定义函数

4 如何自定义函数

- 语法
- 定义有参数函数，及有参函数的应用场景
- 定义无参数函数，及无参函数的应用场景
- 定义空函数，及空函数的应用场景

5 调用函数

- 如何调用函数
- 函数的返回值
- 函数参数的应用：形参和实参，位置参数，关键字参数，默认参数，*args，**kwargs

6 匿名函数

7 高阶函数

8 解析式
<!-- more -->
## 1 什么是函数

想象生活中的例子，修理工需要事先在工具箱里面准备好锤子、扳手、钳子等工具，然后遇到锤钉子的场景，拿来锤子用就可以，而无需临时再制造一把锤子。

修理工===>程序员

具备某一功能的工具===>函数

要想使用工具，需要事先准备好，然后拿来就用且可以重复使用
要想用函数，需要先定义，再使用

定义: 函数是指将一组语句的集合通过一个名字(函数名)封装起来，要想执行这个函数，只需调用其函数名即可

## 2 为什么要用函数

解决三个问题：

1 代码的组织结构不清晰，可读性差

2 遇到重复的功能只能重复编写实现代码，代码冗余

3 功能需要扩展时，需要找出所有实现该功能的地方修改，无法统一管理且维护难度极大 

## 3  函数的分类：内置函数与自定义函数

1 内置（built-in）函数

为了方便我们的开发，针对一些简单的功能，python解释器已经为我们定义好了的函数叫内置函数。

对于内置函数，我们可以拿来就用而无需事先定义，如：len(),sum(),max()

2 自定义函数

很明显内置函数所能提供的功能是有限的，这就需要我们自己根据需求，事先定制好我们自己的函数来实现某种功能，以后，在遇到应用场景时，调用自定义的函数即可。

## 4 如何自定义函数


```python
#语法
def 函数名(参数1,参数2,参数3,...):
    '''注释'''
    函数体
    return 返回的值

#函数名要能反映其意义
```


      File "<ipython-input-1-3a09a5c2bd40>", line 2
        def 函数名(参数1,参数2,参数3,...):
                              ^
    SyntaxError: invalid syntax




```python
def auth(user:str,password:str)->int:
    '''
    auth function
    :param user: 用户名
    :param password: 密码
    :return: 认证结果
    '''
    if user == 'egon' and password == '123':
        return 1
# print(auth.__annotations__) #{'user': <class 'str'>, 'password': <class 'str'>, 'return': <class 'int'>}

user=input('用户名>>: ').strip()
pwd=input('密码>>: ').strip()
res=auth(user,pwd)
print(res)
```

    用户名>>: egon
    密码>>: 123
    1


### 函数使用的原则

先定义，再调用


函数即“变量”，“变量”必须先定义后引用。未定义而直接引用函数，就相当于在引用一个不存在的变量名


```python
#测试一
def foo():
    print('from foo')
    bar()
foo() #报错
```

    from foo



    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-18-37242c8c0654> in <module>()
          3     print('from foo')
          4     bar()
    ----> 5 foo() #报错
    

    <ipython-input-18-37242c8c0654> in foo()
          2 def foo():
          3     print('from foo')
    ----> 4     bar()
          5 foo() #报错


    NameError: name 'bar' is not defined



```python
#测试二
def bar():
    print('from bar')
def foo():
    print('from foo')
    bar()
foo() #正常
```

    from foo
    from bar



```python
#测试三
def foo():
    print('from foo')
    bar()
    
def bar():
    print('from bar')
foo() #会报错吗?
```

    from foo
    from bar



```python
'''
结论:函数的使用,必须遵循原则:先定义,后调用
我们在使用函数时,一定要明确地区分定义阶段和调用阶段
'''
#定义阶段
def foo():
    print('from foo')
    bar()
def bar():
    print('from bar')
#调用阶段
foo()
```

### 函数在定义阶段都干了哪些事？

只检测语法，不执行代码

也就说，**语法错误**在函数定义阶段就会检测出来，而代码的**逻辑错误**只有在执行时才会知道。

### 定义函数的三种形式

- 无参：应用场景仅仅只是执行一些操作，比如与用户交互，打印

- 有参：需要根据外部传进来的参数，才能执行相应的逻辑，比如统计长度，求最大值最小值

- 空函数：设计代码结构


```python
#定义阶段
def tell_tag(tag,n): #有参数
    print(tag*n)

def tell_msg(): #无参数
    print('hello world!')

#调用阶段
tell_tag('*',12)
tell_msg()
tell_tag()

#结论：
#1、定义时无参，意味着调用时也无需传入参数
#2、定义时有参，意味着调用时则必须传入参数

```

    ************
    hello world!



    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-22-f7552c45df36> in <module>()
          9 tell_tag('*',12)
         10 tell_msg()
    ---> 11 tell_tag()
         12 
         13 #结论：


    TypeError: tell_tag() missing 2 required positional arguments: 'tag' and 'n'



```python
# 空函数
def auth(user,password):                             
    '''                                                           
    auth function                                                 
    :param user: 用户名                                              
    :param password: 密码                                           
    :return: 认证结果                                                 
    '''                                                           
    pass                                                          
                                                                  
def get(filename):                                                
    '''                                                           
    :param filename:                                              
    :return:                                                      
    '''                                                           
    pass                                                          
                                                                  
def put(filename):                                                
    '''                                                           
    :param filename:                                              
    :return:                                                      
    '''                                                           
def ls(dirname):                                                  
    '''                                                           
    :param dirname:                                               
    :return:                                                      
    '''                                                           
    pass                                                          

#程序的体系结构立见           
```

### 练习
尝试使用函数完成以下代码实现的效果。


```python
print('+ - - - - + - - - - +')
print('|         |         |')
print('|         |         |')
print('|         |         |')
print('+ - - - - + - - - - +')
print('|         |         |')
print('|         |         |')
print('|         |         |')
print('+ - - - - + - - - - +')
```

    + - - - - + - - - - +
    |         |         |
    |         |         |
    |         |         |
    + - - - - + - - - - +
    |         |         |
    |         |         |
    |         |         |
    + - - - - + - - - - +


进一步优化程序，编写一个函数 print_table(rows, cols, width)实现表格打印，其中参数rows代表表格的行数，参数rows代表表格的列数，参数 width代表单元格的宽度（即两个+中间有几个-）。

## 5 调用函数

### 5.1 调用函数

函数的调用：函数名加括号

1）先找到名字

2）根据名字调用代码

### 5.2 函数返回值

函数外部的代码要想获取函数的执行结果，就可以在函数里用return语句把结果返回。

函数在执行过程中只要遇到return语句，就会停止执行并返回结果，也可以理解为 return 语句代表着函数的结束。

如果未在函数中指定return,那这个函数的返回值为None。


```python
- 无return->None

- return 1个值->返回1个值

- return 逗号分隔多个值->元组
```

什么时候该有返回值？

- 调用函数，经过一系列的操作，最后要拿到一个明确的结果，则必须要有返回值

- 通常有参函数需要有返回值，输入参数，经过计算，得到一个最终的结果

什么时候不需要有返回值？

- 调用函数，仅仅只是执行一系列的操作，最后不需要得到什么结果，则无需有返回值

- 通常无参函数不需要有返回值

### 5.3 全局与局部变量


```python
name = "c"
def change_name():
    name = "Jerry"
    print("After change:", name)
change_name()
print("在外面看看name改了么?",name)
```

    After change: Jerry
    在外面看看name改了么? c


为什么在函数内部改了name的值后， 在外面print的时候却没有改呢？ 因为这两个name根本不是一回事

- 在函数中定义的变量称为局部变量，在程序的一开始定义的变量称为全局变量。

- 全局变量作用域(即有效范围)是整个程序，局部变量作用域是定义该变量的函数。

- 变量的查找顺序是局部变量>全局变量

- 当全局变量与局部变量同名时，在定义局部变量的函数内，局部变量起作用；在其它地方全局变量起作用。

- 在函数里是不能直接修改全局变量的

如果想在函数里修改全局变量怎么办？


```python
name = "Tom"
def change_name():
    global name #声明一个全局变量
    name = "Jerry"
    print("After change:", name)
change_name()
print("在外面看看name改了么?", name)
```

    After change: Jerry
    在外面看看name改了么? Jerry


global name的作用就是要在函数里声明全局变量 name，意味着最上面的name = “Tom”即使不写，程序最后面的print也可以打印name

传递列表、字典、集合产生的现象：


```python
d = {"name":"Alex","age":26,"hobbie":"运动"}
l = ["Rebeeca","Katrina","Rachel"]
def change_data(info,name):
    info["hobbie"] = "学习"
    name.append("XiaoHong")
change_data(d,l)
print(d,l)
```

    {'name': 'Alex', 'age': 26, 'hobbie': '学习'} ['Rebeeca', 'Katrina', 'Rachel', 'XiaoHong']


不是说不能在函数里改全局变量么，为什么改了呢？

其实， 程序只是把d这个dict的内存地址传给了change_data函数，把dict比作鱼缸，里面的key,value比作缸里装的鱼。现在只是把鱼缸丢给了函数，这个鱼缸本身你不能改，但是里面的鱼可以。 

相当于只是传了一个对这个d的引用关系给到函数的形参。这样是为了减少内存的浪费，因为如果这个dict比较大，传一次到函数里就要copy一份新的值的话，效率太低了。

### 5.4 函数的参数

形参（parameter）与实参（argument）

- 形参变量

只有在被调用时才分配内存单元，在调用结束时，即刻释放所分配的内存单元。因此，形参只在函数内部有效。函数调用结束返回主调用函数后则不能再使用该形参变量

- 实参

可以是常量、变量、表达式、函数等，无论实参是何种类型的量，在进行函数调用时，它们都必须有确定的值，以便把这些值传送给形参。因此应预先给实参赋值。


```python
def calc(x, y):
    res = x ** y
    return res
a, b = 5, 8
c = calc(a, b)
print(c)
```

    390625


Python 的函数具有非常灵活多样的参数形态，既可以实现简单的调用，又可以传入非常复杂的参数。从简到繁的参数形态如下：

1.位置参数 (positional argument)

2.默认参数 (default argument)

3.可变参数 (variable argument)

4.关键字参数 (keyword argument)

5.命名关键字参数 (name keyword argument) 

6.参数组合

每种参数形态都有自己对应的应用。

#### 位置参数

![title](img/arg1.jpg)


```python
def calc(x, y):
    res = x ** y
    return res
a, b = 5, 8
c = calc(a, b)
print(c)
```

    390625


「位置参数」是按照参数的位置进行关联的。


```python
def calc(x, y):
    res = x ** y
    return res
a, b = 8, 5
c = calc(a, b)
print(c)
```

    32768


#### 默认参数

![title](img/arg2.jpg)

arg2 = v - 默认参数 = 默认值，调用函数的时候，默认参数已经有值，如果不传值就使用默认值，不会报错。


```python
def stu_register(name,age,country,course):
    print("----注册学生信息------")
    print("姓名:",name)
    print("age:",age)
    print("国籍:",country)
    print("课程:",course)
stu_register("王",22,"CN","python_devops")
stu_register("张",21,"CN","linux")
stu_register("刘",25,"CN","linux")
```

我们发现 country 这个参数 基本都 是”CN”, 就像我们在网站上注册用户，像国籍这种信息，你不填写，默认就会是 中国， 这就是通过默认参数实现的，把country变成默认参数非常简单：


```python
def stu_register(name,age,course,country="CN"):
    print("----注册学生信息------")
    print("姓名:",name)
    print("age:",age)
    print("国籍:",country)
    print("课程:",course)
stu_register("刘",25,"linux")
```


      File "<ipython-input-29-383d67d71eea>", line 1
        def stu_register(name,age,country="CN",course):
                        ^
    SyntaxError: non-default argument follows default argument



> **注意**：默认函数一定要放在位置参数后面，不然程序会报错。


```python
help(print)
```

    Help on built-in function print in module builtins:
    
    print(...)
        print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
        
        Prints the values to a stream, or to sys.stdout by default.
        Optional keyword arguments:
        file:  a file-like object (stream); defaults to the current sys.stdout.
        sep:   string inserted between values, default a space.
        end:   string appended after the last value, default a newline.
        flush: whether to forcibly flush the stream.
    



```python
# 「默认参数」可以是多个
def instrument3( id, ntl=1, curR='CNY' ):
    print( 'id:', id )
    print( 'notional:', ntl )
    print( 'reporting currency:', curR)
#instrument3( 'MM1001', 100, 'USD' )
# 有时在调用函数时，我们会记不住参数的顺序，比如 ntl 和 curR 的位置写反了
#instrument3( 'MM1001', 'USD', 100 )
# 在调用参数把它的「关键字」也带上，我们就可以随便调换参数的顺序。
#instrument3( 'MM1001', curR='USD', ntl=100 )
```

#### 可变参数

![title](img/arg3.jpg)

若你的函数在定义时不确定用户想传入多少个参数，就可以使用可变参数

*args - 可变参数，可以是从零个到任意个，自动组装成元组。




```python
def stu_register(name,age,*args): # *args 会把多传入的参数变成一个元组形式
    print(name,age,args)
stu_register("Alex",22)
#输出
#Alex 22 () #后面这个()就是args,只是因为没传值,所以为空
stu_register("Jack",32,"CN","Python")
#输出
# Jack 32 ('CN', 'Python')
```

    Alex 22 ()
    Jack 32 ('CN', 'Python')


可变参数用两种方式传入

- 直接传入，func(1, 2, 3)

- 先组装列表或元组，再通过 *args 传入，func(*[1, 2, 3]) 或 func(*(1, 2, 3))

#### 关键字参数

![title](img/arg4.jpg)

**kw - 关键字参数，可以是从零个到任意个，自动组装成字典。

「可变参数」和「关键字参数」的同异：

- 可变参数允许传入零个到任意个参数，它们在函数调用时自动组装为一个元组 (tuple)

- 关键字参数允许传入零个到任意个参数，它们在函数内部自动组装为一个字典 (dict)


```python
def stu_register(name,age,*args,**kwargs): 
    print(name,age,args,kwargs)
stu_register("Alex",22)
#输出
#Alex 22 () {}#后面这个{}就是kwargs,只是因为没传值,所以为空
stu_register("Jack",32,"CN","Python",sex="Male",province="ShanDong")
#输出
# Jack 32 ('CN', 'Python') {'province': 'ShanDong', 'sex': 'Male'}
```

    Alex 22 () {}
    Jack 32 ('CN', 'Python') {'sex': 'Male', 'province': 'ShanDong'}



```python
# 除了直接传入多个参数之外，还可以将所有参数先组装成字典 Conv，用以「**Conv」的形式传入函数
# Conv 是个字典，前面加个通配符 ** 是拆散字典，把字典的键值对传入函数中
DCF = (1, 2, 3, 4, 5)
Conv = {'dc':'act/365', 'bdc':'following'}
instrument( 'MM1001', 10, 'EUR', *DCF, **Conv )
```

#### 命名关键字参数

对于关键字参数，函数的调用者可以传入任意不受限制的关键字参数。

如果要限制关键字参数的名字，就可以用「命名关键字参数」

![title](img/arg5.jpg)


```python
print('hello', end = '')
```


```python
# 用户希望 ctp 是个关键字参数
def instrument( id, ntl=1, curR='CNY', *, ctp, **kw ):
    print( 'id:', id )
    print( 'notional:', ntl )
    print( 'reporting currency:', curR )
    print( 'counterparty:', ctp )
    print( 'keyword:', kw)
#instrument( 'MM1001', 100, 'EUR', dc='act/365', ctp='GS' )
# 使用命名关键字参数时，要特别注意不能缺少参数名。
# 如果没有写参数名 ctp， 'GS' 被当成「位置参数」
# 原函数只有 3 个位置函数，现在调用了 4 个，因此程序会报错
instrument( 'MM1001', 100, 'EUR','GS', dc='act/365' )
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-37-ae11fd8aa430> in <module>()
         10 # 如果没有写参数名 ctp， 'GS' 被当成「位置参数」
         11 # 原函数只有 3 个位置函数，现在调用了 4 个，因此程序会报错
    ---> 12 instrument( 'MM1001', 100, 'EUR','GS', dc='act/365' )
    

    TypeError: instrument() takes from 1 to 3 positional arguments but 4 were given


#### 参数组合

在 Python 中定义函数，可以用位置参数、默认参数、可变参数、命名关键字参数和关键字参数

这 5 种参数中的 4 个都可以一起使用，但是注意，参数定义的顺序必须是：

- 位置参数、默认参数、可变参数和关键字参数。

- 位置参数、默认参数、命名关键字参数和关键字参数。

要注意定义可变参数和关键字参数的语法：

- *args 是可变参数，args 接收的是一个 tuple

- **kw 是关键字参数，kw 接收的是一个 dict

命名关键字参数是为了限制调用者可以传入的参数名，同时可以提供默认值。

定义命名关键字参数不要忘了写分隔符 *，否则定义的是位置参数。

### 练习

1、写函数，计算传入字符串中【数字】、【字母】、【空格] 以及 【其他】的个数

提示：字符串的isdigit()、isalpha()、isspace()方法。

2、写函数，检查传入列表的长度，如果大于2，那么仅保留前两个长度的内容，并将新内容返回给调用者。

3、写函数，检查获取传入列表或元组对象的所有奇数位索引对应的元素，并将其作为新列表返回给调用者。

4、写函数，检查字典的每一个value的长度,如果大于2，那么仅保留前两个长度的内容，并将新内容返回给调用者。
dic = {"k1": "v1v1", "k2": [11,22,33,44]}
PS:字典中的value只能是字符串或列表

5、写函数，计算传入数字参数的和。（动态传参）

6、写函数，传入n个数，返回字典{‘max’:最大值,’min’:最小值}

## 6 匿名函数

![title](img/lambda.jpg)

解释一下函数里面的各个部分：

- lambda - 定义匿名函数的关键词。

- argument_list - 函数参数，它们可以是位置参数、默认参数、关键字参数，和正规函数里的参数类型一样。

- ：- 冒号，在函数参数和表达式中间要加个冒号。

- expression - 函数表达式，输入函数参数，输出一些值。

> **注意**： lambda 函数没有所谓的函数名 (function_header)，这也是它为什么叫匿名函数。


```python
# lambda x, y: x*y；函数输入是 x 和 y，输出是它们的积 x*y
func = lambda x, y: x*y
func(2, 3)
```




    6




```python
# lambda *args: sum(args)；输入是任意个数的参数，输出是它们的和
func = lambda *args: sum(args)
func( 1, 2, 3, 4, 5 )
```




    15




```python
# lambda **kwargs: 1；输入是任意键值对参数，输出是 1
func = lambda **kwargs: 1
func( name='Steven', age='36' )
```

> 为什么使用lambda 函数?

> Lambda函数主要在短时间内需要一个函数时才使用。当你想要将函数作为参数传递给高阶函数(即以其他函数作为参数的函数)时，通常使用这种方法。



```python
# 下面的例子演示了在其他函数中使用匿名函数
# testfunc函数传入一个参数，将它与一个未知数相乘。
def testfunc(num):
    return lambda x : x * num
result1 = testfunc(10)
result2 = testfunc(1000)
print(result1(9))
print(result2(9))
```

    90
    9000


对于 lambda 函数，我们应该避免过用 (overuse) 它或误用 (misuse) 它：
* 误用情况：如果用 lambda 函数只是为了赋值给一个变量，用 def 的正规函数。
* 过用情况：如果一个函数很重要，它需要一个正规的名字。

## 7 高阶函数

高阶函数 (high-order function) 在函数化编程 (functional programming) 很常见，主要有两种形式：

* 参数是函数 (map, filter, reduce)

* 返回值是函数 (closure, partial, currying)

#### Map, Filter, Reduce

Python 里面的 map, filter 和 reduce 属于第一种高阶函数，参数是函数。

首先看看 map, filter 和 reduce 的语法：

* map(函数 f, 序列 x)：对序列 x 中每个元素依次执行函数 f，将 f(x) 组成一个「map 对象」返回 (可以将其转换成 list 或 set)

* filter(函数 f, 序列 x)：对序列 x 中每个元素依次执行函数 f，将 f(x) 为 True 的结果组成一个「filter 对象」返回 (可以将其转换成 list 或 set)

* reduce(函数 f, 序列 x)：对序列 x 的第一个和第二个元素执行函数 f，得到的结果和序列 x 的下一个元素执行函数 f，一直遍历完的序列 x 所有元素。


```python
# 用 map 函数对列表每个元素平方
lst = (1, 2, 3, 4, 5)
map_iter = map( lambda x: x**2, lst )
print( map_iter )
print( list(map_iter) )
```

    <map object at 0x7f8ead10bd68>
    [1, 4, 9, 16, 25]


在 map 函数中

* 第一个参数是一个计算平方的「匿名函数」
* 第二个参数是列表，即该「匿名函数」作用的对象

>注意 map_iter 是 map 函数的返回对象 (它是一个迭代器)，想要将其内容显示出来，需要用 list 将其转换成「列表」形式。


```python
#  filter 函数，顾名思义就是筛选函数
# 使用filter 函数把刚才列表中的奇数筛选出来
filter_iter = filter(lambda n: n % 2 == 1, lst)
print( filter_iter )
print( list(filter_iter) )
```

    <filter object at 0x10aab0e80>
    [1, 3, 5]


在 filter 函数中

* 第一个参数是一个识别奇数的「匿名函数」
* 第二个参数是列表，即该「匿名函数」作用的对象

>同样，filter_iter 作为 filter 函数的返回对象，也是一个迭代器，想要将其内容显示出来，需要用 list 将其转换成「列表」形式。




```python
# reduce 函数，顾名思义就是累积函数
# 用reduce 函数把一组数减少 (reduce) 到一个数
from functools import reduce
reduce( lambda x,y: x*y, lst )
```




    120



在 reduce 函数中

* 第一个参数是一个求和相邻两个元素的「匿名函数」
* 第二个参数是列表，即该「匿名函数」作用的对象

在 reduce 函数的第三个参数还可以赋予一个初始值：


```python
reduce( lambda x,y: x+y, lst, 100 )
```




    115



#### 闭包 (closure)

Python 里面的闭包 (closure) 属于第二种高阶函数，返回值是函数。下面是一个闭包函数：


```python
def make_counter(init):
    counter = [init]
    
    def inc(): counter[0] += 1
    def dec(): counter[0] -= 1
    def get(): return counter[0]
    def reset(): counter[0] = init
        
    return inc, dec, get, reset
```

此函数的作用是做一个计数器，可以：

* 用增加子函数 inc() 加一秒
* 用减少子函数 dec() 减一秒
* 用获取子函数 get() 看秒数 
* 用重置子函数 reset() 回原点


```python
inc, dec, get, reset = make_counter(0)
inc()
inc()
inc()
get()
```




    3




```python
dec()
get()
```




    2




```python
reset()
get()
```




    0



属于第二类 (返回值是函数) 的高阶函数还有「偏函数」和「柯里化」

## 8 解析式

### 8.1 框架

解析式（comprehension）是将一个**可迭代对象**转换成另一个**可迭代对象**的工具。

>容器类型数据（str、tuple、list、dict、set）都是可迭代对象。

* 第一个可迭代对象：可以使任何容器类型数据。
* 第二个可迭代对象：取决于什么类型的解析式：
  * 列表解析式：可迭代对象是list
  * 字典解析式：可迭代对象是dict
  * 集合解析式：可迭代对象是set


```python
# list comprehension
[值 for 元素 in 可迭代对象 if 条件]
# dict comprehension
{键值对 for 元素 in 可迭代对象 if 条件}
# set comprehension
{值 for 元素 in 可迭代对象 if 条件} 
```




    complex



这些解析式都有：
* for...in...：for循环
* if：if条件
解析式就是为了把「带条件的for循环」简化成一行代码的。

### 8.2 列表解析式

问题：如何从一个整数列表中把奇数筛选出来再乘以2？


```python
# 用带if的for循环
lst = [1, 2, 3, 4, 5]
odds = []
for n in lst:
    if n % 2 == 1:
        odds.append(n*2)
odds
```




    [2, 6, 10]




```python
# 用列表解析式
lst = [1, 2, 3, 4, 5]
odds = [n*2 for n in lst if n % 2 == 1]
odds
```

列表解析式只用一行代码就解决问题了，但似乎不直观，我们分析一下：

![title](img/01.jpg)

可以把「for 循环」到「解析式」的过程想像成一个「复制-粘贴」的过程：

1.将「for 循环」的新列表复制到「解析式」里

2.将 append 里面的表达式 n * 2 复制到新列表里

3.复制循环语句 for n in lst 到新列表里，不要最后的冒号

4.复制条件语句 if n%2 == 1 到新列表里，不要最后的冒号

把上面具体的例子推广到一般的例子，从「for 循环」到「列表解析式」的过程如下：

![title](img/02.jpg)

### 8.3 其他解析式

我们可以把「列表解析式」那一套举一反三的用到其他解析式上，用下面两图理解一下「字典解析式」和「集合解析式」。

![title](img/03.jpg)

![title](img/04.jpg)

前面我们说过“ Python 不建议使用 map 和 filter。而是用「解析式」优雅地替代 map 和 filter 。”

我们来看看为什么：


```python
#「列表解析式」实现「在列表中先找出奇数再乘以 2」
[ n*2 for n in lst if n%2 == 1]
#「map/filter」实现「在列表中先找出奇数再乘以 2」
list( map(lambda n: n*2, filter(lambda n: n%2 == 1, lst)) )
```

实例：用解析式将二维元组里每个元素提取出来并存储到一个列表中。


```python
tup = ((1, 2, 3), (4, 5, 6), (7, 8, 9))
```

先遍历第一层元组，用 for t in tup，然后遍历第二层元组，用 for x in t，提取每个 x 并"放在“列表中，用 [ ]。

代码如下：


```python
flattened = [x for t in tup for x in t]
flattened
```

![title](img/05.jpg)

## 总结

函数包括**正规函数 (用 def) **和**匿名函数 (用 lambda)**，函数的参数形态也多种多样，有位置参数、默认参数、可变参数、关键字参数、命名关键字参数。

匿名函数主要用在**高阶函数**中，高阶函数的参数可以是函数 (Python 里面内置 map/filter/reduce 函数)，返回值也可以是参数 (闭包、偏函数、柯里化函数)。

**解析式**并没有解决新的问题，只是以一种更加简洁，可读性更高的方式解决老的问题。解析式可以把「带 if 条件的 for 循环」用一行程序表达出来，也可以实现 map 加 filter 的功能。


```python
# here is a mostly-straightforward solution to the
# two-by-two version of the grid.

def do_twice(f):
    f()
    f()

def do_four(f):
    do_twice(f)
    do_twice(f)

def print_beam():
    print('+ - - - -', end=' ')

def print_post():
    print('|        ', end=' ')

def print_beams():
    do_twice(print_beam)
    print('+')

def print_posts():
    do_twice(print_post)
    print('|')

def print_row():
    print_beams()
    do_four(print_posts)

def print_grid():
    do_twice(print_row)
    print_beams()

print_grid()
```

    + - - - - + - - - - +
    |         |         |
    |         |         |
    |         |         |
    |         |         |
    + - - - - + - - - - +
    |         |         |
    |         |         |
    |         |         |
    |         |         |
    + - - - - + - - - - +



```python
def one_four_one(f, g, h):
    f()
    do_four(g)
    h()

def print_plus():
    print('+', end=' ')

def print_dash():
    print('-', end=' ')

def print_bar():
    print('|', end=' ')

def print_space():
    print(' ', end=' ')

def print_end():
    print()

def nothing():
    "do nothing"

def print1beam():
    one_four_one(nothing, print_dash, print_plus)

def print1post():
    one_four_one(nothing, print_space, print_bar)

def print4beams():
    one_four_one(print_plus, print1beam, print_end)

def print4posts():
    one_four_one(print_bar, print1post, print_end)

def print_row():
    one_four_one(nothing, print4posts, print4beams)

def print_grid():
    one_four_one(print4beams, print_row, nothing)

print_grid()
```

    + - - - - + - - - - + - - - - + - - - - + 
    |         |         |         |         | 
    |         |         |         |         | 
    |         |         |         |         | 
    |         |         |         |         | 
    + - - - - + - - - - + - - - - + - - - - + 
    |         |         |         |         | 
    |         |         |         |         | 
    |         |         |         |         | 
    |         |         |         |         | 
    + - - - - + - - - - + - - - - + - - - - + 
    |         |         |         |         | 
    |         |         |         |         | 
    |         |         |         |         | 
    |         |         |         |         | 
    + - - - - + - - - - + - - - - + - - - - + 
    |         |         |         |         | 
    |         |         |         |         | 
    |         |         |         |         | 
    |         |         |         |         | 
    + - - - - + - - - - + - - - - + - - - - + 



```python
def even_items(seq):
    return seq[1::2]
print(even_items([1,2,3,4,5,6,7]))
```

    [2, 4, 6]



```python
def my_sum(*num):
    return sum(num)
out = my_sum(1, 2, 3, 4)
print(out)
```

    10


## 内置函数


```python
abs # 求绝对值 

all #Return True if bool(x) is True for all values x in the iterable.If the iterable is empty, return True.

any #Return True if bool(x) is True for any x in the iterable.If the iterable is empty, return False.

ascii #Return an ASCII-only representation of an object,ascii(“中国”) 返回”‘\u4e2d\u56fd’”

bin #返回整数的2进制格式 

bool # 判断一个数据结构是True or False, bool({}) 返回就是False, 因为是空dict

bytearray # 把byte变成 bytearray, 可修改的数组

bytes # bytes(“中国”,”gbk”) 

callable # 判断一个对象是否可调用 

chr # 返回一个数字对应的ascii字符 ， 比如chr(90)返回ascii里的’Z’

classmethod #面向对象时用，现在忽略

compile #py解释器自己用的东西，忽略

complex #求复数，一般人用不到

copyright #没用

credits #没用

delattr #面向对象时用，现在忽略

dict #生成一个空dict

dir #返回对象的可调用属性

divmod #返回除法的商和余数 ，比如divmod(4,2)，结果(2, 0) 

enumerate #返回列表的索引和元素，比如 d = [“alex”,”jack”]，enumerate(d)后，得到(0, ‘alex’) (1, ‘jack’)

eval #可以把字符串形式的list,dict,set,tuple,再转换成其原有的数据类型。 

exec #把字符串格式的代码，进行解义并执行，比如exec(“print(‘hellworld’)”)，会解义里面的字符串并执行

exit #退出程序

filter #对list、dict、set、tuple等可迭代对象进行过滤， filter(lambda x:x>10,[0,1,23,3,4,4,5,6,67,7])过滤出所有大于10的值

float #转成浮点

format #没用

frozenset #把一个集合变成不可修改的

getattr #面向对象时用，现在忽略

globals #打印全局作用域里的值 

hasattr #面向对象时用，现在忽略

hash #hash函数

help 

hex #返回一个10进制的16进制表示形式,hex(10) 返回’0xa’

id #查看对象内存地址

input 

int

isinstance #判断一个数据结构的类型，比如判断a是不是fronzenset, isinstance(a,frozenset) 返回 True or False

issubclass #面向对象时用，现在忽略

iter #把一个数据结构变成迭代器，讲了迭代器就明白了

len

list

locals

map # map(lambda x:x**2,[1,2,3,43,45,5,6,]) 输出 [1, 4, 9, 1849, 2025, 25, 36]

max # 求最大值 

memoryview # 一般人不用，忽略 

min # 求最小值 

next # 生成器会用到，现在忽略 

object #面向对象时用，现在忽略

oct # 返回10进制数的8进制表示

open 

ord # 返回ascii的字符对应的10进制数 ord(‘a’) 返回97，

print

property #面向对象时用，现在忽略

quit

range 

repr #没什么用

reversed # 可以把一个列表反转

round #可以把小数4舍5入成整数 ，round(10.15,1) 得10.2

set

setattr #面向对象时用，现在忽略

slice # 没用

sorted 

staticmethod #面向对象时用，现在忽略

str

sum #求和,a=[1, 4, 9, 1849, 2025, 25, 36],sum(a) 得3949

super #面向对象时用，现在忽略

tuple 

type 

vars #返回一个对象的属性，面向对象时就明白了

zip #可以把2个或多个列表拼成一个， a=[1, 4, 9, 1849, 2025, 25, 36]，b = [“a”,”b”,”c”,”d”]，
```


```python

```
