# print()函数

----------------------------------

print函数用于打印或输出给定参数

print()函数的定义如下：

```python
def print(
    *values: object,
    sep: str | None = " ",
    end: str | None = "\n",
    file: SupportsWrite[str] | None = None,
    flush: Literal[False] = False,
) -> None: ...
```

这是Python built-in函数print的类型解释，它接收以下参数：
- *values: object : 可变数量的参数，表示要打印的值。这意味着，我们在使用print时，不一定只能输出一个变量或字符串。
- sep: str | None = " " : 表示值之间的分隔值，默认为一个空格。
- end: str | None = "\n" : 表示打印结束后要添加的字符，默认为换行符。（因此每次打印结束后，会默认进入下一行）
- file: SupportsWrite[str] | None = None : 表示要将输出写入的文件对象，默认为标准输出sys.stdout。通过将一个文件对象传递给file参数，你可以将print函数的输出写入到指定文件中，而不是默认的标准输出（终端）。
- flush: Literal[False] = False : 表示是否刷新输出缓冲区，默认为False。
- 返回值：函数的返回类型为None，即没有返回值


```python
# 参数1 接收多个传入参数
print('aaa', 'bbb')

aaa bbb
```

    


```python
# 参数2 修改值之间的分隔值为‘ and ’
print('aaa', 'bbb', sep=' and ')

aaa and bbb
```

    


```python
# 参数3 修改文件结束字符为' !'
print('aaa', end='!')

aaa!
```


```python
# 参数4 将输出写入到文件
with open('test_print.txt', 'a') as f:
    print('aa', 'bbb', file=f)
```

👆使用这种方法时，需要注意文件的打开方式为附加模式，否则会覆盖原文件


```python
# 参数5 将缓冲区刷新
import time

for i in range(5):
    print(f"Processing step {i+1}...")
    time.sleep(3)
    print("Step completed.", flush=True)

print("Program finished!")

Processing step 1...
Step completed.
Processing step 2...
Step completed.
Processing step 3...
Step completed.
Processing step 4...
Step completed.
Processing step 5...
Step completed.
Program finished!
```

    

🛎️刷新缓冲区是指将缓冲区中的数据立即写入到输出设备（终端或文件）中，在Python中，print函数默认情况下不会立即将输出写入到终端，而是先将输出存储在缓冲区中，然后在适当的时机将缓冲区的内容写入到终端。

当flush的参数设置为True时，表示要立即刷新缓冲区，即将缓冲区中的内容立即写入到输出设备中，这在某些情况下很有用。例如当你希望立即将输出显示在终端上，而不是等到缓冲区满或程序结束时才显示。

以下是一些可能需要使用flush=True的情况：

1. 实时日志记录：如果你正在编写一个需要实时记录日志的应用程序，你可能希望将日志消息立即显示在终端或日志文件中。

2. 长时间运行的程序：当你有一个长时间运行的程序，需要逐步输出一些信息时。

3. 调试和排除故障：在调试和故障排除过程中，你可能希望立即将某些信息显示在终端上，以便更好地理解程序的执行流程和状态。

❗使用flush=True会频繁地将输出写入到输出设备，可能会对程序的性能产生影响。因此只在必要时使用，以避免不必要的性能开销。


