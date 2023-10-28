# IF语句

if语句用于检查程序的当前状态

# 1 条件测试

每条if语句的核心都是一个值为True或False的表达式，这种表达式被称为**条件测试**，Python根据条件测试的值为True还是False来决定是否执行if语句中的代码。如果条件测试的值为True，Python就执行紧跟在if语句后面的代码；否则忽略这些代码。


```python
# 1. 检查是否相等： a == b ? 若元素类型为字符串，那么python在检测是否相等时区分大小写。
# 2. 检测是否不相等： 若要判断两个值是否不等，可使用 ！= 符号判断， a ！= b
# 3. 比较数字
# 4. 检查多个条件：
#     4.1 使用and检查多个条件
>>>age = 18 
>>>age >= 20 and age <= 24
#     4.2 使用or检查多个条件
>>>age <= 20 or age >= 24
# 5. 检查特定值
#     5.1 检查特定值是否包含在列表中可使用关键字in：if a in list(a):
>>>3 in [1, 2, 3]
#     5.2 检查特定值是否不包含在列表中可使用关键字not in： if a not in list(a)
>>>3 not in [1, 2, 3]
# 6. 布尔表达式：条件测试的别名，与条件表达式一样，布尔表达式的结果要么为True，要么为False
```



# 2 简单的if语句

- 最简单的if语句：


```python
# 最简单的if语句只有一个测试和一个操作：
#if conditional_tset:
#    do something
```

- if-else语句：


```python
# 在条件测试通过了时执行一个操作，并在没有通过时执行另一个操作
# if conditional_test:
#    do something
# else:
#    do other thing
```

- if-elif-else语句：


```python
# 需要检查的超过两个情形时，python只执行if-elif-else结构中的一个代码块
>>>age = 12
>>>if age < 4:
        price = 0
>>>elif age < 18:
        price = 5
>>>else:
        price = 10
    
>>>print("Your admission cost is $" + str(price) + '.')

Your admission cost is $5.
```
    

- 使用多个elif代码块：


```python
# 可根据需要使用任意数量的if-elif-else代码块，这取决于可能出现的分支情形数量
```

- **省略else代码块**

    Python并不要求if-elif结构后面必须有else代码块，else是一条包罗万象的语句，只要不满足任何if或elif中的条件测试，其中的代码就会执行这可能会引入无效甚至恶意的数据。如果知道最终要测试的条件，应该考虑使用一个elif代码块来代替else代码块，以肯定当且仅当满足相应的条件时，代码才会执行。

- **测试多个条件**

    if-elif-else结构的缺陷在于仅适用于只有一种情形能被继续执行的情况，遇到了通过的测试后python会跳过余下的测试。然而，有时候必须检查所有关心的条件，在这种情况下，应该考虑使用一系列不包含elif和else代码块的简单if语句，即if语句的串联而非并联：


```python
# if conditional_test1:
#    do something
# if conditional_test2:
#    do something
# .....
```
