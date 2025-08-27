-  [zhihu - functools introduction](https://zhuanlan.zhihu.com/p/696908076)
- [functools — Higher-order functions and operations on callable objects — Python 3.13.7 documentation](https://docs.python.org/3/library/functools.html)

阅. 

```python
from functools import partial
def specifications(colour: str,name: str, amount: int) -> None:1usage
    print（f'Specs:{colour=},{name=},{amount=}.)
    
colour_and_name_specs: partial = partial(specifications, amount=10)

color_and_name_spec('red','hall junction')
>> Specs:color=red, name=hall junction,amount=10
```
