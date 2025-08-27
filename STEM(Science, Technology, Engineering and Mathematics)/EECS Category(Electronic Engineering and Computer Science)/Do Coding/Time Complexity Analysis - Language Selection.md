# Programming language selection

## python

- `python` 是解释型语言, 使用`interpreter`, `cpp`等是编译型语言, 使用`compiler`.
	- `compiler`会在运行前就将代码转为汇编语言, 而`interpreter`是边运行边编译. 因此, `python`的`for loop`会显著得慢. 
	- `python`中也有`jit(just in time)`等即时编译功能. 
- `python`有`gil(general interpreter lock)`, 只允许同时存在一个`thread`. 

**cases:**
- [将Python代码改为c++代码,性能会提高吗？](https://www.zhihu.com/question/1899971674029393124/answer/1903935506003269052)  
	- find **bottleneck** of time complexity. 这事不能靠拍脑袋，得靠定位性能瓶颈。记住两个字：**profile！**
	- 可以尝试语言调用. 
	- [Gemini - Python vs C++ 科学计算性能比较](https://g.co/gemini/share/553eb8d20816) 

-  [将Python代码改为c++代码,性能会提高吗](https://www.zhihu.com/question/1899971674029393124/answer/1903935506003269052) 
