# 函数

----------------------------

函数的基本结构：

**函数定义:**  def function_name(): 使用关键字```def```开始，后跟函数名和括号内的形参列表，以冒号结尾，函数语句从下一行开始，并且必须缩进。

**文档字符串** 也称docstring，文档字符串是函数定义中的注释，用于描述函数的功能、参数、返回值等信息，通常以""""""括住，利用文档字符串可以自动生成在线文档或打印版文档，还可以让开发者在浏览代码时直接查阅文档。
    
**函数体** 
    
**函数调用** 通过调用函数名让Python执行函数体中的代码


-----------------
```python
def 变量名(形参列表，包括位置实参和关键字实参):
    """文档字符串"""
    函数体代码块
    (return *)

函数调用
```
-----------------
下面我们来详细阐述和分析以上四种形式：

## 1 函数定义

❗在定义函数时，要注意函数名不能和python保留字或已有函数名冲突


```python
# 一个简单的实例
def greet_user():
    """显示简单的问候语"""
    print("Hello!")
    
greet_user()

Hello!
```


```python
# 向函数传递信息
def greet_user(username):
    """显示简单的问候语"""
    print("Hello! " + username.title() + '.')
    
greet_user('jessica')


Hello! Jessica.
```


```python
# 下面创建一个可以输出限定数值内的斐波那契数列的函数：
def fib(n): 
    """输出n以内的斐波那契数列"""
    a, b = 0, 1
    while a < n:
        print(a,end=' ')
        a, b = b, a + b

fib(100)


0 1 1 2 3 5 8 13 21 34 55 89 
```


### 1.1 实参和形参

在函数greet_user(username)中，变量username是一个**形参**----函数完成其工作所需要的一项信息。在代码```greeet_user('jessica')```中，值'jessica'是一个**实参**，实参是调用函数时传递给函数的信息。

### 1.2 传递实参

函数定义中可能包含多个形参，因此函数调用时也可能包含多个实参，向函数传递实参的方式很多：

- 位置实参：要求实参的顺序与形参的顺序相同

- 关键字实参：其中的每个实参都由变量名和值组成

- 默认值参数

- 列表和字典

#### 1.2.1 位置实参


```python
def describe_pet(animal_type, pet_name): # 注意形参的顺序
    """显示宠物的信息"""
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name is " + pet_name.title() + ".")
    
describe_pet('hamster', 'harry') # 调用时按照形参的顺序
describe_pet('dog', 'Peter')

I have a hamster.
My hamster's name is Harry.

I have a dog.
My dog's name is Peter.
```


#### 1.2.2 关键字实参

kwarg=value 形式的```关键字参数```也可以用于调用函数。函数调用时，关键字参数必须跟在位置参数后面。所有传递的关键字参数都必须匹配一个函数接受的参数，关键字参数的顺序并不重要。这也包括必选参数。不能对同一个参数多次赋值。


```python
# 关键字实参
describe_pet(animal_type='dog', pet_name='peter') # 实参的顺序不影响函数的调用结果
describe_pet(pet_name='peter', animal_type='dog')

I have a dog.
My dog's name is Peter.

I have a dog.
My dog's name is Peter.
```



#### 1.2.3 默认值实参

在函数定义时，可给每个形参指定默认值，在调用函数时提供了实参时，将使用指定的实参值，否则将使用默认值。为参数指定默认值是非常有用的方式。调用函数时，可以使用比定义时更少的参数。**使用默认值时，必须在形参列表中先列出没有默认值的形参，再列出有默认值的形参，保证Python能正确的读取位置实参**


```python
def describe_pet(pet_name, animal_type='dog'):
    """显示宠物信息"""
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name is " + pet_name.title() + ".")
    
describe_pet('whille')


I have a dog.
My dog's name is Whille.
```


❗默认值在```定义```作用域里的函数定义中求值。即默认参数的值是在函数定义时确定的，而不是在函数调用时确定的。下例中，函数f的默认值参数arg被设置为i的当前值，即5。当调用函数f时，arg的值被打印出来。即使在调用函数前将i的值更改为6，函数f的默认参数仍然是5。通过id()方法，方便我们理解下例：

可以发现，原始变量i的地址与函数中参数arg的地址相同，即函数定义时，关键字参数arg的值指向的是原始变量i的地址。在函数中对变量i做+10的操作后打印地址，发现其地址发生变化，且在函数外无法找到函数内的i。在调用函数前，对i重新赋值为6，打印其地址发现与原始的变量i地址不同。


```python
i = 5
print("original i's id: ", id(i))

def f(arg=i):
    print("arg's id: ", id(arg))
    i = arg + 10
    print("i's id in function: ", id(i))
    print(arg)

i = 6
print("latter i's id: ", id(i))
f()

original i's id:  140705923371944
latter i's id:  140705923371976
arg's id:  140705923371944
i's id in function:  140705923372264
5
```

❗尽管默认值只计算一次。默认值为列表、字典或类实例等可变对象时，会产生与该规则不同的结果。例如：

同样使用观察id的方法分析下例，在函数体内循环打印参数L的地址，发现在多次调用中，L指向的地址都不变，因为L.append(a)语句修改该地址存储的列表值，因此只要函数不被重新定义，那么每次调用都会累积之前的调用结果。


```python
def f(a, L=[]):
    print(id(L))
    L.append(a)
    return L

print(f(1))
print(f(2))
print(f(3))

1623407675200
[1]
1623407675200
[1, 2]
1623407675200
[1, 2, 3]
```


这是因为在函数定义时，列表L被赋予了一个默认值[]，当函数被调用时，若没有提供L的实参，将使用默认值[]，由于默认值在函数定义时只被计算一次，所以每次调用函数时，都会使用同一个列表L，因此，当多次调用函数f时，每次调用都会修改同一个列表L，导致结果累积了之前的调用结果。

#### 1.2.4 列表和字典

```python
def function(*args,**kwargs):
```

一、任意实参列表

```python
def make_pizza(*tippings):
    print(tippings)
    
make_pizza('mushrooms', 'greeen peppers', 'extra cheese')


('mushrooms', 'greeen peppers', 'extra cheese')
```

形参名```*tippings```中的星号让python创建一个名为tippings的```空元组```，并将所有收到的值都存入这个空元组中。在结合使用位置实参和任意数量实参时，必须在函数定义中将接纳任意数量的实参的形参放在位置形参之后，python先匹配位置实参和关键字实参，再将余下的实参都收集到最后一个形参中。```*args```形参后的任何形式参数只能是仅限关键字参数，即只能用作关键字参数，不能用作位置参数。

**解包**实参列表：

函数调用要求独立的位置参数，但实参在列表或元组里时，要执行相反的操作。例如，内置的 range() 函数要求独立的 start 和 stop 实参。如果这些参数不是独立的，则要在调用函数时，用```*```操作符把实参从列表或元组解包出来：


```python
list(range(3, 6))            # normal call with separate arguments

args = [3, 6]
list(range(*args))            # call with arguments unpacked from a list


[3, 4, 5]
```




二、任意实参字典


```python
def build_profile(first, last, **user_info):
    """创建一个字典，其中包含我们知道的有关用户的一切"""
    profile = {}
    profile['first_name'] = first
    profile['last_name'] = last
    for key,value in user_info.items():
        profile[key] = value
    return profile

user_profile = build_profile('albert', 'einstein',location='princeton', field='physics')
print(user_profile)

{'first_name': 'albert', 'last_name': 'einstein', 'location': 'princeton', 'field': 'physics'}
```


形参```**user_info```中的两个星号让Python创建一个名为user_info的```空字典```，并将收到的所有名称-值对都封装到这个字典中。

同一，我们可以用```**```操作符解包实参字典：


```python
def parrot(voltage, state='a stiff', action='voom'):
    print("-- This parrot wouldn't", action, end=' ')
    print("if you put", voltage, "volts through it.", end=' ')
    print("E's", state, "!")

d = {"voltage": "four million", "state": "bleedin' demised", "action": "VOOM"}
parrot(**d)

-- This parrot wouldn't VOOM if you put four million volts through it. E's bleedin' demised !
```

#### 1.2.5 限制参数传递

默认情况下，参数可以按位置或显式关键字传递给 Python 函数。为了让代码易读、高效，最好限制参数的传递方式，这样，开发者只需查看函数定义，即可确定参数项是仅按位置、按位置或关键字，还是仅按关键字传递。

```
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        Positional or keyword   |
        |                                - Keyword only
         -- Positional only
```

```/```和```*```是可选的。这些符号表明形参如何把参数值传递给函数：位置、位置或关键字、关键字。关键字形参也叫作命名形参。函数定义中未使用```/```和```*```时，参数可以按位置或关键字传递给函数。

- 仅限位置参数：特定形参可以标记为 仅限位置。仅限位置 时，形参的顺序很重要，且这些形参不能用关键字传递。仅限位置形参应放在```/```（正斜杠）前。```/```用于在逻辑上分割仅限位置形参与其它形参。如果函数定义中没有```/```，则表示没有仅限位置形参。```/```后可以是位置或关键字或仅限关键字形参。

- 仅限关键字参数：把形参标记为仅限关键字，表明必须以关键字参数形式传递该形参，应在参数列表中第一个仅限关键字 形参前添加```*```。

🚀函数内变量的调用规则：

函数在执行时使用函数局部变量符号表，所有函数变量赋值都存在局部符号表中。引用变量时，首先在局部符号表里查找变量；然后是外层函数局部符号表；再是全局符号表，最后是内置名称符号表。因此，尽管可以引用全局变量和外层函数的变量，但最好不要在函数内直接赋值，除非是```global```语句定义的全局变量，或```nonlocal```语句定义的外层函数变量。

在调用函数时，会将实参引入到被调用函数的局部符号表中，因此，实参是使用**按值调用**来传递的，其中值始终是对象的引用而不是对象的值，当一个函数调用另外一个函数时，会为该调用创建一个新的局部符号表。

函数定义在当前符号表中把函数名与函数对象关联在一起。解释器把函数名指向的对象作为用户自定义函数。还可以使用其他名称指向同一个函数对象，并访问该函数：

#### 1.2.6 Lambda表达式

```lambda```关键字用于创建小巧的```匿名函数```。lambda a, b: a+b 函数返回两个参数的和，即冒号```:```前为匿名函数的接收参数，冒号后为其返回值。Lambda 函数可用于任何需要函数对象的地方。在语法上，匿名函数只能是单个表达式。在语义上，它只是常规函数定义的```语法糖```。与嵌套函数定义一样，lambda 函数可以引用包含作用域中的变量：


```python
def make_incrementor(n):
    return lambda x: x + n

f = make_incrementor(42)
print(f)
f(0)
f(1)

<function make_incrementor.<locals>.<lambda> at 0x00000179FA658C20>

43
```


make_incrementor()函数返回的是一个```闭包函数```（函数对象，从print(f)的结果可以看出），该闭包函数可以在每次调用时将传入的参数x与外部参数n相加并返回结果。


```python
pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
pairs.sort(key=lambda pair: pair[1])
pairs


<function <lambda> at 0x00000179F8416AC0>
[(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]
```

😐以上代码是个有趣的用例，如何按照元素的第二个索引来重新排列该列表呢？

为了解决这个问题，我们先看sort函数的参数key：参数key用于指定一个可调用对象（函数、lambda表达式等，其实这二者等价），用于从可迭代对象（待排序的列表）中的每一个元素中提取一个用于比较的键，在排序的过程中，根据这个键对元素进行比较，而不是直接比较元素本身。具体来说，当使用sort()函数对一个列表进行排序时，可以通过key参数指定一个函数，该函数将应用于列表中的每个元素，并返回一个用于比较的键。我们再举一例：

```python
# 按字符串长度重排
names = ['Alice', 'Bob', 'Charlie', 'David']
names.sort(key=len)
print(names)

['Bob', 'Alice', 'David', 'Charlie']
```

返回上例，了解了参数key，我们距离完成重排只剩下一个问题：如何定义一个接收列表，返回其第二个元素的函数？当然我们可以通过def function_name()的方式来定义，如果用lambda语法呢？结果就是```lambda pair:pair[1]```

验证可得：
```python
f = lambda pair:pair[1]
f((0,1))

1
```

### 1.3 函数注解

```函数注解```是可选的用户自定义函数类型的元数据完整信息（详见```PEP 3107```和```PEP 484```）。

标注 以字典的形式存放在函数的```__annotations__```属性中而对函数的其他部分没有影响。 形参标注的定义方式是在形参名后加冒号```:```，后面跟一个会被求值为标注的值的表达式。 返回值标注的定义方式是加组合符号 ```->```，后面跟一个表达式，这样的校注位于形参列表和表示 def 语句结束的冒号。 下面的示例有一个必须的参数、一个可选的关键字参数以及返回值都带有相应的标注:


```python
def f(ham: str, eggs: str = 'eggs') -> str:
    print("Annotations:", f.__annotations__)
    print("Arguments:", ham, eggs)
    return ham + ' and ' + eggs

f('spam')

Annotations: {'ham': <class 'str'>, 'eggs': <class 'str'>, 'return': <class 'str'>}
Arguments: spam eggs

'spam and eggs'
```


## 2 文档字符串

### 2.1 文档字符串的内容和格式规定：

第一行为对象用途的简短摘要。为保持简介，不要在这里显式的说明对象名或类型，因为可通过其他方式获取这些信息，这一行一般以大写字母开头，以句点结尾。

文档字符串为多行时，第二行应为空白行，将摘要与其余描述分开，后面行可包含若干段落，描述对象的调用约定、副作用等。

Python 解析器不会删除 Python 中多行字符串字面值的缩进，因此，文档处理工具应在必要时删除缩进。这项操作遵循以下约定：文档字符串第一行 之后 的第一个非空行决定了整个文档字符串的缩进量（第一行通常与字符串开头的引号相邻，其缩进在字符串中并不明显，因此，不能用第一行的缩进），然后，删除字符串中所有行开头处与此缩进“等价”的空白符。不能有比此缩进更少的行，但如果出现了缩进更少的行，应删除这些行的所有前导空白符。转化制表符后（通常为 8 个空格），应测试空白符的等效性。


```python
# 多行文档字符串例，可自行调整隔行缩进观察效果
def docstring_test():
    """This function do nothing

    Yes, it doesn't do anything fun
    NO, i don't think so
    """
    pass

print(docstring_test.__doc__)

This function do nothing

    Yes, it doesn't do anything fun
    NO, i don't think so
```

### 2.2 文档字符串的提取方式：

- 1.使用```__doc__```属性：在Python中，每个函数对象都有一个__doc__属性，该属性存储着函数的文档字符串，可以通过访问函数的__doc__属性来提取文档字符串。

- 2.使用```pydoc```工具库：pydoc是Python的一个标准库，可以用于生成文档。可以在命令行中使用pydoc命令来查看函数的文档字符串。如：
    
        ```pydoc module_name.function_name```

- 3.使用Sphinx工具库：Sphinx是一个功能强大的文档生成工具，可以用于生成丰富的文档，通过在代码中使用特定的注释格式，结合Sphinx命令行工具，可以生成包括函数文档字符串在内的详细文档。具体使用方法可以参考Sphinx官方文档。

## 3 返回值

函数并非总是直接显示输出，相反，它可以处理一些数据，返回一个或一组值。函数返回的值被称为**返回值**，在函数中，可使用return语句将值返回到调用函数的代码行。返回值能够让你将程序的大部分繁重工作移到函数中去完成，从而简化主程序。


```python
# 返回简单值
def get_formatted_name(first_name, last_name):
    """返回整洁的姓名"""
    full_name = first_name + ' ' + last_name
    return full_name.title()

name = get_formatted_name('lewies', 'hr')
print(name)

Lewies Hr
```

## 5 函数调用

1. 等效的函数调用：鉴于可混合使用位置实参、关键字实参和默认值，通常有多种等效的函数调用方式；

2. 避免实参错误：警惕出现实参不匹配的错误！

## 6 将函数存储在模块中

函数的优点之一：可以使用他们将代码块与主程序分离；通过给函数指定描述性名称，可让主程序容易理解得多。更进一步，将函数存储在被称为**模块**（模块是拓展名为.py的文件）的独立文件中，再将模块导入到主程序中。import语句允许在当前运行的程序文件中使用模块中的代码。

导入方法1： 只需编写一条import语句并在其中指定模块名，就可在程序中使用该模块中的所有函数，使用时需要将模块名和函数名用.连接

导入方法2： 导入特定的函数语法： from module_name import function_1, function_2, function_3，若使用这种方法，调用函数时就无需使用句点

导入时as的用法：

- 使用as给函数指定别名： from pizza import make_pizza as mp
- 使用as给模块指定别名： import pizza as p
- 导入模块中的所有函数： from pizza import *， 然而在使用并非自己编写的大型模块时，最好不用这种方法，如果模块中有函数的名称与你的项目中使用的名称相同，可能导致意想不到的结果，python可能遇到多个名称相同的函数或变量，进而覆盖函数，而不是分别导入所有函数