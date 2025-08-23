![[Pasted image 20250506204727.png]]
**in short i have this fancy pic.** 

# 1. use `if __name__=='__main__': `

# 2. integrate different modules into a `main()` func. 

# 3. seprate unit functions, improve reusability. 

A module should conclude as less as possible unit function.
[[Vibe coding]] shows this principle also. 

# 4. Type Annoation

```python 
num: int = 10 # better
num = 10 # worse

def func(
arg1: type1,
...
)->typeoutput
```
this is related to `mypy` pkg and extension

# 5. list comprehensions

```
names: list[str] = ['James', 'Charlotte', 'Stephany', 'Mario', 'Sandra']
long_names: list[str] = [name for name in people if len(p)  7]
print(f'Long names: {long_names}')
```
