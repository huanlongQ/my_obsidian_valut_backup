必备基础关键字：False/True/None 奠定逻辑与空值基础，and/or/not 构建条件判断，def/class 定义函数与类，return/yield 控制返回与生成器，让你秒懂代码骨架。 
流程控制核心：if/elif/else 实现多层条件分支，for/while 搞定循环逻辑，break/continue 灵活控制循环流程，try/except/finally 轻松处理异常，代码逻辑更清晰。 
进阶与特殊场景：async/await 解锁异步编程，lambda 创建匿名函数简化代码，with 优雅管理资源（如文件操作），match/case（Python 3.10+）实现强大模式匹配，type（3.12 + 软关键字）增强类型定义灵活性。 
避坑与最佳实践：区分is（内存地址比较）vs $\mathrm{==}$（值比较），**巧用pass 占位避免语法错误**，理解软关键字（如match/case/type）的双重用途（变量名与关键字），写出更规范代码。
# 1. notable  KeyWord
~~~
lambda
a brief func def
a: func = lambda x: x**x
print(a(2))
>>4
~~~

# 2. soft kerwords
soft keywords are special keywords that only act as keyword at specific synatcic context.
**match-case-_ clause**: a more powerful if == elif == elif == ... 
~~~
softkeywords = [
'_','match','case',  # they are utilized for match case _ clause. 
]

point = (3, 7)
match point:
    case (x, y):
        print(f"Point has coordinates x={x}, y={y}")
    case _: # means unknown in match case _ clause
        print("Not a point")
~~~
- `_` matches anything (and you can ignore it).
- You can combine patterns with `|`:
~~~
def is_vowel(ch):
    match ch.lower():
        case "a" | "e" | "i" | "o" | "u":
            return True
        case _:
            return False
~~~
