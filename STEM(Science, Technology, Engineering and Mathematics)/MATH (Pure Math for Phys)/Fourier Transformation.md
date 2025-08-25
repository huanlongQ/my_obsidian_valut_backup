
-  [‎Gemini - 方波信号的傅里叶变换](https://g.co/gemini/share/5937d19b9be9)

# Inverse Fourier Transformation 

$$
\begin{align}
\mathcal{F}^{-1}[\cdot] = \frac{1}{2\pi} \int \mathrm{d}\omega\exp(j\omega t)\cdot
\end{align}
$$

**证明**: 

### 黎曼-勒贝格引理的证明 我在大一上学期高数(B)期中考试考场上搞定的压轴题 

黎曼-勒贝格引理的核心思想是：一个绝对可积函数的傅里叶变换，当频率趋近于无穷大时，其值趋近于零。

**数学表述：**
如果函数 $f(t)$ 满足 $\int_{-\infty}^{\infty} |f(t)| dt < \infty$，那么它的傅里叶变换 $F(\omega)$ 满足：
$$
\lim_{|\omega| \to \infty} F(\omega) = \lim_{|\omega| \to \infty} \int_{-\infty}^{\infty} f(t) e^{-j\omega t} dt = 0
$$

**证明过程：**

1.  **分步证明**
    我们将复指数函数 $e^{-j\omega t}$ 拆分成正弦和余弦部分，只要证明它们各自的积分都趋于零即可。我们以余弦部分为例进行证明，正弦部分同理。
    $$
\lim_{|\omega| \to \infty} \int_{-\infty}^{\infty} f(t)\cos(\omega t) dt = 0
$$
2.  **利用积分技巧**
    我们使用一个巧妙的积分技巧。将积分区间 $[-\infty, \infty]$ 看作是若干个 $\pi/\omega$ 长度的子区间拼接而成。我们可以利用三角函数的周期性 $\cos(x+\pi) = -\cos(x)$ 来抵消积分。
    对于任意的 $\omega \ne 0$，我们有：
    
$$
\int_{-\infty}^{\infty} f(t)\cos(\omega t) dt = \int_{-\infty}^{\infty} f\left(t+\frac{\pi}{\omega}\right)\cos\left(\omega t+\pi\right) dt = -\int_{-\infty}^{\infty} f\left(t+\frac{\pi}{\omega}\right)\cos(\omega t) dt
$$
    将两个等式相加，并除以2，我们得到：
    
$$
\int_{-\infty}^{\infty} f(t)\cos(\omega t) dt = \frac{1}{2} \int_{-\infty}^{\infty} \left[ f(t) - f\left(t+\frac{\pi}{\omega}\right) \right] \cos(\omega t) dt
$$
3.  **取绝对值和极限**
    对上式取绝对值，并利用三角不等式 $|\int g(t)dt| \le \int |g(t)|dt$：
    
$$
\left| \int_{-\infty}^{\infty} f(t)\cos(\omega t) dt \right| \leq \frac{1}{2} \int_{-\infty}^{\infty} \left| f(t) - f\left(t+\frac{\pi}{\omega}\right) \right| |\cos(\omega t)| dt
$$
    由于 $|\cos(\omega t)| \le 1$，我们得到：
    
$$
\leq \frac{1}{2} \int_{-\infty}^{\infty} \left| f(t) - f\left(t+\frac{\pi}{\omega}\right) \right| dt
$$
    当 $|\omega| \to \infty$ 时，$\pi/\omega \to 0$。因为 $f(t)$ 是绝对可积的，它在黎曼积分的意义上也是可积的。根据积分的性质，当函数的自变量变化量趋于零时，函数值的积分变化也趋于零。因此，当 $\frac{\pi}{\omega} \to 0$ 时，$\int_{-\infty}^{\infty} |f(t) - f(t+\frac{\pi}{\omega})| dt$ 趋近于零。

4.  **结论**
    由于积分的绝对值趋于零，所以积分本身也趋于零。黎曼-勒贝格引理得证。

---

### 不借助狄拉克函数推导傅里叶逆变换

要推导傅里叶逆变换公式，我们可以从傅里叶积分定理出发，这是一个更基础的结论，不依赖于狄拉克函数的概念。

**傅里叶积分定理：**
$$
f(t) = \frac{1}{2\pi} \int_{-\infty}^{\infty} \left( \int_{-\infty}^{\infty} f(\tau) e^{-j\omega\tau} d\tau \right) e^{j\omega t} d\omega
$$
**证明过程：**

1.  **设置待证表达式**
    我们将内层傅里叶变换 $F(\omega)$ 代入，并只考虑有限区间 $[-R, R]$ 的积分，然后取极限 $R \to \infty$。
    
$$
f(t) = \lim_{R \to \infty} \frac{1}{2\pi} \int_{-R}^{R} \left( \int_{-\infty}^{\infty} f(\tau) e^{-j\omega\tau} d\tau \right) e^{j\omega t} d\omega
$$
2. **交换积分顺序**
    在满足一定收敛条件下，我们可以交换积分顺序：
    
$$
f(t) = \lim_{R \to \infty} \frac{1}{2\pi} \int_{-\infty}^{\infty} f(\tau) \left( \int_{-R}^{R} e^{j\omega(t-\tau)} d\omega \right) d\tau
$$
3. **计算内层积分**
    内层积分是一个常规的定积分：
    
$$
\int_{-R}^{R} e^{j\omega(t-\tau)} d\omega = \frac{e^{jR(t-\tau)} - e^{-jR(t-\tau)}}{j(t-\tau)} = \frac{2\sin(R(t-\tau))}{t-\tau}
$$
4.  **代回外层积分**
    
$$
f(t) = \lim_{R \to \infty} \frac{1}{\pi} \int_{-\infty}^{\infty} f(\tau) \frac{\sin(R(t-\tau))}{t-\tau} d\tau
$$
5.  **利用狄利克雷积分性质**
    当 $R \to \infty$ 时，$\frac{\sin(R(t-\tau))}{t-\tau}$ 的行为类似于一个“冲击函数”。它在 $\tau=t$ 处有一个无限高的主峰，在其他地方迅速震荡并衰减。因此，这个积分只在 $\tau=t$ 附近有贡献。
    我们可以将 $f(\tau)$ 近似为 $f(t)$ 并移出积分号。
    
$$
f(t) = \lim_{R \to \infty} \frac{1}{\pi} f(t) \int_{-\infty}^{\infty} \frac{\sin(R(t-\tau))}{t-\tau} d\tau
$$
    通过变量替换 $x = R(t-\tau)$，这个积分可以简化为著名的**狄利克雷积分**：
    
$$
\int_{-\infty}^{\infty} \frac{\sin(Rx)}{x} dx = \pi \cdot \text{sgn}(R)
$$
    当 $R \to \infty$ 时，$\text{sgn}(R)=1$。

6.  **结论**
    将狄利克雷积分的结果代入，我们得到：
    
$$
f(t) = \frac{1}{\pi} f(t) \cdot (\pi) = f(t)
$$
    等式成立。这证明了傅里叶逆变换公式的正确性，并解释了 $1/(2\pi)$ 归一化因子的由来。

### $\delta$函数
$$
\begin{align}
2\pi\delta(t) = \int \exp(j\omega t)\mathrm{d\omega}
\end{align}
$$
# 卷积定理与Fourier Transformation

## 例: 周期性方波信号的Fourier Transformation

### 方波信号的傅里叶变换：基于卷积定理的推导

要理解周期性方波的傅里叶变换，最深刻的方法是将其看作两个基本信号的**卷积**。这个方法不仅能得到最终结果，还能直观地解释为什么方波的频谱是离散的，且只包含奇次谐波。

其核心思想是：**周期性方波 = 单个矩形脉冲 $*$ 周期性冲激串**。

根据**卷积定理**，时域上的卷积对应于频域上的乘积。因此，周期性方波的傅里叶变换，等于单个矩形脉冲和周期性冲激串各自傅里叶变换的乘积。
$$
F_{方波}(\omega) = F_{矩形脉冲}(\omega) \cdot F_{冲激串}(\omega)
$$
接下来，我们分步进行计算和推导。

---

### 第 1 步：分解信号并求傅里叶变换

我们把一个周期为 $T$、幅度为 $A$、脉冲宽度为 $\tau$ 的方波信号 $f(t)$ 分解为两个信号：

#### 1. 单个矩形脉冲 $p(t)$
$$
p(t) = A \cdot \text{rect}\left(\frac{t}{\tau}\right)
$$
其傅里叶变换 $P(\omega)$ 为：
$$
P(\omega) = \int_{-\infty}^{\infty} p(t)e^{-j\omega t} dt = \int_{-\tau/2}^{\tau/2} A e^{-j\omega t} dt = A\tau \cdot \frac{\sin(\omega\tau/2)}{\omega\tau/2}
$$
这个结果通常用 **sinc 函数** 表示为：
$$
P(\omega) = A\tau \cdot \text{sinc}\left(\frac{\omega\tau}{2\pi}\right)
$$
sinc 函数的形状是一个中央主瓣和两侧逐渐衰减的旁瓣，其零点位于 $\omega\tau/(2\pi) = n$ (n为非零整数) 处。这个 sinc 函数在频域中充当了最终频谱的**幅度包络线**。

#### 2. 周期性冲激串 $\delta_T(t)$ 的傅里叶级数 $\to$ 傅里叶变换方法
$$
\delta_T(t) = \sum_{n=-\infty}^{\infty} \delta(t-nT)
$$
要计算它的傅里叶变换，我们先将其写成傅里叶级数。由于 $\delta_T(t)$ 在一个周期内只在 $t=0$ 处有冲激，其傅里叶级数系数 $C_n$ 都为常数 $1/T$。
$$
C_n = \frac{1}{T} \int_{-T/2}^{T/2} \delta(t)e^{-j n\omega_0 t} dt = \frac{1}{T} e^{-j n\omega_0 (0)} = \frac{1}{T}
$$
根据傅里叶级数与傅里叶变换的关系 $F(\omega) = 2\pi \sum_{n=-\infty}^{\infty} C_n \delta(\omega - n\omega_0)$，我们得到周期性冲激串的傅里叶变换 $\Delta_T(\omega)$：
$$
\Delta_T(\omega) = 2\pi \sum_{n=-\infty}^{\infty} \left(\frac{1}{T}\right) \delta(\omega - n\omega_0) = \frac{2\pi}{T} \sum_{n=-\infty}^{\infty} \delta(\omega - n\omega_0)
$$
这个结果是一个在频域上以 $\omega_0 = 2\pi/T$ 为间隔的**离散冲激串**。

#### 2. 周期性冲激串 $\delta_T(t)$ 的直接傅里叶变换方法

首先计算傅里叶变换为: 
$$
\begin{align}
 & \lim_{ N \to \infty } \int_{-\frac{N}{2 } T}^{+ \frac{N}{2}T} \sum_{n=-\frac{N}{2}}^{+\frac{N}{2}} \delta(t-nT) \exp(-j\omega t)\mathrm{d}t \\
 & = \lim_{ N \to \infty }\sum_{n=-\frac{N}{2}}^{+\frac{N}{2}} \exp(-j\omega T \times n) 
\end{align}
$$
其次, 试着计算$\delta$函数的傅里叶变换: 
$$
\begin{align}
\mathcal{F}[\delta(t-t')] = \exp(-j\omega t') 
\end{align}
$$
那么就有
$$
\begin{align}
\mathcal{F}\left[ \sum_{n=-\frac{N}{2}}^{\frac{N}{2}} \delta (t-nT) \right] = \sum_{n=-\frac{N}{2}}^{\frac{N}{2}} \exp(-j\omega(nT)) = \sum_{n=-\frac{N}{2}}^{\frac{N}{2}}\exp(-j\omega T \times n) 
\end{align}
$$
相互对照不难得到: 

**发现难以得到, $\delta$函数与傅里叶变换相互嵌套, 因而无法独立导出冲激串的傅里叶变换系数.(胡言乱语ing)**   

---

### 第 2 步：应用卷积定理

现在我们将两个分量的傅里叶变换相乘：
$$
F(\omega) = P(\omega) \cdot \Delta_T(\omega)
$$
$$
F(\omega) = \left( A\tau \cdot \text{sinc}\left(\frac{\omega\tau}{2\pi}\right) \right) \cdot \left( \frac{2\pi}{T} \sum_{n=-\infty}^{\infty} \delta(\omega - n\omega_0) \right)
$$

这个乘法运算的含义是，sinc 函数包络在每个冲激点 $\omega = n\omega_0$ 上**“采样”**其值，从而决定了每个冲激的幅度。

### 最终结果分析

如果方波的**占空比为 50%**，那么脉冲宽度 $\tau = T/2$。
此时，sinc 函数的零点将出现在 $\omega = \frac{2\pi}{\tau} = \frac{4\pi}{T} = 2\omega_0$ 的整数倍上。也就是说，在 $\omega = \pm 2\omega_0, \pm 4\omega_0, \pm 6\omega_0, \dots$ 等频率上，sinc 函数的值为零。

由于这些频率点恰好对应于方波的**偶次谐波**，sinc 函数包络的零点刚好将这些谐波“过滤”掉了。

因此，最终的周期性方波频谱是一个**离散的频谱**，它由一系列在基频及其**所有奇次谐波**频率上的冲激组成，且它们的幅度随着频率的增加而减小，遵循 sinc 函数的包络曲线。
