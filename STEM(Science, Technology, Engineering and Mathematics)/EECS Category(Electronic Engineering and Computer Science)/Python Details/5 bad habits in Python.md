![[Pasted image 20250506211132.png]]
**fancy pic**. 

# 1. Never edit list while iter it. Dynamic struct is dangerous. 
~~~
channels: list[str] = ['Carberra', 'Indently', 'ArjanCodes', 'bool']
channels_temp: list[str] = []
for i, channel in enumerate(channels):
	if channel == 'Indently':
		channels.remove(channel)
	print(i, channel)
print(channels)
~~~
**Dynamic struct is dangerous, use tmp file instead. **

# 2. use try exception
**No way in real work.** 

# 3. endless if else nesting
~~~
if bool1:
	if bool2:
		if bool3:
		code body
		else: 
	else:
else:
~~~

use if not instead. this could ***decouple*** everything. 
~~~
if not bool1:
	...

if not bool2:
	...

if not bool3:
	...
~~~


# 4. avoid recurison
use **dynamical programing** or **BFS, DFS** instead. Recursion cost too too much. 

# 5. never use default arg: list=\[\]
\[\] itself point to a fixed id. 
if call this func twice and the first time edited list, then the second initial list is edited too. 
