# 1 for循环

------------

for循环可以遍历任何序列的项目，如列表或字符串（字符串可以看作字符列表，同样可以进行索引、切片等操作）

## 1.1 for循环语法：
```
for 变量名 in 序列：
    函数（变量名） # 后续操作
```
for循环每次从序列中取一个值放入变量中，变量名是自定义的，常常取用i或其他方便理解代码的名称，变量通常会直接在循环体内进行调用


# 2 while循环

--------------

for循环用于针对集合中的每个元素的一个代码块，而while循环不断地运行，直到指定的条件不满足为止

## 2.1 while循环语法：
```
while 条件判断：
    循环体
```


```python
current_number = 1
while current_number <= 5:
    print(current_number)
    current_number += 1

1
2
3
4
5
```


    


```python
# 让用户选择何时推出循环体
prompt = "tell me something, and I will repeat it back to you； "
prompt += "\nEnter 'quit' to end the program"
message = ''
while message != 'quit':
    message = input(prompt)
    print(message)


quit
```

    

## 2.3 使用while循环处理列表和字典

- 1 在列表之间移动元素


```python
# 首先创建一个待验证用户列表
# 和 一个用于储存已验证用户的列表
unconfirmed_users = ['alice', 'brian', 'candace']
confirmed_users = []

# 验证每个用户，知道没有未验证的用户为止
# 将每个经过验证的用户都移到已验证的用户列表中
while unconfirmed_users:
    current_user = unconfirmed_users.pop()
    print("Verifying user: " + current_user.title())
    confirmed_users.append(current_user)
    
# 显示所有已验证的用户
print('\nThe following users have been confirmed:')
for confirmed_user in confirmed_users:
    print(confirmed_user.title())

Verifying user: Candace
Verifying user: Brian
Verifying user: Alice

The following users have been confirmed:
Candace
Brian
Alice
```


    

- 2 删除包含特定值的所有列表元素


```python
# remove()方法只能删除列表中出现的第一个目标元素
pets = ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
print(pets)

while 'cat' in pets:
    pets.remove('cat')
    
print(pets)

['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
['dog', 'dog', 'goldfish', 'rabbit']
```


    

- 3 使用用户输入来填充字典


```python
# 可使用while循环提示用户输入任意熟练的信息
responses = {}

# 设置一个标志，指出调查是否继续
polling_active = True

while polling_active:
    # 提示输入被调查者的名字和回答
    name = input('\nWhat is your name? ')
    response = input('Which moutain would you like to climb someday? ')
    
    # 将答案存储在字典中
    responses[name] = response
    
    # 看看是否还有人要参与调查
    repeat = input('Would you like to let another person respond?(yes/no) ')
    if repeat == 'no':
        polling_active = False
        
# 调查结束，显示结果
print('\n---polling results---')
for name,response in responses.items():
    print(name + " would like to climb " + response + '.')

---polling results---
    would like to climb .
lh would like to climb abc.
```

    

# 3 循环体中的几个重要概念和保留字：

------------------------------

###  3.1 **标志**：
    在要求很多条件都要满足才继续运行的程序中，可定义一个变量，用于判断整个程序是否处于活动状态，这个变量被称为标志，标志很有用，在其中的任何一个事件导致活动的标志位变成False时，主游戏循环将推出，此时可显示一条游戏结束消息，并让用户选择是否要重新玩。


```python
active = True
while active:
    message = input('what: ')
    
    if message == 'quit':
        active = False
    else:
        print(message)
```

### 3.2 **break**: 
    要立即退出**最近的**一层循环体而不执行剩下的代码，也不管条件测试的结果如何，可使用break语句


```python
active = True
while active:
    message = input()
    
    if message == 'quit':
        break
    else:
        print(message)
```

### 3.3 **continue**： 
    若要返回循环开头，并根据条件测试的结果决定是否继续执行循环，可使用continue语句，让python忽略continue语句后的代码


```python
# 打印1~10之间的偶数
current_number = 0
while current_number <= 10:
    current_number += 1
    if current_number % 2 == 0:
        print(current_number)
    else:
        continue


2
4
6
8
10
```

    

### 3.4 **无限循环**：
    关于无限循环，有时我们需要代码一直运行下去，有时我们又希望代码能在限定的条件下停止，因此在设计代码时应对每个循环体进行测试，确保它保持我们需要的运行状态

### 3.5 **pass语句**：
    pass语句是一个空语句，python在遇到pass语句时会什么都不做，我们常常用来在编写或测试代码时将循环体内写为pass以验证代码的条件测试逻辑


```python
while True:
    pass   # 程序运行直至键盘打断(ctrl + c)

class Emptyclass():
    pass

def initlog():
    pass
```

### 3.6 **循环体中的else子句**：

    ❗没错，for、while循环节结构都可以包含else子句。

    在for循环中，else子句会在循环**成功结束最后一次迭代之后**执行

    在while循环中，else子句会在循环条件变为假值后执行


```python
# 找素数
for n in range(2,10):
    for x in range(2,n):
        if n % x == 0:
            print(n, 'equals', x, '*', n // x)
            break
    else:
        # 循环在没有找到因数的情况下结束
        print(n, 'is a prime number')

2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3
```

else子句用于此循环时比起if语句的else子句，更像try语句的。try语句的子句else在未发生异常时执行，循环的else子句则在未发生break时执行。


[上一篇(1_If_statements)](./1_If_statements.md) \| [下一篇(3_Match_statements)](./3_Match_statements.md)