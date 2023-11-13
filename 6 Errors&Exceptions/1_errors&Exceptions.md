# 1 语法错误(Invalid syntax)

----------------------

```语法错误```又称```解析错误```，是Python中最常见的错误：


```python
>>>while True print('Hello World!')

Cell In[1], line 1
while True print('Hello World!')
            ^
SyntaxError: invalid syntax
```

解释器会复现出现语法错误的代码行，并用小箭头指向行里检测到的第一个错误，错误是由箭头上方的token触发的（或是在这里检测出的），本例中，在print()函数中检测到错误，因为在其前面缺少冒号```':'```。错误信息还输出文件名和行号，这样就可以精准定位错误。

# 2 异常(Exceptions)

--------------------------

即使语句或表达式采用了正确的语法，执行时仍然有可能出发错误。执行时检测到的错误被称为```异常```，异常不一定导致严重的错误，接下来我们将学习如何处理异常：

```python
# 一些异常信息
10 * (1/0)

---------------------------------------------------------------------------

ZeroDivisionError                         Traceback (most recent call last)

d:\Studying\python-learning\learn_Python_quickly\6 Errors&Exceptions\JupyterNotebook\1_errors&Exceptions.ipynb Cell 5 line 2
        <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/6%20Errors%26Exceptions/JupyterNotebook/1_errors%26Exceptions.ipynb#W6sZmlsZQ%3D%3D?line=0'>1</a> # 一些异常信息
----> <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/6%20Errors%26Exceptions/JupyterNotebook/1_errors%26Exceptions.ipynb#W6sZmlsZQ%3D%3D?line=1'>2</a> 10 * (1/0)


ZeroDivisionError: division by zero
```


```python
4 + (spam * 3)

---------------------------------------------------------------------------

NameError                                 Traceback (most recent call last)

d:\Studying\python-learning\learn_Python_quickly\6 Errors&Exceptions\JupyterNotebook\1_errors&Exceptions.ipynb Cell 6 line 1
----> <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/6%20Errors%26Exceptions/JupyterNotebook/1_errors%26Exceptions.ipynb#X10sZmlsZQ%3D%3D?line=0'>1</a> 4 + (spam * 3)


NameError: name 'spam' is not defined
```

```python
'2' + 2


---------------------------------------------------------------------------

TypeError                                 Traceback (most recent call last)

d:\Studying\python-learning\learn_Python_quickly\6 Errors&Exceptions\JupyterNotebook\1_errors&Exceptions.ipynb Cell 7 line 1
----> <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/6%20Errors%26Exceptions/JupyterNotebook/1_errors%26Exceptions.ipynb#X11sZmlsZQ%3D%3D?line=0'>1</a> '2' + 2


TypeError: can only concatenate str (not "int") to str
```



错误信息的左后一行说明程序遇到了什么类型的错误，异常有不同的类型，而类型名称会作为错误信息的一部分中打印出来。作为异常类型被打印出的字符串是发生的```内置异常```的名称。对于所有的内置异常都是如此，但对于用户定义的异常则不一定如此，标准的异常类型是内置的标识符（不是保留关键字）。

python使用被称为**异常**的特殊对象来管理程序执行期间发生的错误。每当发生让python不知所措的错误时，它都会创建一个**异常对象**，如果你编写了处理该异常的相关代码，程序将继续运行；否则程序将停止，并显示一个**traceback**，其中包含有关异常的报告。

## 2.1 异常的处理

异常是使用**try-except**代码块处理的，try-except代码块让python执行指定的操作，同时告诉python发生异常时该怎么办，使用该代码块时，即便出现异常，程序也将继续运行，显示你编写的友好的错误信息。

可以编写程序处理选定的异常。下例会要求用户一直输入内容，直到输入有效的整数，但允许用户中断程序（即通过Ctrl-c或其他系统支持的操作触发```KeyboardInterupt```异常。


```python
while True:
    try:
        x = int(input("Please enter a number:"))
        break
    except ValueError:
        print("Oops! That was no valid number.Try again...")



---------------------------------------------------------------------------

ValueError                                Traceback (most recent call last)

d:\Studying\python-learning\learn_Python_quickly\6 Errors&Exceptions\JupyterNotebook\1_errors&Exceptions.ipynb Cell 10 line 3
        <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/6%20Errors%26Exceptions/JupyterNotebook/1_errors%26Exceptions.ipynb#X15sZmlsZQ%3D%3D?line=1'>2</a> try:
----> <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/6%20Errors%26Exceptions/JupyterNotebook/1_errors%26Exceptions.ipynb#X15sZmlsZQ%3D%3D?line=2'>3</a>     x = int(input("Please enter a number:"))
        <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/6%20Errors%26Exceptions/JupyterNotebook/1_errors%26Exceptions.ipynb#X15sZmlsZQ%3D%3D?line=3'>4</a>     break


ValueError: invalid literal for int() with base 10: 'q'


During handling of the above exception, another exception occurred:


TypeError                                 Traceback (most recent call last)

d:\Studying\python-learning\learn_Python_quickly\6 Errors&Exceptions\JupyterNotebook\1_errors&Exceptions.ipynb Cell 10 line 5
        <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/6%20Errors%26Exceptions/JupyterNotebook/1_errors%26Exceptions.ipynb#X15sZmlsZQ%3D%3D?line=2'>3</a>     x = int(input("Please enter a number:"))
        <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/6%20Errors%26Exceptions/JupyterNotebook/1_errors%26Exceptions.ipynb#X15sZmlsZQ%3D%3D?line=3'>4</a>     break
----> <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/6%20Errors%26Exceptions/JupyterNotebook/1_errors%26Exceptions.ipynb#X15sZmlsZQ%3D%3D?line=4'>5</a> except not RuntimeError:
        <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/6%20Errors%26Exceptions/JupyterNotebook/1_errors%26Exceptions.ipynb#X15sZmlsZQ%3D%3D?line=5'>6</a>     print("Oops! That was no valid number.Try again...")


TypeError: catching classes that do not inherit from BaseException is not allowed
```

### 2.1.1 try语句工作原理

```try```语句的工作原理如下：

- 首先，执行```try子句```，即try和except关键字之间的多行语句。
- 如果```try子句```没有触发异常，则跳过except子句，try语句执行完毕
- 如果在执行```try子句```时发生了异常，则跳过该子句中剩下的部分。如果异常的类型与```except```关键字后指定的异常相匹配，则会执行```except子句```，然后跳到**try-except**代码块之后运行。
- 如果发生的异常与```except子句```中指定的异常不匹配，则它会被传递到外部的```try语句```中；如果没有找到处理程序，则他是一个**未处理异常**且执行将终止并输出错误信息。

### 2.1.2 处理多个异常

try语句可以有多个except子句来为不同的异常指定处理程序，但最多只有一个处理程序会被执行。处理程序只处理对应的try子句中发生的异常，而不处理同一try语句中其他处理程序中的异常。**except子句**可以用带圆括号的元组来指定多个异常如：

```python
except (RuntimeError, TypeError, NameError):
    pass
```

❗如果发生的异常与except子句中的类是同一个类或是其派生类时，则该类与该异常相兼容（反之则不成立），即发生的异常类必须是except子句中的类或其派生类（子类）。

```python
# 交换以下代码中except语句顺序试试
class B(Exception):
    pass

class C(B):
    pass

class D(C):
    pass

for cls in [B, C, D]:
    try:
        raise cls
    except D:
        print("D")
    except C:
        print("C")
    except B:
        print("B")
```

### 2.1.3 异常的参数

发生异常时，它可能具有关联值，即```异常参数```，是否需要参数，以及参数的类型取决于异常的类型。```except子句```可能会在异常名称后面指定一个变量。这个变量将被绑定到异常实例，该实例通常会有一个存储参数的```args```属性，为了方便，内置异常类型定义了```__str__()```来打印所有的参数而不是显式地访问```.args```:


```python
try:
    raise Exception('spam', 'eggs') 
except Exception as inst:  # 有趣的用法
    print(type(inst))      # 异常类型
    print(inst.args)       # 存放在 .args 属性中的参数
    print(inst)            # __str__() 允许参数被直接打印出来，但可能在异常的子类被覆盖
    x, y = inst.args
    print('x = ',x)
    print('y = ',y)
    print(inst.__str__())


<class 'Exception'>
('spam', 'eggs')
('spam', 'eggs')
x =  spam
y =  eggs
('spam', 'eggs')
```


### 2.1.4 异常类

```BaseException```是所有异常的**共同基类**。它的一个子类，```Exception```，是所有非致命异常的基类。不是```Exception```的子类的异常通常不被处理，因为他们被用来指示程序应该终止，它们包括由```sys.exit()```引发的```SystemExit```，以及当用户希望中断程序时引发的```KeyboradInterrupt```。

```Exception```可以被用作通配符，捕获几乎一切异常，然而在实际编程中我们应该尽可能具体的说明我们打算处理的异常类型，并允许任何以外的异常传播下去。

处理```Exception```最常见的模式是打印或记录异常，然后重新提出（允许调用者也处理异常）：

```python
import sys

try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
except OSError as err:
    print("OS error:", err)
except ValueError:
    print("Could not convert data to an integer")
except Exception as err:
    print(f"Unexpected {err=}, {type(err)=}")
    raise    # 默认抛出当前异常
```

```try-except```语句具有可选的```else子句```，该子句如果存在，它必须放在所有except子句之后，它适用于try子句没有引发异常但又必须要执行的代码。使用else子句比向try子句添加额外的代码要好，可以避免意外捕获非try-except语句保护的代码出发的异常。代码逻辑为：

```python
# 原代码逻辑，如果要用try-except语句检测statement-a是否抛出异常
statement-a
...
statement-n

# 修改后的代码
try:
    statement-a
except ErrorName:
    pass
else:
    statement-b
    ...
    statement-n
```

异常处理程序不仅会处理在try子句中立刻发生的异常，还会处理在try子句中调用（包括简洁调用）的函数：

```python
def this_fails():
    x = 1 / 0
    
try:
    this_fails()
except ZeroDivisionError as err:
    print('handling run-time error:', err)
```

## 2.3 触发异常

```raise```语句支持强制出发指定的异常，如：

```python
raise NameError('HiThere')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: HiThere
```

```raise```唯一的参数就是要触发的异常，这个参数必须是异常实例或异常类（派生自```BaseException```类，例如```Exception```及其子类。如果传递的是异常类，则通过调用没有参数的构造函数来隐式实例化：
```python
raise ValueError  # raise ValueError()
```

如果只想判断是否触发了异常，但并不打算处理该异常，则可以使用更简单的raise语句重新触发异常：
```python
try:
  raise NameError()
except NameError:
  print('An exception flew by!')
  raise
```

## 2.4 异常链

如果一个未处理的异常发生在```except```部分内，它将会有被处理的异常附加到它上面，并包含在错误信息中。

为了表明一个异常是另一个异常的直接后果，```raise```语句允许一个可选的```from```子句：
```python
raise RuntimeError from exc # exc 必须是一个异常实例或None
```

它还允许使用```from None```表达禁用自动异常链

## 2.5 用户自定义异常

程序可以通过创建新的异常类命名自己的异常，**不论是以直接或间接的方式，异常都应从```Exception```类派生。**

异常类可以被定义成能做其他类所能做的任何事，但通常应该当保持简单，它往往只提供一些属性，允许相应的异常处理程序提取有关错误的信息。

且大多数异常的命名都以'Error'结尾，类似标准内置异常的命名。

## 2.6 定义清理操作

```try语句```还有一个可选子句，用于定义在所有情况下都必须要执行的清理操作。例如：

```python
try:
    raise KeyboardInterrput
finally:
    print('Goodbye, world!')
```

如果存在```finally子句```，则finally子句是try语句结束前执行的最后一项任务，**无论try语句是否触发异常，都会执行finally子句。以下内容介绍了几种比较复杂的触发异常情景：

- 如果执行try子句期间触发了某个异常，则某个except子句应处理该异常。如果该异常没有except子句处理，在finally子句执行后会被重新触发。
- except或else子句执行期间也会触发异常。 同样，该异常会在finally子句执行之后被重新触发。如果finally子句中包含break、continue或return等语句，异常将不会被重新引发。
- 如果执行try语句时遇到break,、continue或return语句，则finally子句在执行break、continue或return语句之前执行。
- 如果finally子句中包含return语句，则返回值来自finally子句的某个return语句的返回值，而不是来自try子句的return语句的返回值。

## 2.7 预定义的清理操作

某些对象定义了不需要该对象时要执行的标准清理操作。无论使用该对象的操作是否成功，都会执行清理操作。例如```with语句```：
```python 
with open('mydile.txt') as f:
    for line in f:
        print(line, end='')
```
语句执行完毕后，即使在处理行时遇到问题，都会关闭文件f。和文件一样，支持预定义清理操作的对象会在文档中指出这一点。

## 2.8 引发和处理多个不相关的异常

在有些情况下，有必要报告几个已经发生的异常。这通常是在并发框架中当几个任务并行失败时的情况，但也有其他的用例，有时需要是继续执行并收集多个错误而不是引发第一个异常。

内置的```ExceptionGroup```打包了一个异常实例的列表，这样它们就可以一起被引发。它本身就是一个异常，所以它可以像其他异常一样被捕获。

```python
>>>def f():
        excs = [OSError('error 1'), SystemError('error 2')]
        raise ExceptionGroup('there were problems', excs)

>>>f()

  + Exception Group Traceback (most recent call last):
  |   File "<stdin>", line 1, in <module>
  |   File "<stdin>", line 3, in f
  | ExceptionGroup: there were problems
  +-+---------------- 1 ----------------
    | OSError: error 1
    +---------------- 2 ----------------
    | SystemError: error 2
    +------------------------------------

>>>try:
        f()
    except Exception as e:
        print(f'caught {type(e)}: e')

caught <class 'ExceptionGroup'>: e
```

通过使用```except*```代替```except```，我们可以有选择地只处理组中符合某种类型的异常。在下面的例子中，显示了一个嵌套的异常组，每个```except*子句```都从组中提取了某种类型的异常，而让所有其他的异常传播到其他子句，并最终被重新引发。

```python
>>>def f():
       raise ExceptionGroup(
                "group1",[OSError(1),SystemError(2),
                ExceptionGroup("group2",[OSError(3),RecursionError(4)])])

>>>try:
       f()
   except* OSError as e:
       print("There were OSErrors")
   except* SystemError as e:
       print("There were SystemErrors")

There were OSErrors
There were SystemErrors
  + Exception Group Traceback (most recent call last):
  |   File "<stdin>", line 2, in <module>
  |   File "<stdin>", line 2, in f
  | ExceptionGroup: group1
  +-+---------------- 1 ----------------
    | ExceptionGroup: group2
    +-+---------------- 1 ----------------
      | RecursionError: 4
      +------------------------------------
```

❗注意，嵌套在一个异常组中的异常必须是实例，而不是类型。这是因为在实践中，这些异常通常是那些已经被程序提出并捕获的异常，其模式如下:

```python
>>>excs = []
>>>for test in tests:
        try:
                test.run()
        except Exception as e:
                excs.append(e)

>>>if excs:
        raise ExceptionGroup("Test Failures", excs)
```

## 2.8 用注释细化异常情况

当一个异常被创建以引发时，它通常被初始化为描述所发生错误的信息。在有些情况下，在异常被捕获后添加信息是很有用的。为了这个目的，异常有一个```add_note(note)```方法接受一个字符串，并将其添加到异常的注释列表。标准的回溯在异常之后按照它们被添加的顺序呈现包括所有的注释。

```python
>>>try:
        raise TypeError('bad type')
    except Exception as e:
        e.add_note('Add some information')
        e.add_note('Add some more information')
        raise

Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
TypeError: bad type
Add some information
Add some more information
```
