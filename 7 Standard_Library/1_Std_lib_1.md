# 标准库简介1

---------------------------


## 1 操作系统接口

- **OS 模块** （Operation System）

os模块提供了许多```与操作系统交互的函数```

```python
os.getcwd()  get current working directory 获取当前工作路径
os.chdir('path') change current working directory 更改当前工作路径
os.system('command') run the commmand in the system shell 在系统的shell中运行指令（从参数获得）
```

❗一定要用`import os`而不是`from os import *`，这将避免内建的`os.open()`函数被`os.open()`隐式替换掉。

内置的`dir()`和`help()`函数可用作交互式辅助工具，用于处理大型模块，如os。

```python
dir(os)  returns a list of all module function 返回一个包含所有模块函数的列表
help(os)  returns a extensive manual page created from the module's docstrings 返回模块的文本字符串
```

- **shutil 模块**

对于日常文件和目录管理任务，`shutil`模块提供了更易于使用的更高级别的接口，`shutil`是python标准库中的一个模块，它提供了一些同于文件和目录操作的高级别接口。shutil模块的目标是提供一种更简单、更易于使用的方式来执行常见的文件和目录的管理任务。shutil模块包含了一些常用的个函数，例如复制文件、移动文件、删除文件、创建目录等。

```python
shutil.copyfile(file_a, file_b) 将文件从file_a复制到文件file_b
shutil.move(a, b) 将文件或目录从a移动到b
```

## 2 文件通配符

`glob`模块提供了一个在目录中使用通配符搜索创建文件列表的函数：
```python
import glob
glob.glob('*.py')  # 搜索所有的py文件
```

## 3 命令行参数

- **sys模块**
  
一般的工具脚本常常需要处理命令行参数，这些参数以`列表`形式存储在`sys`模块的argv属性中：

```python
demo.py
import sys
print(sys.argv)

command line:
python demo.py one two three

output:
['demo.py', 'one', 'two', 'three']
```

sys模块的一些其他常用功能：
```python
sys.path 一个包含模块搜索路径的列表，用于添加或删除模块搜索路径
sys.modules 一个包含已导入模块的字典
sys.stdout 和 sys.stderr 标准输出和标准错误输出流，可以通过重定向这些流来改变输出的目的地
sys.exit() 用于退出程序的函数，用于终止程序的执行
```

- **argparse模块**

argparse模块提供了一种更复杂的机制来处理命令行参数：

argparse模块的常用方法：
```python
1.首先导入argparse模块：import argparse
2.创建ArgumentParser对象：使用 argparse.ArgumentPaeser() 创建一个ArgumentParser对象，用于定义命令行参数的解析规则，通常将该对象命名为 parser，且在定义时会对参数进行初始定义
3.添加命令行参数：使用 add_argument() 方法向parser添加命令行参数，可以指定参数的名称、类型、默认值、帮助信息等。
4.解析命令行参数：使用 parse_args() 方法解析命令行参数。该方法会解析命令行参数并返回一个包含解析结果的命名空间对象
5.使用解析结果：可以通过访问命名空间对象的属性来获取解析结果，然后根据需要进行相应的处理
```

```python 
import argparse   # step 1

parser = argparse.ArgumentParser(
    prog = 'top',
    descripyion = 'Show top lines from each file',)  # step 2
    
parser.add_argument('filenames', nargs='+')
parser.add_argument('-l', '--lines', type=int, default=10) # step 3

args = parser.parse_args() # step 4

print(args.filenames)
print(args.lines)  # step 5
```

当通过`python top.py --lines=5 alpha.txt beta.txt`在命令行运行时，该脚本会将`args.lines`设为5，并将`args.filenames`设为`['alpha.txt', 'beta.txt']`。


## 4 错误输出重定向

错误输出重定向是指将程序的错误信息（通常是通过标准错误流stderr输出的消息）重定向到其他位置或设备，而不是默认的输出位置，在python中，可以使用`sys.stderr`来访问标准错误流，通常情况下，错误消息会直接打印到控制台或终端上，但是，通过重定向标准错误流，我们可以将错误消息输出到其他地方，如日志文件或其他设备。

错误输出重定向可以通过以下方式实现：

1.**重定向到文件**：可以将错误消息重定向到一个文件中，以便后续查看和分析，可以使用文件操作相关的函数（如open()和write()）将错误消息写入文件。sys模块具有`stdin`, `stdout`, `stderr`的属性，后者对于发出警告和错误消息非常有用，即使在stdout被重定向后也可以看到他们。
```python
import sys

with open('error.log', 'w') as f:
    try:
        1/0
    except ZeroDivisionError as e:
        sys.stderr = f
        sys.stderr.write(f'错误消息：{e}')
        sys.stderr = sys.__stderr__
```

2.**重定向到日志**：可以将错误消息重定向到一个日志系统中，以便进行更好的错误管理和记录。可以使用Python的日志模块（如logging）来实现日志记录和管理。
```python
import logging

logging.basicConfig(filename='error_log.log', level=logging.ERROR)

try:
    1/0
except ZeroDivisionError as e:
    logging.error(f'错误信息:{e}')
```

3.**重定向到其他设备**：除了文件和日志系统，还可以将错误消息重定向到其他设备，如网络套接字、串口等。这需要根据具体的需求和设备进行相应的配置和操作。
```python
import sys
import socket

# 配置网络套接字
host = 'localhost'
port = 12345
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.connect((host, port))

try:
    1/0
except ZeroDivisionError as e:
    error_message = f'错误消息：{e}'
    sock.sendall(error_message.encode())
    sock.close()
```

## 字符串模式匹配

`re模块`为高级字符串处理提供`正则表达式`工具。对于复杂的匹配和操作，正则表达式提供简洁，优化的解决方案。

`正则表达式`是一种用于匹配和操作字符串的强大工具，它是一种由字符和特殊字符组成的模式，用于描述字符串的特定模式。正则表达式可以用于搜索、替换、验证和提取字符串中的特定内容。

正则表达式的模式由普通字符（例如字母、数字和标点符号）和特殊字符（元字符）组成。这些特殊字符具有特殊的含义，用于表示匹配规则和模式。

一些常用的正则表达式元字符：

- `.`:匹配任意单个字符，除了换行符
- `*`:匹配前面的字符零次或多次
- `+`:匹配前面的字符一次或多次
- `?`:匹配前面的字符零次或一次
- `[]`:定义字符集，匹配其中的任意一个字符
- `()`:定义捕获组，用于提取匹配的内容
- `\`:转义字符，用于匹配特殊字符本身

正则表达式还支持一些特殊的字符类别，如`\d`表示匹配任意数字字符，`\w`表示匹配任意字母、数字或下划线字符，`\s`表示匹配任意空白字符，`\b`用以表示单词边界等。

```python
import re

re.findall(r'\bf[a-z]*','which foot or hand fell fastest')
```

re模块的一些常用方法：

```
re.match(pattern, string, flags=0) 从字符串的开头开始尝试匹配正则表达式的模式，如果匹配成功，则返回一个匹配对象，否则返回None

re.search(pattern, string, flags=0) 在字符串中搜索匹配正则表达式的模式。如果匹配成功，则返回一个匹配对象，否则返回None

re.findall(pattern, string, flags=0) 在字符串中查找所有匹配正则表达式的模式，并以列表的实行返回所有匹配结果

re.sub(pattern, repl, string, count=0, flags=0) 将字符串中匹配正则表达式的模式替换为指定的字符串

re.split(pattern, string, maxsplit=0, flags=0) 根据正则表达式的模式将字符串分割为列表
```

## 6 数学

- `math模块`提供对浮点数学的底层C库函数的访问：

```python
>>>import math

>>>math.cos(math.pi / 4)
0.7071067811865476
>>>math.log(1024, 2)
10.0
```

- `random模块`提供了进行随机选择的工具：
```python
>>>import random

>>>random.choice(['apple', 'pear', 'banana'])  
'apple'
>>>random.sample(range(100), 10)  # sampling without replacement
[13, 10, 9, 93, 97, 4, 36, 0, 94, 84]
>>>andom.random()  # random float 随机浮点数
0.5988550194540547
>>>random.randrange(6) # random integer chosen from range(6)
1
```

- `statistics模块`计算数值数据的基本统计属性（均值、中位数、方差等）：
```python
>>>import statistics

>>>data = [2.75, 1.75, 1.25, 0.25, 0.5, 1.25, 3.5]
>>>statistics.mean(data)
1.6071428571428572
>>>statistics.median(data)
1.25
>>>statistics.variance(data)
1.3720238095238095
```

## 7 互联网访问

有许多模块可用于访问互联网和处理互联网协议。其中两个最简单的`urllib.request`用于从URL检索数据，以及`smtplib`用于发送邮件：

```python
>>>from urllib.request import urlopen
>>>with urlopen('https://worldtimeapi.org/api/timezone/etc/UTC.txt') as response:
       for line in response:
           line = line.decode()            # convert bytes to str
           if line.startswith('datetime'):
               print(line.rstrip())        # remove trailing newline

datetime: 2023-11-12T06:16:55.235641+00:00
```

```python
>>>import smtplib

>>>server = smtplib.SMTP('localhost')
>>>server.sendmail('soothsayer@example.org', 'jcaesar@example.org',
"""To: jcaesar@example.org
From: soothsayer@example.org

Beware the Ides of March.
""")
>>>server.quit()
```

## 8 日期和时间

`datetime模块`提供了以简单和复杂的方式操作日期和时间的类，虽然支持日期和时间算法，但实现的重点是有效的成员提取以进行输出格式化和操作。该模块还支持可感知时区的对象。

```python
>>># datasets are easily constructed and formatted
>>>from datetime import date
>>>now = date.today()
>>>now
datetime.date(2023, 11, 12)
>>>now.strftime("%m-%d-%y. %d %b %Y is a %A on the %d day of %B")
'11-12-23. 12 Nov 2023 is a Sunday on the 12 day of November'

>>># dates support calendar arithmetic
>>>birthday = date(1964, 7, 31)
>>>age = now - birthday
>>>age.days
21653
```

## 9 数据压缩

常见的数据存档和压缩格式由模块直接支持，包括`zlib`,`gzip`,`bz2`,`lzma`,`zipfile`和`tarfile`:

```python
>>>import zlib
>>>s = b'witch which has which witchses wrist watch'
>>>len(s)
41
>>>t = zlib.compress(s)
>>>len(t)
37
>>>zlib.decompress(t)
b'witch which has which witches wrist watch'
>>>zlib.crc32(s)
226805979
```

## 10 性能测量

一些python用户对了解同一问题的不同方法的相对性能产生了浓厚的兴趣，python提供了可以立即回答这些问题的测量工具。

例如，元组封包和拆包功能相比传统的交换参数可能更具吸引力。`timeit`模块可以快速演示在运行效率方面一定的优势。

```python
>>>from timeit import Timer

>>>Timer('t=a; a=b; b=t','a=1; b=2').timeit()
0.018534100032411516
>>>Timer('a,b = b,a', 'a=1; b=2').timeit()
0.01644139998825267
```

与`timeit`的精细粒度级别相反，`profile`和`pstats`模块提供了用于在较大的代码块中识别时间关键部分的工具。

## 11 质量控制

开发高质量软件的一种方法是在开发过程中为每个函数编写测试，并在开发过程中经常运行这些测试。

- `doctest`模块:
  
  该模块提供了一个工具，用于扫描模块并验证程序文档字符串中嵌入的测试。测试构造就像将典型调用及其结果剪切并粘贴到文档字符串一样简单。这通过向用户提供示例来改进文档，并且它允许doctest模块确保代码保持对文档的真实。

```python
def average(values):
  """Computes the arithmetic mean of a list of numbers.

  >>> print(average([20, 30, 70]))
  40.0
  """
  return sum(values) / len(values)  

import doctest
doctest.testmod()  # automatically validate the embedded tests
```

- `unittest`模块：
  
  不像`doctest`那样易于使用，但它允许在一个单独的文件中维护更全面的测试集：

```python
import unittest

class TestStatiticalFunctions(unitest.TestCase):
  
  def test_average(self):
    self.assertEqual(average([20, 30, 70]). 40.0)
    self.assertEqual(round(average([1, 5, 7]), 1), 4.3)
    with self.assertRaise(ZeroDivisionError):
      average([])
    with self.assertRaises(TypeError):
      average(20, 30, 70)

unittest.main() # Calling from the command line invokes all tests      
```

## 12 自带电池

Python有```自带电池```的理念。通过其包的复杂程度和强大的功能可以最好地看到这一点：

- `xmlrpc.client`和`xmlrpc.server`模块使得实现远程过程调用变成了小菜一碟，尽管存在于模块名称中，单用户不需要直接了解或处理XML。
- `email`包是一个用于管理电子邮件的库，包括MIME和其他符合`RFC 2822`规范的邮件文档。与`smtplib`和`poplib`不同（他们实际上做的是发送和接收消息），电子邮件包提供完整的工具集，用于构建和解码复杂的消息结构（包括附件）以及是西安互联网编码和标头协议。
- `json`包为解析这种流行的数据交换格式提供了强大的支持。`csv`模块支持以逗号分隔值格式直接读取和写入文件，这种格式通常为数据库和电子表格所支持。XML处理由`xml.etree.ElementTree`,`xml.dom`和`xml.sax`包支持。这些模块和软件包共同大大简化了Python应用程序和其他工具之间的数据交换。
- `sqlite3`模块是SQLite数据库的包装器，提供了一个可以使用稍微非标准的SQL语法更新和访问的持久数据库。
- 国际化由许多模块支持，包括`gettext`，`locale`，以及`codecs`包。
