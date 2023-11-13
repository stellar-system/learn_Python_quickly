# match语句

--------------------------

match语句接受一个表达式并把它的值与一个或多个 case 块给出的一系列模式进行比较。这表面上像 C、Java 或 JavaScript（以及许多其他程序设计语言）中的 switch 语句，但其实它更像 Rust 或 Haskell 中的模式匹配。只有第一个匹配的模式会被执行，并且它还可以提取值的组成部分（序列的元素或对象的属性）赋给变量。

## 1 模式匹配用法


```python
# 最简单的形式是将一个主语值与一个或多个字面值进行比较：
>>>def http_error(status):
        match status:
            case 400:
                return "Bad request"
            case 404:
                return "Not found"
            case 418:
                return "I'm a teapot"
            case 401 | 403: # 你可以用 | （“或”）将多个字面值组合到一个模式中：
                return "Not allowed"
            case _:
                return "Something's wrong with the internet"

>>>http_error(404)

'Not found'
```

注意最后一个代码块：**变量名_** 被作为**通配符**并必定会匹配成功，因此其必须被放在代码末尾，否则会导致在其后面的代码块失效。如果没有 case 匹配成功，则不会执行任何分支。



## 2 解包赋值模式用于绑定变量


```python
>>>a = input('please enter number1 :')
>>>b = input('please enter number2 :')
>>>point = (a,b)
# point is an (x,y) tuple
>>>match point:
        case (0,0):
            print("Origin")
        case (0, y):
            print(f"Y={y}")
        case (x, 0):
            print(f"X={x}")
        case (x, y):
            print(f"X={x}, Y={y}")
        case _:
            raise ValueError("Not a point")

X=1, Y=2
```


第一个模式有两个字面值，可视为前述字面值模式的扩展。接下来的两个模式结合了一个字面值和一个变量，变量 绑定 了来自主语（point）的一个值。第四个模式捕获了两个值，使其在概念上与解包赋值 (x, y) = point 类似。

## 3 类名后接参数列表将属性捕获到变量


```python
class Point():
    __match_args__ = ('x', 'y')
    def __init__(self, x, y):
        self.x = x
        self.y = y

def where_is(point):
    match point:
        case Point(x=0, y=0):
            print("Origin")
        case Point(x=0, y=y):
            print(f"Y={y}")
        case Point(x=x, y=0):
            print(f"X={x}")
        case Point():
            print("Somewhere_else")
        case _:
            print("Not a point")
```


```python
>>>point = Point(3,5)
>>>where_is(point)


Somewhere_else
```

    

一些内置类（如 dataclass）为属性提供了一个顺序，此时，可以使用位置参数。自定义类可通过在类中设置特殊属性  ```__match_args__```，为属性指定其在模式中对应的位置。若设为 ("x", "y")，则以下模式相互等价（且都把属性 y 绑定到变量 var）：

```python
Point(1, var)
Point(1, y=var)
Point(x=1, y=var)
Point(y=var, x=1)
```

建议这样来阅读一个模式——通过将其视为赋值语句等号左边的一种扩展形式，来理解各个变量被设为何值。match 语句只会为单一的名称（如上面的 var）赋值，而不会赋值给带点号的名称（如 foo.bar）、属性名（如上面的 x= 和 y=）和类名（是通过其后的 "(...)" 来识别的，如上面的 Point）。

模式可以任意嵌套。举例来说，如果我们有一个由 Point 组成的列表，且 Point 添加了 ```__match_args__``` 时，我们可以这样来匹配它：

```python
>>>class Point:
        __match_args__ = ('x', 'y')
        def __init__(self, x, y):
            self.x = x
            self.y = y

>>>match points:
        case []:
            print("No points")
        case [Point(0, 0)]:
            print("The origin")
        case [Point(x, y)]:
            print(f"Single point {x}, {y}")
        case [Point(0, y1), Point(0, y2)]:
            print(f"Two on the Y axis at {y1}, {y2}")
        case _:
            print("Something else")
```

我们可以为模式添加 if 作为守卫子句。如果守卫子句的值为假，那么 match 会继续尝试匹配下一个 case 块。注意是先将值捕获，再对守卫子句求值：

```python
>>>match point:
        case Point(x, y) if x == y:
            print(f"Y=X at {x}")
        case Point(x, y):
            print(f"Not on the diagonal")
```

该语句的一些其它关键特性：

- 与解包赋值类似，元组和列表模式具有完全相同的含义并且实际上都能匹配任意序列，区别是它们不能匹配迭代器或字符串。

- 序列模式支持扩展解包：[x, y, *rest] 和 (x, y, *rest) 和相应的解包赋值做的事是一样的。接在 * 后的名称也可以为 `_`，所以 (x, y, *_) 匹配含至少两项的序列，而不必绑定剩余的项。

- 映射模式：{"bandwidth": b, "latency": l} 从字典中捕获 "bandwidth" 和 "latency" 的值。额外的键会被忽略，这一点与序列模式不同。**rest 这样的解包也支持。（但 **_ 将会是冗余的，故不允许使用。）

- 使用 as 关键字可以捕获子模式：

```python
>>>case (Point(x1, y1), Point(x2, y2) as p2): ...
```
将把输入中的第二个元素捕获为 p2 （只要输入是包含两个点的序列）

- 大多数字面值是按相等性比较的，但是单例对象 True、False 和 None 则是按 id 比较的。

- 模式可以使用具名常量。它们必须作为带点号的名称出现，以防止它们被解释为用于捕获的变量：

```python
>>>from enum import Enum
>>>class Color(Enum):
        RED = 'red'
        GREEN = 'green'
        BLUE = 'blue'

>>>color = Color(input("Enter your choice of 'red', 'blue' or 'green': "))

>>>match color:
        case Color.RED:
            print("I see red!")
        case Color.GREEN:
            print("Grass is green")
        case Color.BLUE:
            print("I'm feeling the blues :(")
```

[上一篇(2_Loop_structure)](./2_Loop_structure.md)