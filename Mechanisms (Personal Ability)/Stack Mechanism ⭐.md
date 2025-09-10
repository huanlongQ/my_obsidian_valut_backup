# Stack Mechanism of Task Management

In my life, i need much entertainment, especially for sleeping. therefore, i need a **stack** to arrange my entertainment items. that's it. 
It means Checklist now. 
**`urge for year, not for second.`**  

## Long Term Stack

- realized by **Obsidian CheckList** plugin. 

## Short Term Stack

- **[make a `.md` note in `(non-)Daily Work`, record your steps.]** 
	- do `DFS` first
	- then do `BFS` and **control variables**. 

## non-Work Stack 

**e.g.** 

- ![[Pasted image 20250809215618.png]]
	- 几个大块红色和afk时间用于听"抵抗系"主播录播. 
	- 1h左右用于Obsidian, 1h左右用于gemini. 
	- 2h+用于调试UTG900E. 
	- **进一步思考, 聪明的选择是将抵抗系时间挪到夜晚, 而将白天的抵抗系时间用于读书、人物与文章分析和推进Work**. 
**即为**: 
- 游玩时间 $\to$ 夜晚. 
- 白天空闲时间 $\to$ 读书.  

## Stack of Daily 

this will make me exhausted from daily stacks if more forums or etc, so switch from a forum list. [[Markson and PKM|@Markson]]

**`a forum you never surf is gonna never useful to you.`** 
-  [[Forums on Programing and Coding|@Forums on Programing and Coding]]  

# Stack Mechanism of (AI-driven) Workflow 

maybe it should be called **pipeline** sometimes. 

- get 到控制变量法的关键在于维护一个工作流栈`stack of workflow`
	- 工作流栈 **stack of workflow** 将物理层, 技术栈、具体的抽象code都放入一个栈(stack)中, 以控制变量纠错, 在这个过程中层间通信也应当被考虑. [[实习项目内容-李强公司|@实习项目内容-李强公司]] 
	- 除了纵向, 横向上 **stack of workflow**也专注于各个栈层内部各个功能实现的分化. 
		- 李志轩讲的往年设备出现的问题 [[实习项目内容-李强公司|@实习项目内容-李强公司]]
			- **位移台内光纤光栅标尺质量差.**  
			- **光源内声光调制器导致功率以8~9s为周期出现不稳定信号.** 
			- **代码忘记加入delay relaxation time.**  
		- 基础的初中电路题做法
		- [[实习项目内容-李强公司|@实习项目内容-李强公司]]中, 在HuaWeiRectReflection项目中, 我没有把可视化部分code的传参修改好, 因而出现了大的问题, 这在当时引起了一个sus-point, 但是没有注意. 
	also known as **Control Variables**. 
	[‎Gemini - Control Variables for Workflow Debugging](https://g.co/gemini/share/6d2537acfe6d) 
![[Pasted image 20250824180028.png|723]]
- 在stack mechanism的每一层stack中, 其工作资源来源有AI与具体知识内容如书籍、论坛、个人主页等的种类之分. 
	**内容三一模型**的工具型内容中, 切不可忽略AI之外的**书籍**(Manual, Handbook, Documentation)、**论坛**(Forums, Stack of ..., BBS)、**个人主页**等内容来源. [[Reading, Learning and Neuroscience Mechanism|@Reading, Learning and Neuroscience Mechanism]]  
![[Pasted image 20250813181453.png|717]] 

# Sus-point

Sus-point means suspicious or suspectable point in learning and doing things that you can see but do not want to figure. 
well, for debuging, `the magic you are looking for is in the work you are avoiding.` 

even more importanti a factor is that i need a effective method to **distinguish valuable and non-valuable** **sus-points**. 

- [[实习项目内容-李强公司|@实习项目内容-李强公司]] 
	在李强公司做的[华为矩形反射谱需求]项目中, 我尝试非polynomial chirp modulation function时, 发现输出的loss数值与nomalized spectrum plot不一致, 这是一个sus-point. 
	- 最终我们发现问题在于我的可视化阶段将chirp modulation function固定设置为了polynomial性质, 只改变`coeffs:np.ndarray`传参没有意义. 
- 面对ply, 应该如何处理关系. 这是一个重要的sus-point. 
- [[Zen|@Zen]] 's **做自己能力边界上的事情**
	能力边界上的事情由sus-point组成. 
