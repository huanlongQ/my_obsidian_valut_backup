
[[Indently's Python tutorial]][[KeyWords in Python]] should also be Basic Python content. Anyway it has been there. 
# 1. Generator
sace storage 
~~~
def count_up_to(n)-> GeneratorExit:
    """
    一个简单的生成器，依次输出从 1 到 n 的整数。
    No return but returned a generator
    """
    i = 1
    while i <= n:
        yield i  # notice this yield
        i += 1

# 创建生成器对象
gen = count_up_to(3)
print(gen)          # <generator object count_up_to at 0x...>

>> 1
next(gen)
>> 2
print(gen)
>> 3 
~~~

# 2. Decorator: Decorator is a functional in mathematical pespecticve. 
input a func/class output a new func/class
~~~
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}()…")
        result = func(*args, **kwargs)
        print(f"{func.__name__}() returned {result!r}")
        return result
    return wrapper


# 手动使用
def hello(name):
    return f"Hello, {name}"
  
hello = my_decorator(hello)

# 或者用 @ 语法
@my_decorator
def hello(name):
    return f"Hello, {name}"

# 调用
print(hello("Alice"))

>>Calling hello()…  Hello, Alice
>>hello() returned 'Hello, Alice'

>>Hello, Alice
~~~

# 3. 49 built in funcs


```
builtins = [
    'abs', 'aiter', 'all', 'anext', 'any', 'ascii', 'bin', 'bool',
    'breakpoint', 'bytearray', 'bytes', 'callable', 'chr', 'classmethod',
    'compile', 'complex', 'delattr', 'dict', 'dir', 'divmod', 'enumerate',
    'eval', 'exec', 'filter', 'float', 'format', 'frozenset', 'getattr',
    'globals', 'hasattr', 'hash', 'help', 'hex', 'id', 'input', 'int',
    'isinstance', 'issubclass', 'iter', 'len', 'list', 'locals', 'map',
    'max', 'memoryview', 'min', 'next', 'object', 'oct', 'open', 'ord',
    **'pow'**, 'print', 'property', 'range', 'repr', 'reversed', 'round',
    'set', 'setattr', 'slice', 'sorted', 'staticmethod', 'str', 'sum',
    'super', 'tuple', 'type', 'vars', **'zip'**, '__import__'
]

most_used_builtins = [
    'print',      # #1
    'len',        # #2
    'id',         # #3
    'range',      # #4
    'list',       # #5
    'tuple',      # #6
    'dict',       # #7
    'int',        # #8
    'zip',        # #9
    'filter',     # #10
    'enumerate',  # #11
]
```

```
	for item in zip([1, 2, 3], ['sugar', 'spice', 'everything nice']):
...     print(item)
...
(1, 'sugar')
(2, 'spice')
(3, 'everything nice')
```

# 4. Nice Features
## 4.1 `:=` combines expression and assignment
```
if is_eq := (A==B):
	print(is_eq)
```






