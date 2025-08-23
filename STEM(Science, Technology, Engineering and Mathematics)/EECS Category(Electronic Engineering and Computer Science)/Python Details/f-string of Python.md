![[Pasted image 20250506170629.png]]
![[Pasted image 20250514200326.png]]
**in short, above pic.** 




**My favorite:**
~~~
a: int = 2

print(
    f'{a+a=:>10}'
)

>> a+a=         4      
~~~

# 1.  number display `:,` or `:_`
~~~
number: int = 1000
print(f'{number:,}')
print(f'{number:_}')

>>1,000
>>1_000

~~~

# 2. str align $\star$ `:pad_obj>num_pad`
~~~
var: str = 'var'

print(f'{var:#>5}')
>>##var
print(f'{var:#^5}')
>>#var#
print(f'{var:#<5}')
>>var##

~~~

# 3. `.numf`

~~~

n: float = 12.34

print(f'{n:.1f}')
>>12.3
~~~

# 4. f  equal $\star \star \star \star \star$ `f'{obj=}'`
~~~

a: int = 1
b: int = 2
print(f'{a+b=}')
>>a+b=3


~~~

# 6. Scientific notation of a number `:.num_be`
```
print(
f'{a_big_number:.5e}' # this means scientific notation with 5 bite of initial numbers left
)
```

# 7. nest f-string
it's a semi stupid trick
```
f_string_setting: str = '.5e'
print(
f'{num=:{f_string_setting}}'
)
```

# 8. raw string
```
a_specific_folder:str = r'...'
my_path:str = fr'halljunction\codes\...\{a_specific_folder}'
```

# 9. superposition of f-string syntax
```
print(
f'{a+b=:.2e>5}'
)
```



# 10. `!s` string form, `!r`  raw form, `!a` ascii form. 
