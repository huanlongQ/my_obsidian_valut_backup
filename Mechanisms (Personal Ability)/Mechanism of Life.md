# 学习-思考-执行的并行模式

- 尽可能实现学习, 思考和执行的并行模式, 避免***学而不思则罔, 思而不学则殆***的困境. 
- 学习内容、思考内容相对容易确定, 而执行内容难以确定. 需要建立一个机制来最低限度地选择一个可接受的执行内容. 
	$\mathbf{MR.CEOL\ 1.0}$
	
	$\mathbf{CEOL(Chief \ Executive\  Officer\  of\  Life)  1.0}$ 
		当在英文语境中看到 "ceol" 时，尤其在与音乐（特别是爱尔兰或苏格兰音乐）相关的讨论中，应将其理解为盖尔语中“音乐”的意思，并发音近似为 **"kyohl"/kyoːl/**。
	设定一个$\mathbf{Accessible\ Project\  Set }$, 为该可接受项目集合设定一个$\mathbf{DDL}$, 一旦超过这个DDL且没有找到更加优质的idea, 就必须从该项目集合中按接受度顺序选不少于一个项目开始执行. 
	考虑到**避免盲目执行**, 这个DDL的设计必须相对远(按月级别设计), 以避免$\mathbf{CEOL}$拖DDL到直接执行可接受项目集而不去有效寻找优质idea.
	在寻找优质idea方面, 需要建立一个**挖矿机机制**$\mathbf{MR(Mining \ Rig)\ 1.0}$. 
		Mr. 是 Mister 的缩写, Mister 源自 Master, 所以，从词源学的角度看，**Master** 可以被认为是 "Mr." 最终的“词根”或起源词。
	在这个机制下, 需要设立一恶搞$\mathbf{Mine \ Set}$, 在Mine Set内工作进行选矿, 知道出现优质idea. 

# Sus-point

Sus-point means suspicious or suspectable point in learning and doing things that you can see but do not want to figure. 
well, for debuging, `the magic you are looking for is in the work you are avoiding.` 

- [[实习项目内容-李强公司|@实习项目内容-李强公司]] 
	在李强公司做的[华为矩形反射谱需求]项目中, 我尝试非polynomial chirp modulation function时, 发现输出的loss数值与nomalized spectrum plot不一致, 这是一个sus-point. 
	- 最终我们发现问题在于我的可视化阶段将chirp modulation function固定设置为了polynomial性质, 只改变`coeffs:np.ndarray`传参没有意义.  [[Stack Mechanism ⭐|@Stack Mechanism ⭐]]
