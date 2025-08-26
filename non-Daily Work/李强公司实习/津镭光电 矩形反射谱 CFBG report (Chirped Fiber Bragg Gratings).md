
CFBG(Chirped Fiber Bragg Gratings)是传统FBG(Fiber Bragg Gratings)的啁啾变体, 它的啁啾特性使得反射频谱显著展宽, 同时赋予了CFBG对栅区内各个位置温度与张力变化的响应能力. 
应市场需求, [上海津镭光电科技有限公司](http://genlaser.net/)(下称我们)实现了矩形反射谱CFBG, 其矩形反射谱涨落在1dB以下, 谱边缘涨落在3dB以下(实际实现中不超过1dB). 

下面, 我们将分 **反射谱计算理论**、**矩形反射谱优化思路**和**反射谱涨落来源分析**三个部分介绍矩形反射谱CFBG的理论、实现和下一步改进方向. 

# 一、反射谱计算理论

## 理论图像

![[Pasted image 20250826102104.png]] 
在传统FBG中, 根据Bragg干涉原理, 我们有反射波~光纤长度周期关系: 
$$
\begin{align}
2n_{\text{eff}} \times \Lambda = \lambda \tag{1}  
\end{align}
$$
其中, $\lambda$为反射波波长, $n_{\text{eff}}$为光纤纤芯有效折射率, 而$\Lambda$为光纤栅极空间周期(即间距). 
关系(1)表明, **反射波波长与FBG的空间周期对应**, 这构成了我们最基本的理论图像. 

我们进一步将这个图像推广到整个频域内, 根据**耦合模理论**我们有超弱均匀光栅的反射谱~FBG栅极空间分布关系: 
$$
\begin{align}
R(\lambda)  \overset{\lambda \to f}{=} R(f)\propto |\mathcal{F}\{\text{FBG}(x)\}|^{2} \tag{2}
\end{align}
$$
其中$R$为反射谱, $\mathcal{F}\{\}$为傅里叶变换, 而$\text{FBG(x)}$为FBG相对折射率变化的空间分布, 式中的模平方来自光波谱的振幅能量转换关系. 

根据(2)式, 我们得到: **CFBG频域的啁啾区原则上与反射谱对应, 扩大啁啾范围就是展宽反射谱, 增强特定啁啾值处加工能量就是增强对应反射谱处反射率**. 

## 具体建模

为进行具体计算, 我们将CFBG建模为一个一维折射率分布$\text{signal}(x)$, $\text{signal}(x)$表示CFBG在特定位置$x$处的相对折射率. 
我们在**脉冲飞秒激光**加工过程中使用**切趾**、**啁啾**两个工具控制CFBG的$\text{signal}(x)$输出. 
具体而言, **切趾**决定了$\text{signal}(x)$的包络$\text{env}(x)$, 而**啁啾**决定了$\text{signal}(x)$的空间频率调制$\text{mod}(x)$. 
我们用正弦函数模拟飞秒激光, 得到$\text{signal}(x)$对各个加工参数的依赖为: 
$$
\begin{align}
\text{signal}(x) = \text{env}(x) \times \sin \left[ (f_{0} + \text{mod(x)}) x + \varphi_{0} \right]\tag{3}
\end{align}
$$
其中$f_{0}$为脉冲激光中心触发频率, $\varphi_{0}$为初相位. 

**这里, 我们利用(3)式首先进行理论上的探索:**
利用傅里叶变换与卷积定理, 我们得到: 
$$
\begin{align}
\mathcal{F}[\text{signal}(x)] = \mathcal{F}[\text{env}(x) ] \text{conv} \mathcal{F} \{ \sin \left[ (f_{0} + \text{mod(x)}) x + \varphi_{0} \right]\}\tag{4}
\end{align}
$$
排除无关的相位影响, 利用(2)式, 立即得到
$$
\begin{align}
\sqrt{R(\lambda)} \propto|\mathcal{F}[\text{signal}(x)]| = |\mathcal{F}[\text{env}(x) ] \text{conv} \mathcal{F} \{ \sin \left[ (f_{0} + \text{mod(x)}) x + \varphi_{0} \right]\}|\tag{5}
\end{align}
$$
在这里, (5)式表明, 反射谱将正比于$\mathcal{F}[\text{env}(x)]$与$\mathcal{F}\{\sin \left[ (f_{0} + \text{mod(x)}) x + \varphi_{0} \right]\}$ 的卷积. 其中后者较为简单, 可**暂先视作形式为不同频率值上$\delta$函数的求和的输入特征**, 而前者$\mathcal{F}[\text{env}(x)]$代表了卷积的**卷积核**. 

因此, 反射谱$R(\lambda)$的形式将来源于**切趾**工艺决定的$\mathcal{F}[\text{env}(x)]$**卷积核**形式与**啁啾**工艺决定的$\mathcal{F}\{\sin \left[ (f_{0} + \text{mod(x)}) x + \varphi_{0} \right]\}$**频域输入特征**. 
从这个理论分析出发, 我们得以正式进入第二节对矩形反射谱优化思路的讨论. 

# 二、矩形反射谱优化思路

首先援引(5)式, 我们来依次分析各个工艺对最终反射谱的影响效果:
$$
\begin{align}
\sqrt{R(\lambda)} \propto|\mathcal{F}[\text{signal}(x)]| = |\mathcal{F}[\text{env}(x) ] \text{conv} \mathcal{F} \{ \sin \left[ (f_{0} + \text{mod(x)}) x + \varphi_{0} \right]\}|\tag{5}
\end{align}
$$

## 1. 切趾工艺决定的$\mathcal{F}[\text{env}(x)]$**卷积核**形式

我们的加工中, 切趾主要有**矩形功率切趾、倾斜切趾、高斯功率切趾、四次高斯功率切趾**等几种选项, 其中**倾斜切趾暂定作为等效高斯功率切趾理解**. 

1) 矩形功率切趾:
若加工采用矩形功率切趾, 则$\mathcal{F}[\text{rect}(x)] \propto \text{sinc}(f) = \frac{\sin(f)}{f}$. 
![[Pasted image 20250826113817.png|719]] 
如上图所示, $\text{sinc}$函数外侧有不少于两个明显的side peak, 这些side peak使卷积结果涨落明显加大, 在矩形谱区涨落1dB的限制下, 良率要求难以达到, 故不做选择. 

2) 高斯功率切趾(倾斜切趾的等效高斯功率切趾)
同样地, 我们有, $\mathcal{F}\left[ \exp\left( -\frac{1}{2}\left( \frac{x}{\sigma} \right)^{2} \right) \right] \propto \exp\left( -\frac{1}{2} K\left( \frac{f}{\left( \frac{1}{\sigma} \right)} \right)^{2} \right)$ 
![[Pasted image 20250826114934.png|722]] 
容易发现, 高斯功率切趾工艺下, 卷积核峰值突出, 边缘涨落不明显. 这样的性质有助于我们在矩形谱区内实现低于1dB的低涨落. 
同时, 我们可以得知该卷积核的频域展宽反比于其实空间展宽, 这在对矩形谱区边缘的涨落抑制可能有作用. 

3) 四次高斯功率切趾
四次高斯函数$\text{env} \propto \exp(-Kx^{4})$比对位的高斯函数展宽更大, 图像上从高斯功率切趾时实空间与频域卷积核的展宽反比关系出发思考, 四次高斯功率切趾对应于一个峰值更加尖锐, 展宽更小的卷积核. 这也可以用于对目标参数工艺的加工. 

## 2. 啁啾工艺决定的$\mathcal{F}\{ \sin \left[ (f_{0} + \text{mod(x)}) x + \varphi_{0} \right]\}$输入特征形式

我们知道$\mathcal{F}\{\sin(f_{0}x)\} \propto \delta(f-f_{0})$, 进一步地可以认为有: 
$$
\begin{align}
|\mathcal{F}\{ \sin \left[ (f_{0} + \text{mod(x)}) x + \varphi_{0} \right]\}| = \sum_{f_{\text{mod}}}   \delta(f-f_{\text{mod}}) \tag{6}
\end{align}
$$
在每个单一频率$\delta$函数处, 必然有: **该频率在空间上持续的距离越长, 则输入特征在该频率附近的$\delta$函数数目就越多.** 

下面, 我们固定卷积核为高斯函数, 研究不同啁啾工艺对反射谱的影响: 
1) 对于线性啁啾情况:
在线性啁啾情况下, 啁啾频域区内各频率空间长度相同, $\delta$函数间距相同, 反射谱主要由卷积核形式控制. 
由于反射谱中央处各个卷积核叠加最多, 故反射谱最大, 而边缘处卷积核叠加少, 反射谱值比中央处低得多. 
![[Pasted image 20250826122504.png|1122]]

2) 对于非线性啁啾情况:
![[Pasted image 20250826143739.png|369]]
这里以$\text{erf}(x)$函数为例演示非线性啁啾情况下的反射谱结果: 

由于$\text{erf}(x)$的函数特性, 其频域输入特征表现为**两端密集, 中间稀疏的$\delta$函数求和**, 将这样的$\delta$函数求和与卷积核做卷积, 即可得到一个相对更平坦的反射谱: 
![[Pasted image 20250826135650.png|1107]]
若提高**两端$\delta$密集程度**, 则反射谱两端上升, 变得更平坦, 若降低**两端$\delta$密集程度**, 则反射谱两端降低, 变得更尖锐. 
![[Pasted image 20250826123726.png|687]]![[Pasted image 20250826134928.png|547]]  

## 3. 切趾、啁啾、栅区长度间的balance

通过本节1. 2. 两小节的介绍, 我们明确**实现矩形反射谱需要一个以$\sigma$为实空间展宽的类高斯功率切趾与类$\text{erf}$函数啁啾间的配合**. 
它们二者(切趾、啁啾)与栅区长度间的关系为: 
- $\sigma$越大, 则切趾卷积核$\frac{1}{\sigma}$越小, 对应啁啾的两端密集程度越低. 
- $\sigma$越大, 则为容纳功率切趾函数所需的栅区长度越大. 

具体实现过程中, 为避免不同实空间位置间光纤纤芯的相对位置误差, 我们倾向于使用**小栅区长度、小$\sigma$功率切趾函数和大两端密集程度啁啾调制函数**生产CFBG. 

## 4. 最终优化实现

我们固定$\sigma = 3\text{mm}$高斯功率切趾函数, 使用`rbf_bspline`(B-spline-like Gaussian radial basis function)对啁啾调制$\mathrm{mod}(x)$进行优化, 得到了如下最优反射谱形: 
![[Pasted image 20250826155010.png]]

- 当前这个code的问题在于不够干爽, 太粘稠, 相互、前后耦合太多. 
- 应该试试bi-stage optmization: 先优化一个erf函数, 再再erf之上优化一个`rbf_bspline`(或者anything possible) 

# 三、反射谱涨落来源分析

在上机测试中, 我们发现矩形反射谱矩形边缘区涨落并不大, 一般不会超过1dB, 而矩形平台区涨落较大, 普遍在1dB上下, 占据我们实现市场要求中的主要矛盾. 下面我们将从模拟和上机测试两种情况下分析该涨落的来源: 
(以下分析均在与二、4. 中实现的$\sigma = 3\mathrm{mm}$高斯功率切趾最优化参数下进行)

## 1. 模拟

1) 模拟算法的客观能力. 
无需多言. 

2) `shift`: $\text{env}(x)$与$\text{mod}(x)$的中心对齐程度. 
涨落主要体现为峰值的整体偏移, `shift = 1e-2 * 7 # mm`时造成涨落达到1dB. 
 ![[Pasted image 20250826151727.png|900]] 
**然而, 上机测试中未见此特征涨落.** 
3) `power_noise`: 高斯功率切趾的输出能量涨落, 涨落频率都在10Hz以下, 更低或更高频率不能带来更大涨落. 
`power_noise = 1e-2 * 20`时, 涨落达到0.5dB. 
![[Pasted image 20250826152049.png|900]] 
4) `position_noise`: 栅极加工位置与理想位置偏移, 偏移频率都在10Hz以下, 更低或更高频率不能带来更大涨落. 
`position_noise = 1e-6 * 60 # mm`时, 涨落可能达到1dB以上, `position_noise = 1e-6 * 30 # mm`时, 涨落在0.5dB附近. 
![[Pasted image 20250826152559.png]] 

## 2. 上机测试

测试中未见`shift`引起的涨落, 涨落主要集中于平台区内, 涨落值普遍在1dB上下. 
![[e7c6f74f80bc14e24a6b6a2932fbfe8.png|997]] 

1) 上机测试与模拟参数不符合. ⭐
	轩哥讲没有这种可能性. 
2) 高斯功率切趾的功率涨落导致的相对折射率涨落
	1) 光纤纤芯位置偏移形成等效倾斜切趾, 导致相对折射率涨落
3) 栅极加工位置与理想位置偏移
	1) 位移台低频误差
	2) 其他
