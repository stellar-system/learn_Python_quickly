# Dictionary(字典)

--------------------------------

在Python中，字典是一系列**键-键值**对，每个键都与一个键值相关联，可以使用键来访问与之相关联的值，这个值可以是任何类型的元素。

简言之，字典能够将相关信息关联起来。

在Python中，字典用放在花括号{}中的一系列**键-值对**表示。


```python
# 一个简单的字典示例,其中，color和points为键，green和5为值：
alien_0 = {'color': 'green', 'points': 5} 
```

## 1 使用字典


```python
# 访问字典中的值：
print(alien_0['color'])

green
```



```python
# 添加键-值对，可依次指定字典名、用方括号括起的键和相关联的值，（字典是一种动态结构）
print(alien_0)
alien_0['x_position'] = 0
alien_0['y_position'] = 25
print(alien_0)

{'color': 'green', 'points': 5}
{'color': 'green', 'points': 5, 'x_position': 0, 'y_position': 25}
```
    

**python不关心键-值对的添加顺序，而只关心键和值之间的关联关系**


```python
# 修改字典中的值,要修改字典中的值，可依次指定字典名、用方括号括起的键以及该键相关联的新值。
alien_0['color'] = 'yellow'
print(alien_0)


{'color': 'yellow', 'points': 5, 'x_position': 0, 'y_position': 25}
```


```python
# 删除键值对
del alien_0['points']
print(alien_0)


{'color': 'yellow', 'x_position': 0, 'y_position': 25}
```

    

# 2 遍历字典


```python
# 遍历所有键值对，注意要使用方法items()，他返回一个键-值对列表
for key, value in alien_0.items():
    print("\nkey:" + key)
    print("value:" + str(value))
print(type(alien_0.items()))

key:color
value:yellow

key:x_position
value:0

key:y_position
value:25
<class 'dict_items'>
```

    

**注意：即便遍历字典时，键-值对的返回顺序也与存储顺序不同**


```python
# 遍历字典中的所有键，方法keys()可省略
for name in alien_0.keys():
    print(name)

color
x_position
y_position
```

```python
# 按顺序遍历字典中的所有键
for name in sorted(alien_0.keys()):
    print(name)

color
x_position
y_position
```


```python
# 遍历字典中的所有值，使用方法values()，他返回一个值列表，而不包含任何键
for value in alien_0.values():
    print(value)

yellow
0
25
```


**这种做法提取字典中的所有值，而没有考虑是否重复。要去除重复项，可使用集合(set),集合类似于列表，但每个元素都必须是独一无二的**

## 3 嵌套

有时候需要将一系列字典存储在列表中，或将列表作为值存储在字典中，这称为嵌套。

- 字典列表： 元素为字典的列表
- 在字典中存储列表
- 在字典中存储字典

# 4 如何根据值查找对应的键

可以使用以下两种方法：

1.使用循环遍历字典的键值对，然后通过比较值来找到对应的键：


```python
for key, val in alien_0.items():
    if val == 'yellow':
        print(key)

color
```


2.使用**字典推导式**来创建一个新字典，将原字典的键值对颠倒，然后通过查找新字典的键值对来获取原字典的值：


```python
inverted_dict = {v:k for k,v in alien_0.items()}
print(inverted_dict['yellow'])

color
```

[上一篇(5_Tuple&Set)](./5_Tuple&Set.md)