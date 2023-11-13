# 1 变量

--------------------------------------------------

变量是计算机存储在内存中的值，变量名是该值的抽象表述，在创建变量时，会在内存中开辟一个空间，基于变量的数据类型，解释器会分配指定内存，并决定存储什么样的数据在内存中。变量可以指定不同的数据类型，包括整数、浮点数及字符。

## 1.1 变量的命名和使用规范：
- 1.变量名只能包含```字母```、```数字```和```下划线```。变量名可以字母或下划线打头，但不能以数字打头；
- 2.变量名不能包含空格，但可使用下划线来分隔其中的单词；
- 3.不可将Python关键字和函数名作变量名，即不要使用Python的保留字；
- 4.变量名应既简短又具有描述性；
- 5.慎用小写字母l和大写字母O，可能被误读为数字1和0；

## 1.2 变量赋值

python属于强类型语言，即需要显式的转换变量类型(如a = 1, b = str(a))，否则该变量将保持其原本的类型。但python变量在创建时并不需要指定类型，其类型取决于赋给它的值是何种类型。这种变量本身类型不固定的语言称之为动态语言，与之对应的就是静态语言。静态语言在定义变量时必须指定变量类型，如果赋值的时候类型不匹配，就会报错。

python中，等号“=”是赋值语句，可以把任意类型的数据赋值给变量，同一个变量可以反复赋值，而且可以是不同类型的变量。


```python
# 单变量赋值

a = 123 # a 为整型数据
b = 'abc' # b 为字符串数据
```


```python
# 多变量赋值

a = b = c = 1
```


```python
# 为多个变量指定多个值

a, b, c = 1, 2, 3
```


```python
# 常量，常常将认为固定不变的量（如数学中的Π）用大写的变量名表示

PI = 3.14
```

## 1.3 变量关系判断

如何判断两个变量是否指向同一对象？

在Python中，每个对象都有一个唯一的标识符，可以通过内置函数id()来获取。当两个变量使用is运算符进行比较时，实际上是在比较它们的标识符是否相同。

如果a is b返回True，表示a和b指向同一个对象；如果返回False，表示a和b指向不同的对象。

需要注意的是，is运算符比较的是对象的标识符，而不是对象的值。即使两个对象的值相同，但它们可能是不同的对象，所以a is b可能为False。


```python
>>>a = 0.1
>>>b = 0.1
>>>print(id(a))
>>>print(id(b))
>>>print(a == b)
>>>print(a is b)

2623612757168
2623612756944
True
False
```


    


```python
>>>a = 0.1
>>>b = a
>>>print(a == b)
>>>print(a is b)

True
True
```


## 1.4 变量使用错误

使用变量时需要注意的常见错误：

- 使用变量前忘记给它赋值（NameError: name 'xxx' is not defined）

- 输入变量名时拼写不正确（善用自动补全）

# 2 数据类型简述

--------------------------------------------------

python包含6种标准的数字类型:


    不可变数据：Number（数字）、String（字符串）、Tuple（元组）
    
    可变数据：List（列表）、Sets（集合）、Dictionary（字典）

    以及布尔值：Bool

## 2.1 变量类型判断方式：

- type()函数

```python
>>> a, b, c, d = 11, 3.3, True, 1+2j
>>> print(type(a), type(b), type(c), type(d))

<class 'int'> <class 'float'> <class 'bool'> <class 'complex'>
```

- isinstance函数
```python
>>> a = 111
>>> isinstance(a, int)

True
```

isinstance 和 type 的区别在于：

    type()不会认为子类是一种父类类型。
    isinstance()会认为子类是一种父类类型。


[下一篇(2_Number)](./2_Number.md)