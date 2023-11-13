# Output

## 1 print()函数

----------------------------------

print函数用于打印或输出给定参数

print()函数的定义如下：

```python
def print(
    *values: object,
    sep: str | None = " ",
    end: str | None = "\n",
    file: SupportsWrite[str] | None = None,
    flush: Literal[False] = False,
) -> None: ...
```

这是Python built-in函数print的类型解释，它接收以下参数：
- *values: object : 可变数量的参数，表示要打印的值。这意味着，我们在使用print时，不一定只能输出一个变量或字符串。
- sep: str | None = " " : 表示值之间的分隔值，默认为一个空格。
- end: str | None = "\n" : 表示打印结束后要添加的字符，默认为换行符。（因此每次打印结束后，会默认进入下一行）
- file: SupportsWrite[str] | None = None : 表示要将输出写入的文件对象，默认为标准输出sys.stdout。通过将一个文件对象传递给file参数，你可以将print函数的输出写入到指定文件中，而不是默认的标准输出（终端）。
- flush: Literal[False] = False : 表示是否刷新输出缓冲区，默认为False。
- 返回值：函数的返回类型为None，即没有返回值


```python
# 参数1 接收多个传入参数
print('aaa', 'bbb')

aaa bbb
```

```python
# 参数2 修改值之间的分隔值为‘ and ’
print('aaa', 'bbb', sep=' and ')

aaa and bbb
```

```python
# 参数3 修改文件结束字符为' !'
print('aaa', end='!')

aaa!
```

```python
# 参数4 将输出写入到文件
with open('test_print.txt', 'a') as f:
    print('aa', 'bbb', file=f)
```

👆使用这种方法时，需要注意文件的打开方式为附加模式，否则会覆盖原文件


```python
# 参数5 将缓冲区刷新
import time

for i in range(5):
    print(f"Processing step {i+1}...")
    time.sleep(3)
    print("Step completed.", flush=True)

print("Program finished!")

Processing step 1...
Step completed.
Processing step 2...
Step completed.
Processing step 3...
Step completed.
Processing step 4...
Step completed.
Processing step 5...
Step completed.
Program finished!
```

    

🛎️刷新缓冲区是指将缓冲区中的数据立即写入到输出设备（终端或文件）中，在Python中，print函数默认情况下不会立即将输出写入到终端，而是先将输出存储在缓冲区中，然后在适当的时机将缓冲区的内容写入到终端。

当flush的参数设置为True时，表示要立即刷新缓冲区，即将缓冲区中的内容立即写入到输出设备中，这在某些情况下很有用。例如当你希望立即将输出显示在终端上，而不是等到缓冲区满或程序结束时才显示。

以下是一些可能需要使用flush=True的情况：

1. 实时日志记录：如果你正在编写一个需要实时记录日志的应用程序，你可能希望将日志消息立即显示在终端或日志文件中。

2. 长时间运行的程序：当你有一个长时间运行的程序，需要逐步输出一些信息时。

3. 调试和排除故障：在调试和故障排除过程中，你可能希望立即将某些信息显示在终端上，以便更好地理解程序的执行流程和状态。

❗使用flush=True会频繁地将输出写入到输出设备，可能会对程序的性能产生影响。因此只在必要时使用，以避免不必要的性能开销。

## 2 更复杂的输出格式

-------------------------------

对输出格式的控制不只是打印空格分隔的值，还需要更多方式：

### 2.1 使用```格式化字符串字面值```

- 要在字符串开头的引号/三引号前添加```f```或```F```（简称f-字符串）。在这种字符串中，可以在```{```和```}``字符之间```（```{expressions}```）输入引用的变量，或字面值的Python表达式。

```python
>>> year = 2016
>>> event = 'Referendum'
>>> f'Results of the {year} {event}'

'Results of the 2016 Referendum'
```

- 格式说明符是可选的，写在表达式后面，可以更好地控制格式化值的方式：
```python
>>>import math
>>>print(f'The value of pi is approximately {math.pi:.3f}')
                                               ↑       ↑
                                               |       |-格式说明符
                                               |-表达式
The value of pi is approximately 3.142
```

- 在```':'```后传递整数，为该字段设置最小字符宽度，常用于列对齐：
```python
>>>table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 7678}
>>>for name, phone in table.items():
       print(f'{name:10} ==> {phone:10d}')

Sjoerd     ==>       4127
Jack       ==>       4098
Dcab       ==>       7678
```

- 还有一些修饰符可以在格式化前转换值。`'!a'`应用`ascii()`,`'!s'`应用`str()`,`'!r'`应用`repr()`:

```python
>>>animals = 'eels'
>>>print(f'My hovercraft is full of {animals}.')

My hovercraft is full of eels.
>>>print(f'My hovercraft is full of {animals!r}.')

My hovercraft is full of 'eels'.
```

- `=`说明符可被用于将一个表达式拓展为表达式文本、等号再加表达式求值结果的形式
```python
>>>bugs = 'roaches'
>>>count = 13
>>>area = 'living room'
>>>print(f'Debugging {bugs=} {count=} {area=}')

Debugging bugs='roaches' count=13 area='living room'
```

### 2.2 字符串format()方法

- 字符串的```str.format()```方法需要更多手动操作。该方法也用```{```和```}``标记替换变量的位置，虽然这种方法支持详细的格式化指令，但需要提供格式化信息。

```python
>>> year = 42_512_654
>>> no_votes = 43_132_495
>>> percentage = yes_votes / (yes_votes + no_votes)
>>> '{:-9} YES votes {:2.2%}'.format(yes_votes, percentage)

' 42572654 YES votes  49.67%'
```

- 花括号及之内的字符（称为格式字段）被替换为传递给`str.formta()`方法的对象，花括号中的数字表示传递给`str.format()`方法的对象所在的位置：

```python
>>>print('{0} and {1}'.format('spam', 'eggs'))
spam and eggs
>>>print('{1} and {0}'.format('spam', 'eggs'))
eggs and spam
```

- `str.format()`方法中使用关键字参数名引用值。

```python
>>>print('The story of {0}, {1}, and {other}'.format('Bill', 'Manfred', other='Georg'))

The story of Bill, Manfred, and Georg.
```

- 如果不想分拆较长的格式字符串，最好按名称引用变量进行格式化，不要按位置。这项操作可以通过传递字典，并用方括号`'[]'`访问键来完成。

```python
>>>table = {'Sjoerd':4127, 'Jack':4098, 'Dcab':8637678}
>>>print('Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; Dcab: {0[Dcab]:d}'.format(table))

Jack: 4098; Sjoerd: 4127; Dcab: 8637678
```

- 也可以通过将`table`字典作为采用`**`标记的关键字参数传入来实现。

```python
>>>table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
>>>print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(**table))

Jack: 4098; Sjoerd: 4127; Dcab: 8637678
```

### 2.3 手动格式化字符串
  
最后，还可以用字符串切片和合并操作完成字符串处理操作，创建任何排版布局。字符串类型还支持将字符串按给定列宽进行补充。

字符串对象的`str.rjust()`方法通过在左侧填充空格，对给定宽度字段中的字符串进行右对齐。同类方法还有`str.ljust()`和`str.center()`。这些方法不写入任何内容，只返回一个新字符串，如果输入的字符串太长，它们不会截断字符串，而是原样返回；虽然这种方式会弄乱列布局，但也比另一种方法好，后者在显示值时可能不准确（如果真的想截断字符串，可以使用`x.ljust(n)[:n]`这样的切片操作。）

另一种方法是`str.zfill()`，该方法在数字字符串左边填充零，且能识别正负号。

`%`运算符（求余符）也可用于字符串格式化。给定`'string' % values`，则`string`中的`%`实例会以零个或多个`values`元素替换。此操作被称为字符串插值。
