
- [gemini chat on DQPT](https://g.co/gemini/share/7230f051bfe0) 

# 动态量子相变综合勘察：从基本概念到现代前沿

---

## 第一部分 动态临界性的基本原理

本部分旨在为动态量子相变（DQPT）领域奠定必要的理论基础。内容将从非平衡物理学的宏观背景出发，逐步深入到描述DQPT现象的具体数学形式。

### 1. 非平衡量子动力学导论

#### 1.1 平衡与非平衡相变的对比

物质相变是物理学中的核心概念，传统上在平衡态的框架下进行研究 1。平衡相变主要分为两类：

- **热力学相变**：这类相变在有限温度（T>0）下发生，由热涨落驱动。其标志是系统的热力学势（如自由能F）作为某个控制参数（如温度）的函数，在临界点出现非解析行为 2。
	
- **量子相变 (QPT)**：这类相变严格发生在绝对零度（T=0），由量子涨落驱动。当一个非热学参数（如磁场、压力）被调谐至量子临界点（QCP）时，系统的基态性质会发生突变 3。在任何有限温度下（
	
	T>0），尖锐的相变会被平滑为一个渐变区（crossover）2。

近年来，随着量子模拟器（如囚禁离子和超冷原子）技术的发展，研究孤立、相干演化的量子多体系统成为可能 2。在这些系统中，体系与环境的耦合非常微弱，使得系统能够在远离任何热平衡的状态下进行演化。动态量子相变（DQPT）正是为了描述和理解在这种非平衡条件下涌现的临界现象而提出的理论框架 2。

#### 1.2 量子淬火：诱导动力学的标准协议

为了在实验和理论上研究非平衡动力学，一种被称为“量子淬火”的标准协议被广泛采用 9。该协议的具体步骤如下：

1. 系统首先被制备在初始哈密顿量$H(\lambda_i)$的基态$|\psi_0\rangle$上。
	
2. 在t=0时刻，哈密顿量中的某个参数$\lambda被瞬时（或在有限时间内）从初始值\lambda_i改变为最终值\lambda_f$ 12。
	
3. 此后，系统在新的、时间无关的哈密顿量$H(\lambda_f)$下进行幺正演化，其含时波函数为$|\psi(t)\rangle = e^{-iH(\lambda_f)t} |\psi_0\rangle$ 13。

由于初始态$|\psi_0\rangle通常不是末态哈密顿量H(\lambda_f)$的本征态，这种淬火过程将系统带入一个高度的非平衡状态，从而引发非平庸的、丰富的量子动力学行为 8。

量子淬火协议不仅是一种技术手段，它从根本上定义了DQPT这一研究领域。与研究系统在特定温度或场强下静态性质的平衡相变不同，DQPT研究的是系统对其参数发生_变化_的_响应_。非平衡状态正是由这种变化所创造的。因此，DQPT的性质不仅内在地取决于初始和末态哈密顿量，也取决于淬火过程本身的特性，例如是瞬时淬火还是缓慢的斜坡式变化 12。这揭示了该领域的核心是研究量子系统的瞬态行为，其中时间本身扮演了临界现象展开的坐标轴。

### 2. 动态量子相变的数学形式

#### 2.1 洛施密特振幅与回波

描述DQPT的核心物理量是洛施密特振幅（Loschmidt amplitude）G(t)，它定义为含时演化态$|\psi(t)\rangle与初始态|\psi_0\rangle$的交叠：

$$
G(t) = \langle\psi_0|\psi(t)\rangle = \langle\psi_0|e^{-iHt}|\psi_0\rangle
$$

其中$H$是淬火后的哈密顿量 2。$G(t)$也被称为返回振幅或真空存活概率 2。

**洛施密特回波**（Loschmidt echo）$L(t)$是其振幅的模方：$L(t) = |G(t)|^2$ [9, 11, 18]。它代表了在$t$时刻，系统被发现仍处于其初始态的概率。

#### 2.2 作为动态自由能的速率函数

DQPT理论的基石在于洛施密特振幅$G(t)$与平衡态统计物理中的正则配分函数$Z(\beta) = \text{Tr}(e^{-\beta H})$之间存在一个深刻的形式对偶 [2, 9, 10]。通过将时间$t$解析延拓到复平面，即t→−iβ，洛施密特振幅可以被映射为一个具有复数参数z的边界配分函数Z(z) 11。

这个对偶关系启发了速率函数（rate function）$\lambda(t)$的定义，它被视为一种动态的自由能密度：

$$
\lambda(t) = -\frac{1}{N} \ln[L(t)] = -\frac{2}{N} \text{Re}[\ln G(t)]
$$

其中$N$是系统的自由度数目（如格点数）9。

基于此，**DQPT被正式定义为速率函数$\lambda(t)在某个临界时间t^*$处出现的非解析行为（如尖点或扭结）** 2。这种非解析性是DQPT的核心标志，通常被称为DPT-II型相变 7。

#### 2.3 费希尔零点与非解析性的起源

在热力学极限下（N→∞），速率函数$\lambda(t)的非解析性源于洛施密特振幅G(z)在复时间平面上的零点，这些零点被称为∗∗费希尔零点∗∗（Fisherzeros）[2,14,22]。在复平面上，这些零点可以汇聚成线或区域。当这些线或区域的边界与实时间轴在t = t^*$处相交时，它们会导致速率函数定义中的对数项发散，从而产生非解析行为 2。

对于有限尺寸的系统，速率函数通常是光滑的。然而，在某些经过精确调制的淬火参数下，洛施密特回波$L(t)$可以出现严格的零点，这会导致有限尺寸系统中的速率函数在临界时间点发散 19。

---

## 第二部分 理论图景与关键模型

本部分将探索DQPT研究中最为重要的理论模型，揭示不同的物理系统如何催生出丰富多样的动态临界现象。

### 3. DQPT的范式模型

#### 3.1 横场伊辛模型（TFIM）：原型范例

横场伊辛模型是Heyl、Polkovnikov和Kehrein在其开创性工作中引入DQPT概念时所使用的模型 23。该模型的重要性源于其可被精确求解（通过Jordan-Wigner变换映射为自由费米子），并且它本身展示了一个典型的平衡态QPT，这为理论比较提供了理想的平台 13。研究表明，当淬火过程跨越平衡态QPT的临界点时，速率函数会呈现周期性的非解析行为，这些行为与动态序参量（磁化强度）的零点直接相关 6。因此，TFIM成为了展示DQPT的标度、普适性和鲁棒性等基本特性的首选模型。

#### 3.2 Su-Schrieffer-Heeger（SSH）模型：对称性与拓扑的作用

SSH模型及其推广形式（如SSH-3、SSH-4）对于研究对称性、拓扑与DQPT三者之间的相互作用至关重要 9。在标准的SSH模型中，DQPT的出现与淬火过程跨越拓扑相变点紧密相连 9。

而广义的SSH模型则揭示了更为丰富的物理。例如，SSH-3模型虽然缺乏真正的手性对称性，但拥有一种点群对称性。研究发现，即使在整个动力学过程中能隙始终保持打开，跨越拓扑相变的淬火仍然能够诱发DQPT 9。这是一个关键的发现，它表明DQPT的发生可以与末态哈密顿量的能隙闭合解耦。相比之下，拥有手性对称性的SSH-4模型仅在从一个无能隙的初态出发并跨越临界点进行淬火时才会出现DQPT 9。这些结果有力地证明了系统的对称性对DQPT的发生条件具有深远的影响。

#### 3.3 其他关键模型

- **Kitaev链**：该模型被用于研究DQPT与拓扑之间的关系，特别是通过一个类似时间反演的操作，揭示了标准的拓扑DQPT与所谓的“意外”DQPT之间的内在联系 12。
	
- **Lipkin-Meshkov-Glick (LMG) 模型**：这是一个具有无限程相互作用的精确可解模型，与具有全连接特性的实验平台（如超导量子比特）高度相关。它被用来研究不同临界概念（DPT-I和DPT-II）的融合 25。
	
- **XY自旋链**：通过随机矩阵理论的研究，在该模型中发现了一种新颖的三阶DQPT，这与之前观测到的相变类型截然不同 16。
	
- **Potts模型**：利用复动力学和重整化群方法的研究表明，系统的相变由朱利亚集（Julia set）决定，并且边界条件可以改变相变的性质 11。

### 4. 动态临界性的分类

#### 4.1 DPT-I 与 DPT-II：两种临界性的故事

文献中逐渐形成了两种不同类型的动态相变（DPT）的分类 7：

- **DPT-I**：其特征是某个可观测量（动态序参量）的长时间平均值随着控制参数的变化而发生质的改变。这类似于朗道关于平衡相变的理论，系统最终会弛豫到一个有序或无序的稳态 7。
	
- **DPT-II**：这是指由洛施密特回波速率函数的非解析性所定义的标准DQPT。它在特定的临界时间发生，是一个纯粹的非平衡现象，与稳态序参量没有直接的对应关系 7。

这两种相变不仅是分类上的不同，在某些系统中甚至可能是相互排斥的。有理论提出，系统的能谱可以被一个激发态量子相变（ESQPT）分为两个不同的相区 7。在一个相区中，存在一个额外的守恒荷$\hat{C}$

。这个守恒荷的存在使得DPT−I的动态序参量可以非零，从而允许DPT−I的发生。然而，正是这个守恒荷$\hat{C}$的守恒性，_阻止_了导致DPT-II非解析性的主要机制（通常涉及特定能级的交叉）。这在某些系统中建立了一种根本性的不兼容性：允许DPT-I的条件可能禁止DPT-II，反之亦然。这一观点极具启发性，它表明“动态相变”这一术语涵盖了物理上截然不同的现象，而具体出现哪种现象，是由系统动力学的内在对称性和守恒律决定的。

#### 4.2 异常与意外DQPT

- **异常DQPT (Anomalous DQPTs)**：这类DQPT指的是在_同一个_平衡相内部进行淬火（即未跨越QCP）时出现的速率函数非解析性 7。它们的存在表明，基态性质的改变并非DQPT发生的必要条件。
	
- **意外DQPT (Accidental DQPTs)**：这类DQPT仅在哈密顿量被精确微调时才会出现，不受拓扑或对称性的保护。然而，研究揭示了一个令人惊讶的联系：一个标准的、受拓扑保护的DQPT，可以通过一个类似时间反演的操作，在另一个参照系中被形式上映射为一个意外DQPT 12。这暗示了不同类型的DQPT之间可能存在更深层次的结构关联。

---

## 第三部分 拓扑与动力学的交汇

本部分将聚焦于该领域最具影响力的发展方向之一：非平衡动力学与物质拓扑性质之间的深刻联系。

### 5. 拓扑动态量子相变 (TDQPTs)

#### 5.1 连接动力学与平衡拓扑

一类非常稳固的DQPT，通常被称为拓扑动态量子相变（TDQPT），在淬火过程连接了两个分属不同平衡拓扑相的哈密顿量时出现 9。这些平衡拓扑相由整数值的拓扑不变量来表征，例如一维系统（如SSH模型）中的

**卷绕数**（winding number）或二维系统中的**陈数**（Chern number）。

一个关键的发现是，在许多模型中，跨越一个拓扑QPT（即改变拓扑不变量）的淬火是诱发TDQPT的充分条件 2。对于二维系统，这个条件更为精细，通常要求陈数的

_绝对值_发生改变。

#### 5.2 鲁棒性与保护

与意外DQPT不同，TDQPT对于那些保持了保护拓扑相的基本对称性的微扰是鲁棒的 2。这与平衡态下拓扑边缘态的鲁棒性非常相似。

### 6. 动态拓扑序参量 (DTOP)

#### 6.1 定义一个动态序

为了表征被TDQPT分开的“动态相”，一个被称为**动态拓扑序参量**（Dynamical Topological Order Parameter, DTOP）的概念被引入 10。DTOP通常被定义为与含时演化态相关的

**潘查拉特南几何相位**（Pancharatnam geometric phase, PGP）在动量空间中的卷绕数 9。

#### 6.2 量子化跳变与涡旋动力学

DTOP是一个量子化的整数。其定义性特征是：在一个动态相内部，它保持为一个恒定的整数；而恰好在TDQPT的临界时间点，它的值会发生一个整数跳变（例如，±1）27。

这种跳变与波函数在动量空间中的行为直接相关。在临界时间t∗，波函数在某个特定的临界动量kc​处与初始态正交。这导致了PGP在kc​处出现一个$\pi$的相位滑移，进而引起其卷绕数（即DTOP）的跳变。在二维系统中，这些临界点表现为在布里渊区内波函数相位剖面图中**涡旋-反涡旋对**的产生、移动和湮灭 29。这些涡旋的数量本身也可以作为一个DTOP。

拓扑概念的引入，将DQPT的研究从对速率函数上“扭结”或“尖点”的定性观察，提升到了一个基于稳固的、整数值序参量的定量科学。DTOP提供了一个明确无误的信号：从$\nu=0到\nu=1$的跳变是一个离散的、清晰的事件 27。这不仅将非解析性这一抽象概念与一个具体的物理图像——几何相位的卷绕和动量空间中拓扑缺陷（涡旋）的产生——联系起来，还提供了一个强大的分类框架。它解释了为何某些DQPT是鲁棒的，并建立了非平衡动力学与系统基态性质之间的直接桥梁，使得整个理论更加严谨且易于实验验证。

---

## 第四部分 实验实现与探测

本部分将考察DQPT的实验研究现状，展示量子模拟技术的进步如何使DQPT从一个理论概念转变为一个可被直接观测和操控的物理现象。

### 7. 作为DQPT窗口的量子模拟器

多种先进的实验平台已被用于研究DQPT，每种平台都具有独特的优势：

- **囚禁离子**：提供高保真度的量子操控和长相干时间。该平台被用于模拟长程相互作用的TFIM，并首次直接观测到了速率函数的非解析行为 30。
	
- **光晶格中的超冷原子**：在构建不同的晶格几何和哈密顿量（如Hubbard、Haldane模型）方面具有高度的灵活性。该平台对于观测DQPT的拓扑性质，如动量空间中涡旋的出现，至关重要 4。
	
- **超导量子比特**：在某些架构中具有可扩展性和全连接能力。该平台被用于在LMG模型中探测DPT，以及通过将动量模式映射到单个量子比特来模拟TFIM 25。
	
- **光子量子行走**：非常适合研究单粒子动力学和拓扑现象。该平台已被用于模拟弗洛凯（Floquet）拓扑相之间的淬火，并首次探索了混合态和非幺正系统中的DQPT 35。

### 8. 关键实验观测

#### 关键实验进展概述

|平台|模拟模型|淬火协议|测量的DQPT标志|关键贡献与参考文献|
|---|---|---|---|---|
|**囚禁离子**|横场伊辛模型 (TFIM)|跨越平衡态QCP的淬火|速率函数的非解析性|首次直接观测到速率函数的非解析尖点 31|
|**超冷费米原子**|Haldane模型|拓扑相之间的淬火|动量空间中的涡旋|首次观测到作为DQPT标志的动态涡旋 29|
|**超导量子比特**|Lipkin-Meshkov-Glick (LMG) 模型|跨越动态临界点的淬火|序参量零点；洛施密特回波|探测DPT-I与DPT-II的融合；验证临界现象 25|
|**光子量子行走**|弗洛凯拓扑模型|弗洛凯拓扑相之间的淬火|DTOP的跳变|首次测量DTOP；首次研究混合态与非幺正DQPT 37|

#### 速率函数非解析性的直接观测

囚禁离子实验是该领域的里程碑。通过对多达10个离子的系统进行高精度操控，实验人员直接测量了洛施密特回波，并由此构建了速率函数，清晰地观测到了理论预测的在临界时间出现的非解析尖点 30。

#### 动态拓扑序参量的测量

利用超冷原子和光子量子行走平台，实验上成功测量了潘查拉特南几何相位，并提取出了DTOP。观测结果显示，DTOP呈现量子化的整数值，并在临界时间点发生突变，这有力地证实了相变的拓扑性质 27。

#### 新奇体系中的DQPT探测

实验探索已超越了理想化的基态淬火。在旋量玻色-爱因斯坦凝聚体中，科学家们观测到了与激发态QPT相对应的DQPT，为探测高能物理开辟了新途径 39。此外，光子平台独特的灵活性使其能够研究初始混合态以及在受控耗散（非幺正演化）下的DQPT，从而检验了该现象在更真实条件下的鲁棒性 37。

---

## 第五部分 现代前沿与更广泛的影响

本部分将探讨该领域的前沿问题，包括挑战、开放性问题以及新兴应用，这些将共同塑造DQPT研究的未来。

### 9. 复杂与开放系统中的DQPT

#### 9.1 超越理想化模型

- **有限温度与混合态**：虽然QPT是严格的T=0现象，但DQPT可以在有限温度下持续存在，尽管其行为会受到修正 9。在低温下，混合态DQPT通常与其纯态对应物相似；但在高温下，可能会出现新的特征，如多个临界时间，或者相变本身完全消失 9。
	
- **强关联与高维系统**：从精确可解的一维模型推广到更高维度和强关联系统是一个重大挑战。诸如累积量方法 41 和张量网络 20 等数值技术正在被开发用于研究二维和强关联系统中的DQPT，但这在计算上仍然是一个难题 41。
	
- **耗散与开放系统**：环境引起的耗散效应是一个至关重要的前沿。研究表明，DQPT可以由环境本身诱导 43，或被环境所改变。光子学实验已经通过引入受控损耗开始探索这一领域 37。

#### 9.2 与非遍历动力学的交织：多体局域化 (MBL)

多体局域化（MBL）系统是指由于强无序而无法达到热平衡的相互作用系统，表现出非遍历的动力学特性 44。DQPT与MBL之间的关系是一个活跃且充满挑战的研究领域 47。

在准周期系统（如Aubry-André模型）中的研究表明，跨越局域化-离域化相变点的淬火可以诱发DQPT 48。一个引人注目的联系被发现：当从一个低纠缠的局域化（MBL）相淬火到一个高纠缠的离域化（遍历）相时，纠缠增长的速率与DQPT的出现密切相关。更快的纠缠增长导致非解析性更快地显现 48。此外，作为MBL关键要素的多体相互作用，会抑制DQPT的信号，随着相互作用强度的增加，速率函数的非解析性会逐渐消失 48。

这些发现表明，DQPT的行为在遍历系统和非遍历（MBL）系统中存在根本差异。在遍历系统中，淬火导致热化和信息在整个系统中扩散。而在MBL系统中，由于存在局域守恒量（l-bits），系统会保留对初始态的记忆 46。纠缠增长率与DQPT出现时间之间的关联，直接在两个概念之间架起了一座桥梁。快速的纠缠增长是混沌、遍历动力学的标志，而缓慢的（对数）增长则是MBL的特征。因此，DQPT不仅是在特定动力学区域（遍历或MBL）内发生的现象，它还可以作为探测这些区域之间

_相变_的有力工具。DQPT的存在、缺失或其特征可用于诊断潜在多体动力学的性质，使其成为研究量子热化问题的重要工具。

### 10. 应用与未来展望

#### 10.1 在量子技术中的应用

随着理论的成熟，DQPT的研究正从基础探索转向实际应用，展现出在量子技术领域的潜力。

- **量子计量学与增强传感**：与DQPT相关的临界性可以被用于实现高精度测量。作为衡量测量精度的上限，量子费希尔信息（QFI）在DQPT附近可能发散或呈现尖锐特征。这表明，将传感器工作在动态临界点附近，有望实现超越标准量子极限的测量精度（即海森堡标度）49。通过外部场调控的可控DQPT，更可用于设计优化的传感协议 52。
	
- **量子计算**：不同的动态相（如热化相与MBL相）具有不同的计算能力。研究表明，热化相天然适用于一种名为量子水库计算（QRC）的机器学习范式，其性能在向MBL相的动态转变点附近达到峰值 53。

#### 10.2 开放性问题与未来方向

DQPT领域虽然取得了显著进展，但仍面临诸多挑战和开放性问题，这些问题将指引未来的研究方向。

- **普适性与标度律**：尽管已经发现了一些标度律，但一个类似于平衡相变的DQPT普适性分类方案仍有待建立。是否存在具有非平庸临界指数的奇异DQPT，也是一个悬而未决的问题。
	
- **高维与强关联**：精确预测相互作用的二维和三维系统中的DQPT，在理论和计算上都是一个巨大的挑战 41。
	
- **普适的序参量理论**：是否存在一种普适的方法来为任何DQPT（特别是非拓扑或异常的DQPT）定义动态序参量？28。
	
- **与热化的联系**：在最终会热化的系统中，DQPT的瞬态非解析性如何与最终稳态的性质相关联，是一个关键的开放问题。
	
- **实验挑战**：由于洛施密特回波随系统尺寸呈指数衰减，在更大、更复杂的系统中，尤其是在存在噪声和退相干的情况下，测量DQPT信号仍然极具挑战性 2。

该领域的研究轨迹清晰地展示了其从初生到成熟的演化过程。早期（约2013-2017年）的研究主要集中于定义概念 2、在范式模型中建立理论 13 并实现首次实验观测 29，核心问题是“DQPT是什么？”。中期阶段，拓扑等强大概念的引入带来了更结构化的理解 28，问题转变为“如何对DQPT进行分类？”。当前，研究的前沿则更多地关注“DQPT在真实世界的复杂性（如MBL、耗散）面前是否稳固？”以及“我们能否利用DQPT现象做一些有用的事？”，如在量子计量和计算中的应用 50。这种从基础到应用的演进，标志着一个研究领域的成熟。其未来不仅在于发现新型的DQPT，更在于理解它们在广阔的非平衡物理学图景中的角色，并将其独特性质转化为推动技术创新的动力。

### 结论

动态量子相变（DQPT）作为非平衡量子多体物理学的一个核心概念，成功地将相变的思想从平衡态推广到了相干的实时演化领域。通过洛施密特回波及其速率函数的形式化定义，DQPT被确立为时间驱动的临界现象，其标志是物理量在临界时间出现的非解析行为。

该领域的发展深受拓扑学和对称性思想的滋养。特别是拓扑动态量子相变（TDQPT）的发现，以及动态拓扑序参量（DTOP）的引入，为一类重要的DQPT提供了基于量子化不变量的严谨分类和深刻物理图像，极大地推动了理论的深化。

在实验方面，囚禁离子、超冷原子、超导量子比特和光子量子行走等量子模拟平台的飞速发展，使得DQPT从理论构想走向了实验验证。科学家们不仅直接观测到了速率函数的非解析性，还测量了DTOP的量子化跳变，甚至开始在混合态、非幺正演化、激发态等更复杂的场景中探索DQPT。

当前，DQPT的研究正迈向新的前沿。它与多体局域化等非遍历动力学的关系，以及在耗散、强关联和高维系统中的行为，是理论和计算面临的主要挑战。与此同时，DQPT在量子计量学和量子计算等领域的潜在应用也开始显现，预示着该领域正从基础科学探索向应用技术开发迈进。未来，对DQPT更深入的理解，有望为我们揭示更多关于物质在远离平衡时所遵循的普适规律。

[

![](https://t3.gstatic.com/faviconV2?url=https://quantum-journal.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

quantum-journal.org

Dynamical quantum phase transitions from random matrix theory

在新窗口中打开](https://quantum-journal.org/papers/q-2024-02-29-1271/pdf/)[

![](https://t3.gstatic.com/faviconV2?url=https://www.iopb.res.in/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

iopb.res.in

Complex dynamics approach to dynamical quantum phase transitions: The Potts model

在新窗口中打开](https://www.iopb.res.in/~somen/SMB_papers/DQPT-Potts2024.pdf)[

![](https://t2.gstatic.com/faviconV2?url=https://en.wikipedia.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

en.wikipedia.org

State of matter - Wikipedia

在新窗口中打开](https://en.wikipedia.org/wiki/State_of_matter)[

![](https://t2.gstatic.com/faviconV2?url=https://pmc.ncbi.nlm.nih.gov/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

pmc.ncbi.nlm.nih.gov

Anomalous correlation-induced dynamical phase transitions - PMC - PubMed Central

在新窗口中打开](https://pmc.ncbi.nlm.nih.gov/articles/PMC10257700/)[

![](https://t0.gstatic.com/faviconV2?url=https://physics.stackexchange.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

physics.stackexchange.com

Is Bose-Einstein condensation a quantum phase transition? - Physics Stack Exchange

在新窗口中打开](https://physics.stackexchange.com/questions/512457/is-bose-einstein-condensation-a-quantum-phase-transition)[

![](https://t0.gstatic.com/faviconV2?url=https://www.researchgate.net/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

researchgate.net

Dynamical quantum phase transitions and the Loschmidt echo: A transfer matrix approach

在新窗口中打开](https://www.researchgate.net/publication/259312961_Dynamical_quantum_phase_transitions_and_the_Loschmidt_echo_A_transfer_matrix_approach)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

Exploring dynamical quantum phase transition from pure states to mixed states through extended Su-Schrieffer-Heeger models - arXiv

在新窗口中打开](https://arxiv.org/html/2501.06794v3)[

![](https://t0.gstatic.com/faviconV2?url=https://www.researchgate.net/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

researchgate.net

Dynamical Quantum Phase Transitions in Systems with Broken-Symmetry Phases - ResearchGate

在新窗口中打开](https://www.researchgate.net/publication/268881421_Dynamical_Quantum_Phase_Transitions_in_Systems_with_Broken-Symmetry_Phases)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

arXiv:2205.03443v2 [cond-mat.stat-mech] 16 Feb 2023

在新窗口中打开](https://arxiv.org/pdf/2205.03443)[

![](https://t0.gstatic.com/faviconV2?url=https://www.semanticscholar.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

semanticscholar.org

[PDF] Observation of a dynamical topological phase transition

在新窗口中打开](https://www.semanticscholar.org/paper/826e27d048d11c762fae48af137e61f086cf58ac)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Dynamical singularity of the rate function for quench dynamics in finite-size quantum systems | Phys. Rev. B - Physical Review Link Manager

在新窗口中打开](https://link.aps.org/doi/10.1103/PhysRevB.107.134302)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Dynamical phase transitions in quantum spin models with antiferromagnetic long-range interactions | Phys. Rev. B - Physical Review Link Manager

在新窗口中打开](https://link.aps.org/doi/10.1103/PhysRevB.104.115133)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

Exploring dynamical quantum phase transition from pure states to mixed states through generalized Su-Schrieffer-Heeger models - arXiv

在新窗口中打开](https://arxiv.org/html/2501.06794v1)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

[2202.05519] Dynamical Quantum Phase Transitions in Strongly Correlated Two-Dimensional Spin Lattices Following a Quench - arXiv

在新窗口中打开](https://arxiv.org/abs/2202.05519)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Anatomy of dynamical quantum phase transitions | Phys. Rev …

在新窗口中打开](https://link.aps.org/doi/10.1103/PhysRevResearch.5.033090)[

![](https://t3.gstatic.com/faviconV2?url=https://quantum-journal.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

quantum-journal.org

Dynamical quantum phase transitions from random matrix theory …

在新窗口中打开](https://quantum-journal.org/papers/q-2024-02-29-1271/)[

![](https://t0.gstatic.com/faviconV2?url=https://www.researchgate.net/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

researchgate.net

Experimental Observation of Equilibrium and Dynamical Quantum Phase Transitions via Out-of-Time-Ordered Correlators | Request PDF - ResearchGate

在新窗口中打开](https://www.researchgate.net/publication/338228294_Experimental_Observation_of_Equilibrium_and_Dynamical_Quantum_Phase_Transitions_via_Out-of-Time-Ordered_Correlators)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

[1612.06902] Direct observation of dynamical quantum phase transitions in an interacting many-body system - arXiv

在新窗口中打开](https://arxiv.org/abs/1612.06902)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Observation of Dynamical Quantum Phase Transitions with Correspondence in an Excited State Phase Diagram | Phys. Rev. Lett. - Physical Review Link Manager

在新窗口中打开](https://link.aps.org/doi/10.1103/PhysRevLett.124.043001)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Direct Observation of Dynamical Quantum Phase Transitions in an Interacting Many-Body System | Phys. Rev. Lett. - Physical Review Link Manager

在新窗口中打开](https://link.aps.org/doi/10.1103/PhysRevLett.119.080501)[

![](https://t3.gstatic.com/faviconV2?url=https://www.numberanalytics.com/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

numberanalytics.com

Quantum Phase Transitions in Ultracold Atoms - Number Analytics

在新窗口中打开](https://www.numberanalytics.com/blog/quantum-phase-transitions-ultracold-atomic-physics)[

![](https://t0.gstatic.com/faviconV2?url=https://www.researchgate.net/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

researchgate.net

(PDF) Experimental realization of the topological Haldane model with ultracold fermions

在新窗口中打开](https://www.researchgate.net/publication/268228000_Experimental_realization_of_the_topological_Haldane_model_with_ultracold_fermions)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

arXiv:2305.08400v4 [quant-ph] 11 Jan 2024

在新窗口中打开](https://arxiv.org/pdf/2305.08400)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Experimentally detecting dynamical quantum phase transitions in a slowly quenched Ising-chain model | Phys. Rev. A

在新窗口中打开](https://link.aps.org/doi/10.1103/PhysRevA.102.042222)[

![](https://t0.gstatic.com/faviconV2?url=https://pubmed.ncbi.nlm.nih.gov/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

pubmed.ncbi.nlm.nih.gov

Observation of Dynamical Quantum Phase Transitions with Correspondence in an Excited State Phase Diagram - PubMed

在新窗口中打开](https://pubmed.ncbi.nlm.nih.gov/32058743/)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

Probing the dynamical phase transition with a superconducting quantum simulator - arXiv

在新窗口中打开](https://arxiv.org/abs/1912.05150)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

[2312.05697] Environment induced dynamical quantum phase transitions in two-qubit Rabi model - arXiv

在新窗口中打开](https://arxiv.org/abs/2312.05697)[

![](https://t3.gstatic.com/faviconV2?url=https://dash.harvard.edu/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

dash.harvard.edu

Photonic Quantum Simulators - Harvard DASH

在新窗口中打开](https://dash.harvard.edu/bitstreams/7312037d-0f97-6bd4-e053-0100007fdf3b/download)[

![](https://t0.gstatic.com/faviconV2?url=https://www.researchgate.net/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

researchgate.net

Simulating Dynamic Quantum Phase Transitions in Photonic

在新窗口中打开](https://www.researchgate.net/publication/330428300_Simulating_Dynamic_Quantum_Phase_Transitions_in_Photonic_Quantum_Walks)[

![](https://t0.gstatic.com/faviconV2?url=https://www.researchgate.net/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

researchgate.net

Simulating dynamic quantum phase transitions in photonic quantum walks - ResearchGate

在新窗口中打开](https://www.researchgate.net/publication/326057116_Simulating_dynamic_quantum_phase_transitions_in_photonic_quantum_walks)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

[2403.07111] Many-Body Localization in the Age of Classical Computing - arXiv

在新窗口中打开](https://arxiv.org/abs/2403.07111)[

![](https://t2.gstatic.com/faviconV2?url=https://pmc.ncbi.nlm.nih.gov/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

pmc.ncbi.nlm.nih.gov

Measuring a dynamical topological order parameter in quantum walks - PMC

在新窗口中打开](https://pmc.ncbi.nlm.nih.gov/articles/PMC6971032/)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Colloquium: Many-body localization, thermalization, and entanglement | Rev. Mod. Phys.

在新窗口中打开](https://link.aps.org/doi/10.1103/RevModPhys.91.021001)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Dynamical topological order parameters far from equilibrium | Phys. Rev. B

在新窗口中打开](https://link.aps.org/doi/10.1103/PhysRevB.93.085416)[

![](https://t1.gstatic.com/faviconV2?url=https://courses.physics.ucsd.edu/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

courses.physics.ucsd.edu

Quantum phase transitions - Physics Courses

在新窗口中打开](https://courses.physics.ucsd.edu/2020/Winter/physics211b/GOODIES/T_Vojta_RPP.pdf)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Dynamical quantum phase transitions and quantum thermodynamics: An approach through dynamical transformations | Phys. Rev. E - Physical Review Link Manager

在新窗口中打开](https://link.aps.org/doi/10.1103/PhysRevE.111.014130)[

![](https://t0.gstatic.com/faviconV2?url=https://www.researchgate.net/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

researchgate.net

Dynamical quantum phase transitions (Review Article) - ResearchGate

在新窗口中打开](https://www.researchgate.net/publication/311524704_Dynamical_quantum_phase_transitions_Review_Article)[

![](https://t0.gstatic.com/faviconV2?url=https://www.researchgate.net/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

researchgate.net

Dynamical quantum phase transitions: A review - ResearchGate

在新窗口中打开](https://www.researchgate.net/publication/320014196_Dynamical_quantum_phase_transitions_A_review)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Determination of Dynamical Quantum Phase Transitions in Strongly Correlated Many-Body Systems Using Loschmidt Cumulants | Phys. Rev. X - Physical Review Link Manager

在新窗口中打开](https://link.aps.org/doi/10.1103/PhysRevX.11.041018)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Simulating Dynamic Quantum Phase Transitions in Photonic …

在新窗口中打开](https://link.aps.org/doi/10.1103/PhysRevLett.122.020501)[

![](https://t3.gstatic.com/faviconV2?url=https://d-nb.info/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

d-nb.info

Direct Observation of Dynamical Quantum Phase Transitions in an …

在新窗口中打开](https://d-nb.info/1259733262/34)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

arxiv.org

在新窗口中打开](https://arxiv.org/abs/1806.09269)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

Observation of a dynamical topological phase transition - arXiv

在新窗口中打开](https://arxiv.org/abs/1608.05616)[

![](https://t2.gstatic.com/faviconV2?url=https://pmc.ncbi.nlm.nih.gov/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

pmc.ncbi.nlm.nih.gov

Probing dynamical phase transitions with a superconducting …

在新窗口中打开](https://pmc.ncbi.nlm.nih.gov/articles/PMC7299620/)[

![](https://t0.gstatic.com/faviconV2?url=https://www.researchgate.net/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

researchgate.net

Dynamical quantum phase transitions in many-body localized systems | Request PDF

在新窗口中打开](https://www.researchgate.net/publication/331644708_Dynamical_quantum_phase_transitions_in_many-body_localized_systems)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

[1603.06618] Nonequilibrium quantum dynamics and transport: from integrability to many-body localization - arXiv

在新窗口中打开](https://arxiv.org/abs/1603.06618)[

![](https://t3.gstatic.com/faviconV2?url=https://d-nb.info/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

d-nb.info

Dynamical quantum phase transitions: a review

在新窗口中打开](https://d-nb.info/1259732789/34)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

Dynamical quantum phase transitions in a spinor Bose-Einstein condensate and criticality enhanced quantum sensing - arXiv

在新窗口中打开](https://arxiv.org/html/2209.11415v2)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

Dynamical quantum phase transition with divergent multipartite entanglement - arXiv

在新窗口中打开](https://arxiv.org/html/2506.13898v1)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Dynamical phase transitions as a resource for quantum enhanced metrology | Phys. Rev. A - Physical Review Link Manager

在新窗口中打开](https://link.aps.org/doi/10.1103/PhysRevA.93.022103)[

![](https://t0.gstatic.com/faviconV2?url=https://www.researchgate.net/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

researchgate.net

(PDF) Dynamical quantum phase transition in diamond: applications in quantum metrology

在新窗口中打开](https://www.researchgate.net/publication/358509752_Dynamical_quantum_phase_transition_in_diamond_applications_in_quantum_metrology)[

![](https://t1.gstatic.com/faviconV2?url=https://link.aps.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

link.aps.org

Dynamical Phase Transitions in Quantum Reservoir Computing …

在新窗口中打开](https://link.aps.org/doi/10.1103/PhysRevLett.127.100502)[

![](https://t1.gstatic.com/faviconV2?url=https://arxiv.org/&client=BARD&type=FAVICON&size=256&fallback_opts=TYPE,SIZE,URL)

arxiv.org

Many-body dynamical phase transition in quasi-periodic potential

](https://arxiv.org/pdf/2103.09065)
