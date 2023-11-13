# 生成器(Generator)

------------

```生成器(generator)```是一个用于创建迭代器的简单而强大的工具。他们的写法类似于标准的函数，但是当他们要返回数据时会使用```yield```语句。每次在生成器上调用```next()```时，他会从上次离开的位置恢复执行（即它会记住上次执行语句时的所有数据值）。一个显示如何非常容易地创建生成器的示例如下：


```python
>>>def reverse(data):
        for index in range(len(data)-1,-1,-1):
            yield data[index]

>>>for char in reverse('golf'):
        print(char)


f
l
o
g
```

    

**可以用生成器完成的任何功能都可以用基于类的迭代器来完成**，但生成器的写法更为紧凑，因为它会自动创建```__iter__()```和```__next__()```方法。

另一个关键特性在于```局部变量```和```执行状态```会在每次调用之间自动保存，这使得该函数相比使用```slef.index```和```self.data``` 这种实例变量的方式更易编写且更为清晰。

除了会自动创建方法和保存程序状态，当生成器终结时，他们还会自动引发```StopIteration```，这些特性结合在一起，使得创建迭代器能与编写常规函数一样容易。

**生成器表达式**

某些简单的生成器可以写成简洁的表达式代码，语法类似列表推导式。但外层为圆括号而非方括号。这种表达式被设计用于生成器将立即被外层函数所使用的情况。生成器表达式相比完整的生成器更紧凑但较不灵活，相比等效的列表推导式则更节省内存。


```python
>>>sum(i*i for i in range(10))

285
```


```python
>>>x_vec = [10, 20, 30]
>>>y_vec = [7, 5, 3]
>>>sum(x*y for x,y in zip(x_vec,y_vec))

260
```



```python
# 这段代码使用生成器表达式来创建一个包含唯一单词的集合，它遍历page中的每一行，然后对每一行使用split()方法将其拆分成发单词，并将这些单词添加到生成器中，最后，通过将生成器传递给set()函数，创建一个只包含唯一单词的集合。
unique_words = set(word for line in page for word in line.split())
valedictorian = max((student.gpa, student.name) for student in graduates)
```


```python
>>>data = 'golf'
>>>list(data[i] for i in range(len(data)-1, -1, -1))

['f', 'l', 'o', 'g']
```

[上一篇(3_iteratior)](./3_iterators.md)