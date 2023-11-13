# 迭代器

------------------------------

到目前位置，你可能已经注意到大多数```容器对象```（在python中，容器对象是可以包含其他对象的对象，这些对象包括：list、tuple、set、dict等）都可以使用```for```语句，也就是说你可以用```for```循环来遍历容器中的每一个元素。

这种访问风格清晰简洁且方便。迭代器的使用非常普遍并使得Python成为一个统一的整体，在幕后，```for```语句会在容器对象上调用```iter()```。该函数返回一个定义了```__next__()```方法的迭代器对象，此方法将逐一访问容器中的元素，当元素用尽时，```__next__（）```将引发```StopIteration```异常来终止```for循环```。你可以使用```next()```函数来调用```__next__()```方法：


```python
>>>s = 'abc'
>>>it = iter(s)
>>>it

>>>print(next(it)) # 这两种方式都可以
>>>print(it.__next__())
>>>print(next(it))

a
b
c
```

    

了解迭代器协议背后的机制后，就可以为你的自定义的类添加迭代器行为了。定义```__iter__()```方法用于返回一个带有```__next__()```方法的对象，如果类已经定义了```__next__()```，那么```__iter__()```可以简单地返回```self```:


```python
>>>class Reverse():
        """Iterator for looping over a sequence backwards
        
        一个用于反向循环序列的迭代器"""
        def __init__(self, data):
            self.data = data
            self.index = len(data)

        def __iter__(self):
            return self
        
        def __next__(self):
            if self.index == 0:
                raise StopIteration
            self.index = self.index - 1
            return self.data[self.index]
    
>>>rev = Reverse('spam')
>>>iter(rev)
>>>for char in rev:
        print(char)
  
m
a
p
s
```

    

因此，如何初步实现一个迭代器的方法就明晰了。首先，我们在类定义中添加```__iter__(self)```方法，使这个方法返回类本身，即```return self```这是因为```for```循环语句会调用类中的该方法。然后我们定义一个```__next__(self)```方法，在该方法下定义对象实例在```for```语句下会进行什么样的动作。

[上一篇(2_inheritance)](./2_inheritance.md) | [下一篇(4_generator)](./4_generator.md)