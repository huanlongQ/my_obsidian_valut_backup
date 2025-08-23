# 1. AttributeError: attribute not exist
~~~
>>obj has no attribute ''
~~~

# 2. ImportError: nonsense import
~~~
>>no module found named ''
~~~

# 3. IndexError: out of range

# 4. KeyError
~~~
dict['somekey']
>>KeyError: 'somekey'
~~~
# 5. NameError
~~~
>>NameError: name 'name' is not defined
~~~ 
BTW, take care of global and local scope problem. 

# 6. NotImplementError $\star \star \star \star \star$ 
~~~
de scrape_website(url: str) -> dict: 1usage
	pass # notice that you passed this func body, you want to write it latter. 
scrape_website('www.indently.io')
>> NotImplementError
~~~

# 8. SynatexError

# 9. IndentionError

# 10. ValueError and TypeError
for typeerror, use mypy