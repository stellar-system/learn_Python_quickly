#  input()函数

-------------------------------

函数input()让程序停止运行，等待用户输入一些文本，获取用户输入后，python将其存储在一个变量中方便调用

input()函数的定义如下：

```python
def input(__prompt: object = "") -> str: ...
```

这是Python built-in函数input()的类型注解，它接收一个可选的__prompt参数，该参数的默认值为空字符串。函数返回一个字符串，可以将返回值赋给某一变量。input函数用于从用户获取输入，并将用户输入作为字符串返回。如果提供了__prompt参数，它将作为提示显示给用户。

input()在help函数中的解释

```input(prompt='', /)```

Read a string from standard input.  The trailing newline is stripped.

The prompt string, if given, is printed to standard output without a
trailing newline before reading input.

If the user hits EOF (*nix: Ctrl-D, Windows: Ctrl-Z+Return), raise EOFError.
On *nix systems, readline is used if available.


```python
msg = input("Tell me something, and I will repeat it back to you: ")
print(msg)

Tell me something, and I will repeat it back to you: mesg
mesg
```


    

注意：input()方法会默认将用户输入存储为str格式，若需要的变量为int或其他类型，需要进行类型转换


```python
num = input('tell me a number: ')
print(num)
print(type(num))
num = int(num)
print(type(num))

1
<class 'str'>
<class 'int'>
```


    
