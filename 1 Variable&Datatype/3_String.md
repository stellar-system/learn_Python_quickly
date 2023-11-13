# String 字符串

--------------

字符串就是一系列字符，在Python中，用引号括起的都是字符串，其中引号可以是单引号，可以是双引号。不同于c，Python 不支持单字符类型，单字符也在Python也是作为一个字符串使用。

字符串常用操作：

1.调整大小写 upper()、lower()、swapcase()、capitalize()、istitle()、isupper()、islower()

2.拼接

3.添加/删除空白 strip()、lstrip()、rstrip()

4.切片、索引

5.替换  s.replace('a', 'b')

6.查找  find()、index()、rfind()、rindex()

7.格式化 

- '%s %s' % ('win', '64')

- '{}, {}'.format(21, 'win') # 推荐使用format格式化字符串

- '{0}, {1}, {0}'.format('Windrivder', 21)

- '{name}: {age}'.format(age=21, name='Windrivder')

8.连接与分隔

## 1.1 调整字符串大小写


```python
# 以首字母大写的方式显示每个单词
name = 'ada lovelace'
print(name.title())

# 所有字母大写
name = name.upper()
print(name)

# 所有字母小写
name = name.lower()
print(name)

Ada Lovelace
ADA LOVELACE
ada lovelace
```


在print语句中，方法title()出现在变量name后面，**方法**是Python可对数据执行的操作。在name.title()中，name后面的句点(.)让Python对变量name执行方法title()指定的操作。每个方法后面都跟着一对括号，这是因为方法通常需要额外的信息来完成其工作，这种信息实在括号内提供的。函数title()不需要额外的信息，因此括号内是空的。

## 1.2 拼接字符串
使用'+'拼接字符串，可以使用拼接来创建消息


```python
>>>first_name = 'ada'
>>>last_name = 'lovelace'
>>>full_name = first_name + ' ' +  last_name
>>>print(full_name.title())

Ada Lovelace
```

    

## 1.3 使用制表符或换行符来添加空白、删除空白

要确保字符串没有空白，可使用方法strip(),**这种删除只是暂时的，并不会改变变量本身存储的字符串**


```python
>>>print('python')
>>>print('\tpython')
>>>print('languages:\npython\nC\njavascript')

python
    python
languages:
python
C
javascript
```
    
```python
>>>favorite_language = ' python '
>>>print(favorite_language)
>>>print(favorite_language.strip())
>>>print(favorite_language.rstrip())
>>>print(favorite_language.lstrip())

 python 
python
 python
python 
```
    

## 1.4 切片、索引


```python
>>>s = 'hello world'
>>>print(s[0])
>>>print(s[::-1])
>>>print(s[3:])

h
dlrow olleh
lo world
```

## 1.5 替换 


```python
>>>s.replace('l', 'PP')

'hePPPPo worPPd'
```

## 1.6 查找


```python
# find(a,b)  a为要查找的字符串，b为从下标b开始寻找，找不到返回-1
>>>print(s.find('l'))  # 返回第一次出现子串的下标
>>>print(s.find('l', 4))  # 设定下标4开始寻找
# rfind(a,b) 从右侧开始寻找，返回最右侧出现的子串的索引（正索引），找不到子串返回-1
>>>print(s.rfind('l')) 

2
9
9
```

```python
>>>print(s.index('l')) # 返回第一次出现的子串的下标，找不到会抛出异常

2
```

## 1.7 格式化


```python
# 以下方法中连接各元素的符号如逗号，冒号分号等都可以随意改动

>>>print('%s %s' % ('win', '64'))

win 64

>>>print('{}, {}'.format(21, 'win')) # 推荐使用format格式化字符串

21, win

>>>print('{0}, {1}, {0}'.format('Windrivder', 21)) # 花括号内的数字是format内的元素的索引

Windrivder, 21, Windrivder

>>>print('{name}: {age}'.format(age=21, name='Windrivder'))

Windrivder: 21
```


## 1.8 连接与分隔


```python
# 使用 + 连接字符串，每次操作会重新计算、开辟、释放内存，效率很低，所以推荐使用join
>>>l = ['2017', '03', '29', '22:00']
>>>string = '-'.join(l)
>>>print(string)

2017-03-29-22:00
```


```python
# 使用split()按元素分隔字符串,分隔后以列表形式返回
>>>print(string.split('-'))

['2017', '03', '29', '22:00']
```

# 字符串编码

------

所有的 Python 字符串都是 Unicode 字符串，当需要将文件保存到外设或进行网络传输时，就要进行编码转换，将字符转换为字节，以提高效率。


```python
# encode 将字符转换为字节
>>>str = '你好世界，hello world!'
>>>print (str.encode())			# 默认编码是 UTF-8  输出：b'\xe5\xad\xa6\xe4\xb9\xa0Python'
>>>print (str.encode('gbk'))      # 输出  b'\xd1\xa7\xcf\xb0Python'
# decode 将字节转换为字符
>>>print (str.encode().decode('utf8'))   # 输出 'hello world'
>>>print (str.encode('gbk').decode('gbk'))             # 输出 'hello world'

b'\xe4\xbd\xa0\xe5\xa5\xbd\xe4\xb8\x96\xe7\x95\x8c\xef\xbc\x8chello world!'
b'\xc4\xe3\xba\xc3\xca\xc0\xbd\xe7\xa3\xachello world!'
你好世界，hello world!
你好世界，hello world!
```

[上一篇(2_Number)](./2_Number.md) \| [下一篇(4_String)](./4_List.md)