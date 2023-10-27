# List 列表

---------------------

**列表由一系列按特定顺序排列的元素组成**且列表元素可以是任何类型，在python中，通常用方括号（[]）来表示列表，并用逗号（，）来分隔其中的元素


```python
# bicycles.py
>>>bicycles = ['trek', 'cannondale', 'redline', 'specialized']
>>>print(bicycles)

['trek', 'cannondale', 'redline', 'specialized']
```

    

## 1 访问列表及搜索元素

列表是有序集合，因此要访问列表中的任何元素，只需将该元素的位置或索引（index）告诉Python即可。**列表的索引值是从0开始而非从1开始**
Python为访问列表的靠后元素提供了一种特殊语法，通过将索引指定为负值，可让Python返回倒数某位的元素值。**仅当列表为空时，这种访问最后一个元素的方式才会导致错误**

若要搜索列表中某一元素，返回其索引值，可使用index()方法：


```python
>>>week = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']
>>>week.index('Wednesday')

2
```

## 2 列表的增删改


```python
## 修改列表元素
>>>motorcycles = ['honda', 'yamaha', 'suzuki']
>>>print(motorcycles)

>>>motorcycles[0] = 'ducati'
>>>print(motorcycles)

['honda', 'yamaha', 'suzuki']
['ducati', 'yamaha', 'suzuki']
```


    


```python
## 在列表中添加元素
>>>motorcycles = ['honda', 'yamaha', 'suzuki']
# 1.在列表末尾添加元素append()
>>>motorcycles.append('ducati')
>>>print(motorcycles)

# 2.在列表中插入元素insert(index, 元素)，这种操作将列表中所有在index及其之后的元素向右移一个位置
>>>motorcycles.insert(0, 'ducati')
>>>print(motorcycles)

['honda', 'yamaha', 'suzuki', 'ducati']
['ducati', 'honda', 'yamaha', 'suzuki', 'ducati']
```


    


```python
## 在列表中删除元素
>>>motorcycles = ['honda', 'yamaha', 'suzuki']
# 1.使用del语句删除元素,此操作将列表中所有被删除元素右侧的元素向左移一个位置
>>>print(motorcycles)
>>>del motorcycles[1]
>>>print(motorcycles)
>>>print('\n')

['honda', 'yamaha', 'suzuki']
['honda', 'suzuki']

# 2.使用方法pop()删除元素，方法pop()删除列表末尾的元素，列表就像一个栈，而删除末尾元素相当于弹出栈顶元素
#   此方法将元素从列表中删除，但可以接着使用它
>>>motorcycles = ['honda', 'yamaha', 'suzuki']
>>>print(motorcycles)
>>>popped_motorcycle = motorcycles.pop()
>>>print(motorcycles)
>>>print(popped_motorcycle)
>>>print('\n')

['honda', 'yamaha', 'suzuki']
['honda', 'yamaha']
suzuki

# 3.弹出列表中任何位置的元素，实际上，方法pop()可以用来弹出列表中的任意一个元素，只需要在括号中指定要删除的元素的索引即可
>>>motorcycles = ['honda', 'yamaha', 'suzuki']
>>>print(motorcycles)
>>>firsy_motorcycle = motorcycles.pop(0)
>>>print(motorcycles)
>>>print(firsy_motorcycle)
>>>print('\n')

['honda', 'yamaha', 'suzuki']
['yamaha', 'suzuki']
honda

# 4.根据值删除元素，使用remove()方法可以根据括号中提供的值删除元素,若有多个值相同的元素，该方法只删除索引值最小的那个
>>>motorcycles = ['honda', 'yamaha', 'suzuki']
>>>print(motorcycles)
>>>motorcycles.remove('honda')
>>>print(motorcycles)

>>>numbers = [1, 1, 2, 1, 1, 1]
>>>numbers.remove(1)
>>>print(numbers)

['honda', 'yamaha', 'suzuki']
['yamaha', 'suzuki']
[1, 2, 1, 1, 1]

```


    

## 3 组织列表
以特定的顺序显示列表元素


```python
## 1.使用方法sort()对列表进行永久性排序
>>>cars = ['bmw', 'audi', 'toyota', 'subaru']
>>>print(cars)
>>>cars.sort()
>>>print(cars)
>>>cars.sort(reverse=True) # 按照字母反向排列只需要传入参数reverse=True
>>>print(cars)
>>>print('\n')

['bmw', 'audi', 'toyota', 'subaru']
['audi', 'bmw', 'subaru', 'toyota']
['toyota', 'subaru', 'bmw', 'audi']

## 2.使用函数sorted()对列表进行临时排序，即保留原列表的排序，也接受传入参数reverse
>>>cars = ['bmw', 'audi', 'toyota', 'subaru']
>>>print(cars)
>>>print(sorted(cars))
>>>a = sorted(cars)
>>>print(a)
>>>print(cars)
>>>print('\n')

['bmw', 'audi', 'toyota', 'subaru']
['audi', 'bmw', 'subaru', 'toyota']
['audi', 'bmw', 'subaru', 'toyota']
['bmw', 'audi', 'toyota', 'subaru']

## 3.使用方法reverse()永久性的反转列表元素的排列顺序
>>>cars = ['bmw', 'audi', 'toyota', 'subaru']
>>>print(cars)
>>>cars.reverse()
>>>b = cars[::-1] # 方向切片列表整体可以达到一样的目的
>>>print(cars)
>>>print(cars)

['bmw', 'audi', 'toyota', 'subaru']
['subaru', 'toyota', 'audi', 'bmw']
['subaru', 'toyota', 'audi', 'bmw']

## 4.确定列表的长度
>>>len(cars)

4
```


## 4 遍历整个列表
通过for循环进行遍历


```python
>>>magicians = ['alice', 'david', 'carolina']
>>>for magician in magicians: # 临时变量magician可指定任何名称
        print(magician) # for循环体内的每行代码，缩进是必要的

alice
david
carolina
```


    

## 5 创建数值列表


```python
## 1.使用函数range(a,b,c),数值域为[a,b),其中c为取值的步长
>>>for value in range(1,5):
        print(value)

1
2
3
4
```


    


```python
## 2.使用range()创建数字列表
>>>print(type(range(1,5)))
>>>numbers = list(range(1,5))
>>>print(numbers)
>>>print(type(numbers))

<class 'range'>
[1, 2, 3, 4]
<class 'list'>
```


```python
## 3.对数字列表执行简单的统计计算
>>>digits = list(range(1,11))
>>>min(digits) # 取最小值
>>>max(digits) # 取最大值
>>>sum(digits) # 求和

55
```


## 6 列表解析
思考如何生成一个列表，将前十个整数的平方加入到一个列表中，常规的使用for循环的方法为：


```python
>>>squares = []
>>>for value in range(1,11):
        squares.append(value**2)
>>>print(squares)

[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```


如果使用列表解析，一行代码即可实现：


```python
>>>squares = [value**2 for value in range(1,11)]
>>>print(squares)

[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```


## 7 列表切片
要创建切片，可指定要使用的第一个元素和最后一个元素的索引。与range()函数一样，python在到达指定的第二个索引前面的元素后停止。


```python
>>>players = ['charles', 'martina', 'michael', 'florence', 'eli'] 
>>>print(players[0:3]) # 实际打印索引为0，1，2的元素

['charles', 'martina', 'michael']
```


```python
# 若不指定第一个索引，切片将从列表开头开始,不指定第二个索引同理
>>>print(players[:4])

['charles', 'martina', 'michael', 'florence']
```
    


```python
# 同样，第一个索引可以从负数开始
>>>print(players[-3:])

['michael', 'florence', 'eli']
```

- 要遍历列表中的部分元素，可在for循环中使用列表切片：

    for player in players[:3]:

- 要复制列表，可创建一个包含整个列表的列表切片，方法是同时省略起始索引和终止索引：

    old_players = players[:]

    倘若我们只是简单的将players赋值给old_players，如 old_players = players 则行不通，在这种方法下，old_players与players指向的实际上是同一个列表
