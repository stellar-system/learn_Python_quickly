# 1 Tuple(元组)

---------

有时为了满足创建一系列不可修改的元素，元组可以满足这一要求。Python将不能修改的值称为**不可变的**，而不可变的列表被称为元组。



```python
# 元组犹如列表，但使用圆括号但不是方括号来标识
dimensions = (50, 100)
# 尝试修改元组中的元素
dimensions[1] = 0

    ---------------------------------------------------------------

    TypeError            Traceback (most recent call last)

    d:\Studying\python-learning\learn_Python_quickly\1 变量及数据类型\JupyterNotebook\5_Tuple_Set_Dict.ipynb Cell 3 line 4
          <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/1%20%E5%8F%98%E9%87%8F%E5%8F%8A%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B/JupyterNotebook/5_Tuple_Set_Dict.ipynb#W3sZmlsZQ%3D%3D?line=1'>2</a> dimensions = (50, 100)
          <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/1%20%E5%8F%98%E9%87%8F%E5%8F%8A%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B/JupyterNotebook/5_Tuple_Set_Dict.ipynb#W3sZmlsZQ%3D%3D?line=2'>3</a> # 尝试修改元组中的元素
    ----> <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/1%20%E5%8F%98%E9%87%8F%E5%8F%8A%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B/JupyterNotebook/5_Tuple_Set_Dict.ipynb#W3sZmlsZQ%3D%3D?line=3'>4</a> dimensions[1] = 0
    

    TypeError: 'tuple' object does not support item assignment

```


```python
# 遍历元组元素，同列表使用for循环结构
# 修改元组元素，重新赋值
dimensions = (50, 100)
dimensions = (400, 100)
```

# 2 Set(集合)

--------------

集合(Set)是一个无序不重复元素的序列，使用大括号{}或set{}函数创建集合，需要注意的是，创建一个空集合必须用set{}而不是{}，因为{}用于创建一个空字典。

集合不能被切片，也不能被索引，除了做集合运算之外，集合元素可以被添加或删除。


```python
a = set(range(1,5))
print(a[0])


    -----------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    d:\Studying\python-learning\learn_Python_quickly\1 变量及数据类型\JupyterNotebook\5_Tuple_Set_Dict.ipynb Cell 5 line 2
          <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/1%20%E5%8F%98%E9%87%8F%E5%8F%8A%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B/JupyterNotebook/5_Tuple_Set_Dict.ipynb#X11sZmlsZQ%3D%3D?line=0'>1</a> a = set(range(1,5))
    ----> <a href='vscode-notebook-cell:/d%3A/Studying/python-learning/learn_Python_quickly/1%20%E5%8F%98%E9%87%8F%E5%8F%8A%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B/JupyterNotebook/5_Tuple_Set_Dict.ipynb#X11sZmlsZQ%3D%3D?line=1'>2</a> print(a[0])
    

    TypeError: 'set' object is not subscriptable
```



```python
# 添加集合元素
a_set = {1,2,3,4}
a_set.add(5)
print(a_set)


{1, 2, 3, 4, 5}
```


```python
# 删除集合元素
a_set.discard(5)
print(a_set)

{1, 2, 3, 4}
```


集合还可以用来消除列表或元组中的重复元素：


```python
a_list = [1,1,1,1,132,3,3,2,2,4,5]
a_set = set(a_list)
print(sorted(a_set))

[1, 2, 3, 4, 5, 132]
```


```python
a_tuple = (1,1,1,2,2,2,3,3,3)
a_set = set(a_tuple)
print(a_set)

{1, 2, 3}
```


    
