# 继承

-----------------------------

## 1 通过继承创建派生类

编写类时，并非总是要从空白开始，如果你要编写的类是另一个现成类的特殊版本，可使用**继承**。一个类继承另一个类时，它将自动获得另一个类的所有属性和方法；原有的类称为**父类**，而新的类称为**子类**。子类继承其父类的所有属性和方法，同时还可以定义自己的属性和方法。

派生类定义的语法如下所示：
```python
class DerivedClassName(BaseClassName):
    <statement-1>
    .
    .
    .
    <statement-N>
```

名称```BaseClassName```必须定义于可从包含所派生的类的定义的作用域访问的命名空间中。

派生类定义的执行过程与基类相同。 当构造类对象时，基类会被记住。 此信息将被用来解析属性引用：**如果请求的属性在类中找不到，搜索将转往基类中进行查找**（注：要实现这一前提需要在子类的__init__方法中调用父类的初始化函数，否则也无法查找到未被明文定义的子类属性）。 如果基类本身也派生自其他某个类，则此规则将被递归地应用。


```python
>>>class A():
        def __init__(self):
            self.a = 1
            self.b = 2
        
        def prinA(self):
            print('a')

>>>class B(A):
        def __init__(self):
            # 当我们在子类中需要调用父类的方法时，可以使用super()函数
            super().__init__()
            self.c = 3

# 实例化一个子类B()的对象
>>>obj = B()

# 若没有super().__init__()，则对象obj的a属性不存在
>>>print(obj.a)

# 对于父类中的方法，则没有此项规则，可以直接调用
>>>obj.prinA()


1
a
```

    

派生类可能会重写其基类的方法。 因为方法在调用同一对象的其他方法时没有特殊权限，所以基类方法在尝试调用同一基类中定义的另一方法时，可能实际上调用是该基类的派生类中定义的方法。


```python
>>>class A():
        def __init__(self):
            self.a = 1

        def printA(self):
            print('a')

        def use_printA(self):
            self.printA()

>>>class B(A):
        def __init__(self):
            super().__init__()
            self.c = 3

        def printA(self):
            print('b')

>>>obj_a = A()
>>>obj_b = B()

>>>obj_a.use_printA()
>>>obj_b.printA()
# obj_b对象调用use_print方法时，不会调用基类中定义的printA函数，而是派生类B所定义的printA函数
>>>obj_b.use_printA()


a
b
b
```

Python有两个内置函数可被用于继承机制：

- 使用```isinstance()```来检查一个实例的类型:
  
  ```isinstance(obj, int)```仅会在```obj.__class__```为```int```或某个派生自```int```的类时为```True```。

- 使用```issubclass()```来检查类的继承关系:
  
  ```issubclass(bool, int)```为```True```，因为```bool```是```int```的子类（在Python中，bool类型的True和False实际上就是整数1和0的别名，可以通过简单的运算来验证：True+True的结果是2）。 但是，```issubclass(float, int)```为```False```，因为```float```不是```int```的子类。


```python
>>>True + True

2
```


## 2 多重继承

Python也支持一种多重继承。带有多个基类的类定义语句如下所示：

```python
class DerivedClassName(Base1, Base2, Base3):
    <statement-1>
    .
    .
    .
    <statement-N>
```

对于多数目的来说，最简单的情况下，你可以认为搜索从父类所继承属性的操作是```深度优先、从左到右的```，当层次结构存在重叠时不会再同一个类中搜索两次。因此，如果某个属性在```DerivedClassName```中找不到，就会在Base1中搜索它，然后（递归的）在Base1的基类中搜索，如果在那里也找不到，就将在Base2中搜索，以此类推。

真实情况较上述更为复杂，```方法解析顺序(MRO)```会动态的改变以支持对```super()```的协同调用。MRO是一个用于确定属性和方法查找顺序的规则，在Python中，MRO是从左到右的，也就是说，在定义类时，左边的类会被优先考虑。


```python
>>>class Base1():
        def __init__(self):
            self.a = 1

        def method(self):
            print("This method is from Base1.")

>>>class Base2():
        def __init__(self):
            self.b = 2

        def method(self):
            print("This method is from Base2.")

>>>class DerivedClass(Base1, Base2):
        def __init__(self):
            super().__init__()
            Base2.__init__(self)
            self.c = 3

        def method(self):
            print("This method is from DerivedClass")
            Base2().method()

>>>obj = DerivedClass()

>>>m = obj.method
>>>print(m.__self__) # 带有m()方法的实例对象
>>>print(m.__func__) # 该方法所对应的函数对象

>>>try:
        print(obj.a)
        print(obj.b)
        obj.method()
>>>except AttributeError:
        pass

<__main__.DerivedClass object at 0x0000023198A54D10>
<function DerivedClass.method at 0x0000023197BEB920>
1
2
This method is from DerivedClass
This method is from Base2.
```


    

考虑到MRO的存在，当你在定义一个从多个父类继承的子类时，有两点需要注意：

- 1.从第一个父类继承属性时，可通过```super().__init__()```方法初始化从第一父类继承的属性，若要初始化第二个及之后的父类的属性时，需要直接使用```Base2.__init__(self)```，即直接通过类名来调用类的属性，只需要手动传入self参数。

- 2.若父类中存在同名方法且子类需要调用该同名方法时，直接调用会默认使用第一父类的该方法，若要使用第二及之后的父类方法，也应该直接通过类名调用```Base2.MethodName```

## 3 私有变量

那种仅限从一个对象内部访问的”私有“实例变量在Python中并不存在，但是，大多数Python代码都遵循这样一个约定：带有一个下划线的名称(例如```_spam```)应该被当做是API的非公有部分(无论他是函数、方法或数据成员)。

由于存在对于私有类成员的有效使用场景（例如避免名称与子类所定义的名称相冲突），因此存在对此种机制的优先支持，称为```名称改写```，任何形式为```__spam```的标识符（至少都带有两个前缀下划线，至多一个后缀下划线）的文本将被替换成```_classname__spam```，其中```classname```为去除了前缀下划线的当前类名称。这种改写不考虑标识符的句法位置，只要它出现在类定义内部就会进行。

名称改写有助于让子类重载方法而不破坏方法内调用，例如：


```python
>>>class Mapping():
        def __init__(self, iterable):
            self.items_list = []
            self.__update(iterable)

        def update(self, iterable):
            for item in iterable:
                self.items_list.append(item)

        __update = update  # privacy copy of original update() method

>>>class MappingSubclass(Mapping):
        def update(self, keys, values):
            # provides new signature for update()
            # but does not break __init__()
            for item in zip(keys, values):
                self.items_list.append(item)

```

上面的实例即使在```MappingSubclass```引入了一个```__update```标识符的情况下也不会出错，因为它会在```Mapping```类中被替换为```_Mapping__update```而在```MappingSubclass```类中被替换为```_MappingSubclass__update```

请注意，改写规则的设计主要是为了避免意外冲突；访问或修改被视为私有的变量仍然是可能的。这在特殊情况下甚至会很有用，例如在调试器中。

注意点：

1. 创建子类时，父类必须包含在当前文件中，且位于子类前面。

2. 定义子类时，必须在括号内指定父类的名称。

3. super()是一个特殊函数，帮助PYthon将父类和子类关联起来，这行代码让Python调用父类的__init__()方法，让子类实例包含父类所有属性，父类也成为**超类(superclass)**

4. 重写父类的方法，对于父类的方法，只要他不符合子类模拟的实物的行为，都可对其进行重写。为此，可在子类中定义一个这样的方法，即它与要写的父类方法同名，这样，Python不会考虑这个父类方法，而只关注你在子类中定义的相应方法。

5. 将实例用作属性：在使用代码模拟实物时，你可能会发现自己给类添加的细节越来越多，属性和方法清单以及文件都越来越长。在这种情况下，可能需要将类的一部分作为一个独立的类提取出来，放到另一个类中，并将该类实例用作前一类的属性。

## 4 导入类

1. 导入单个类：car.py只包含一个类Car()，from car import Car

2. 在一个模块中存储多个类：可根据需要在一个模块中存储任意数量的类，car.py中包含Car(),ElectricCar(),Battery()等多个类

3. 从一个模块中导入多个类：可根据需要在程序文件中导入任意数量的类，from car import Car, ElectricCar

4. 导入整个模块：可以先导入模块，再用句点表示法访问需要的类，import car, 调用时car.Car()

5. 导入模块中的所有类：from module_name import * (不推荐使用，1.没有明确指明使用了哪些类，2.可能引发名称方面的错误，因为这种导入方法在调用时无需使用句点表示法)

[上一篇(1_class)](./1_class.md)