# Number 数字

-------------------------------------------------------------------

在编程中，常使用数字来记录游戏得分、表示可视化数据、存储Web应用信息等。Python根据数字的用法以不同的方式处理它们。

Python支持四种不同的数字类型：
- int 有符号整型
- long 长整型，也可代表八进制和十六进制
- float 浮点型
- complex 复数

一些数值类型的实例：
| int | long | float | complex |
| :--- | :--- | :--- | :--- |
| 10 | 515924361L | 0.0 | 3.14j|
| 100 | -0x19323L | 15.20 | 45.j |
| -786 | 0122L | -21.9 | 9.322e-36j |
| 080 | 0xDEFABCECBDAECBFBAEl | 32.3e+18 | .876j |
| -0490 | 535633629843L | -90. | -.6545+0J |
| -0x260 | 	-052318172735L | -32.54e100 | 3e+26J |
| 0x69 | -4721885298529L | 70.2E-12 | 4.53e-7j |

- Python复数除了a+bj的形式，也可使用complex(a,b)来表示
- Python3.x版本中移除了long类型，使用int替代
- 进制前缀：

| 进制 | 英文 | 范围 | 前缀 | 后缀 |
| :--| :-- | :-- | :-- | :-- |
|二进制 | Binary | 0-1 | 0B | B |
|八进制 | Octal | 0-7 | 0O,也可以使用空格加上0 即:" 0" | O |
|十进制 | Decimal | 0-9 | 无 | D |
|十六进制 | Hexadecimal | 0-9,A-F | 0x | H |

- e或E(exponent)为科学计数法表示，其表示以10为底的底数，aeb中a为float类型，b为int类型，如3.2e+2表示' 3.2 x 10^2 '
- 复数的实部和虚部都是浮点型


```python
>>>print(0B0100010101)

277
``` 


```python
>>>print(0O76)

62
```

```python
>>>print(1E-12)

1e-12
```
    

## 1 int 整型

-------------------------------------------------------------------

指定一个值时，Number对象被创建


```python
>>>var1 = 1
>>>var2 = 2
>>>print(var1,var2)

 1 2
```
    
可以使用del语句删除一些对象的引用，其基本语法为：
```python
    del var1
    del var1, var2
```


```python
>>>del var1
>>>var1

---------------------------------------------------------------------------
    NameError                                 Traceback (most recent call last)

    Cell In[6], line 1
    ----> 1 del var1
          2 var1
    

    NameError: name 'var1' is not defined
```

## 2 浮点数

-------------------------------------------------------------------

Python将带小数点的数字都称为**浮点数**，小数点可出现在数字的任何位置，包括首位数字前，整数部分默认为0。


```python
>>>0.2 + 0.1

0.30000000000000004
```

```python
>>>3 * 0.1

0.30000000000000004
```

出现这一现象的原因与计算机内部存储浮点数的方式有关：
- 计算机将所有数据以二进制的形式存储
- 计算机用有限的大小来存储数据（因为现实生活中不存在无限大的内存或硬盘）

计算机如何存储0.1和0.2？

![示例图片](..\images\二进制数据存储.png)

十进制的 0.1 转为二进制，得到一个无限循环小数：0.00011…。
也就是说，二进制无法「用有限的位数」来表示 0.1。对于 0.2 也是一样的，不赘述。二进制能「用有限的位数」表示的有：0.5、0.25、0.125 等（可以由2的负整数幂直接相加得到的数）。

**所以当我们计算 0.1 + 0.2 时，实际上算的是两个近似值相加，得到的值当然也是近似等于 0.3。**

# 3 数值计算

------

在Python中可以对数值对象进行各类运算：

```
print (5 + 4)  # 加法   输出 9
print (4.3 - 2) # 减法   输出 2.3
print (3 * 7)  # 乘法  输出 21
print (2 / 4)  # 除法，得到一个浮点数    输出 0.5
print (2 // 4) # 除法，得到一个整数 输出 0
print (17 % 3) # 取余   输出 2
print (2 ** 5) # 乘方  输出 32
```

需要更多数值运算方法时，可以使用math模块，其中提供了许多浮点数的运算函数

[上一篇(1_Variable)](./1_Variable.md) \| [下一篇(3_String)](./3_String.md)