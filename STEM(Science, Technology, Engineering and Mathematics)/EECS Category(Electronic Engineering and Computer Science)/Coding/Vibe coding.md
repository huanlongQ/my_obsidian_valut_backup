
**`the key is to know the workflow, the structure, the feature, the specific conceptions while vibing.`** 
- like `callback, buffer, grabber, handle`

# 1. give shot 

i need a func/class that its function is balabala. 
~~~python
def func(
	arg1:type1, then detailed desc
	arg2:type2, then detailed desc
	arg3:type3, then detailed desc
	)-> type output
    # detailed process
    detailed process
    return output
~~~

I should give a shot for ai. 

# 2. fix crucial nodes in the code

**Nodes Control** 
check every node to make sure the validation. 

~~~python 
def func(
	arg1:type1, then detailed desc
	arg2:type2, then detailed desc
	arg3:type3, then detailed desc
	)-> type output
	detailed process: 
	node1: convert arg1 to arg1'
	fix shape is shape1 to shape1'
	node2: 
	node3: 
	return output
~~~

# 3. Modularize every single process, use api in main code body. 

A module should conclude as less as possible unit function. 

define many many modularized funcs first and then call them at a big func. 
this makes the whole code decoupled and eaiser to edit. 

# 4. prompt engineering

- `via words/via formulism/via graph/via pesudo code`
- `by nodes`, `by step/procedure`, `by ...`
- `timeline of events`
- `rewrite`
- `by the way, ` BTW can be used to add parallel ability to our human-LLM interactive workflow. 
- `someworkflow aside, recall someworkflow`, aside and recall enable us to jump form a main stream workflow and go to a branch. 
- `both in code and in real life` slove the problem that AI always give a real life but useless vague ambiguous case. 
- **Reconstruct context by transverse BEST(Basic Elements Structure Thinking) and longitudinal single element analysis.**  

## Code Review Prompt

Now, this could be better with `by nodes`. 
```

here is a source code. its main body is ****.

plz explain this code by crucial sequential nodes(AKA objs) in the main body via pesudo code, words desc, and formulism like below: 
- Node 1
codeblock{
node1:type_annotation_of_node1_obj(
arg1_of_node_1:type_of_arg, #shape_of_arg1(if possible)
arg2_of_node_2:..., ...
)->output_of_node1:type_of_output
} 
words desc with necessary code terms 
formulism 
- Node 2 
...
remember to render the LaTeX. 
```

this one based on `steps` term is totally bullshit. 
```
here is a source code whose main body is ****.

plz explain this code by crucial sequential steps in the main body via words desc, formulism and pesudo code like below:  #pesudo code should be in code block, words desc should be out of code block, formulism should be LaTeX rendered fashion
- Step 1
for obj_i in objs:
	code block{
	obj_i_:type_annotation_of_node1_obj(
	arg1_of_node_1:type_of_arg, # shape_of_arg1(if possible) \n
	arg2_of_node_1:..., #... \n
	arg3 ...
	)->output_of_node1:type_of_output # shape_of_output
	}
	words desc
	formulism
- Step 2
...
```

## API Search Prompt

Notice not to fix the specific form or shape of the objs to tightly, that may cuz huge reduction of searched space. 
```
I need a [api/pkg] that [] based on [], what pkg or api can i choose? 
it should obey: 
[a abstract restriction] or [a input-output mapping relation]
```

## Templated Notes

```
按照下述结构给我总结上述chat, 输出为md格式. 使用****.
# 研究对象(object):
## 事实性属性(objective feature):
## 价值性属性(evaluative feature):
## 规律原理(principle):
## 可操作点(operations on object):
## 应用场景(application scenario):
## 与对位产品的对比(comparison with alternatives):
## 对话关切与解释(concerns and interpretations in chat):
```
