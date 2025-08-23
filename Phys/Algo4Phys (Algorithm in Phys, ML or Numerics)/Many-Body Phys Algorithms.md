* [计算凝聚态物理发展大观](https://www.zhihu.com/question/38845619/answer/1838677936)
# 1. DMRG on MPS
[[Tensor Network Representation (General)]] My notes on DMRG and MPS. 
## 1.1 DMRG talk with Grok
I want a DMRG understanding and a low energy state calculation scheme.

要查看键盘快捷键，按下问号

查看键盘快捷键


what dmrg do phys


15 网页


It seems like you might be asking, "What does DMRG do in physics?" I'll assume that’s the intent and provide an answer based on that.

In physics, the Density Matrix Renormalization Group (DMRG) is a powerful numerical method used to study quantum many-body systems, particularly those that are strongly correlated and difficult to solve with traditional approaches. Here's what DMRG does:

DMRG is primarily used to find the low-energy states, like the ground state, of quantum systems, especially in one-dimensional (1D) setups. It tackles the challenge of the exponentially large Hilbert space—the mathematical space describing all possible states of a quantum system—by cleverly reducing it to a manageable size. This is crucial because, in many-body physics, the number of possible states grows so fast with system size that exact calculations become impossible even for relatively small systems.

The method works by representing the quantum state as a matrix product state (MPS), a type of tensor network, and then iteratively optimizing it. It focuses on keeping only the most relevant states—those with the largest contributions to the system's properties—based on the eigenvalues of the reduced density matrix. This "renormalization" process discards less important states, making the computation efficient while still capturing the essential physics, like energy levels or correlation functions.

In practice, DMRG shines for 1D systems with short-range interactions, such as spin chains (e.g., the Heisenberg or Ising models) or fermionic systems (e.g., the Hubbard model). It’s been a game-changer for understanding phenomena like quantum phase transitions, magnetism, or superconductivity in these systems. It’s also been extended to other areas, like quantum chemistry for strongly correlated molecules, 2D systems (with some limitations), and even time-dependent problems.

So, in short, DMRG helps physicists simulate and understand the behavior of complex quantum systems by efficiently approximating their low-energy properties when exact solutions are out of reach. If you meant something different by "dmrg do phys," feel free to clarify!


any other algo to do that


Yes, there are several other algorithms and methods in physics that tackle similar problems to DMRG—namely, simulating quantum many-body systems and finding their low-energy states. Here are some key alternatives, each with its own strengths and trade-offs:

Quantum Monte Carlo (QMC)  

What it does: QMC uses statistical sampling to compute properties of quantum systems, like ground-state energies or correlation functions. It’s based on mapping quantum problems to classical ones via path integrals.



Pros: Works well for higher dimensions (2D, 3D) and can handle bosonic systems or unfrustrated spin systems effectively.



Cons: Suffers from the "sign problem" for fermionic systems or frustrated models, where negative probabilities make it inefficient or intractable.



Use case: Great for systems where DMRG struggles, like 3D lattices, if the sign problem isn’t an issue.


Tensor Network Methods (beyond DMRG)  

Matrix Product States (MPS): DMRG itself uses MPS, but MPS can be applied more broadly with different optimization techniques (e.g., variational methods).



Projected Entangled Pair States (PEPS): An extension of MPS to 2D systems. PEPS represents states as a 2D tensor network.

Pros: Better suited for 2D systems than DMRG.



Cons: Much more computationally expensive, and convergence can be tricky.


Multiscale Entanglement Renormalization Ansatz (MERA): A hierarchical tensor network for critical systems.

Pros: Excels at capturing critical phenomena and long-range entanglement.



Cons: Complex to implement and computationally intensive.


Use case: These are go-tos for 2D or critical systems where DMRG’s 1D focus falls short.


Exact Diagonalization (ED)  

What it does: Solves the full Hamiltonian matrix directly to get exact eigenvalues and eigenstates.



Pros: Gives exact results, no approximations.



Cons: Limited to very small systems (e.g., ~20-30 sites) due to exponential growth of the Hilbert space.



Use case: Useful for benchmarking other methods on small systems.


Variational Monte Carlo (VMC)  

What it does: Uses a trial wavefunction (often parameterized by neural networks, like restricted Boltzmann machines) and optimizes it variationally.



Pros: Flexible and can handle higher dimensions; pairs well with machine learning advances.



Cons: Accuracy depends heavily on the quality of the trial wavefunction.



Use case: Good for exploring new systems where you can guess a decent starting state.


Time-Evolving Block Decimation (TEBD)  

What it does: Evolves quantum states in time using MPS, similar to DMRG’s framework.



Pros: Excellent for time-dependent problems (e.g., dynamics after a quench) in 1D.



Cons: Limited by entanglement growth over time, less effective for equi

## 1.2 DMRG Tutorial this tutorial is not good. and i donot need it anymore. 
[simple dmrg](https://github.com/yangyuan16/simple-dmrg?tab=readme-ov-file) 
## 1.3 DMRG-X
每次DMRG时保存不止一个Ground State, 而且保存前结果Low Energy States. 这样扫一圈拿出低能态. 




# 2. QMC Quantum Monte Carlo

# 3. ED Exact Diagonalization

# 4. MF Mean Field

# 5. Bosonization Theory

# 6. IVM Iterative Variational Method
IVM是一种用于近似求解Hamiltonian本征问题的Krylov子空间变分方法. 它可以用于求解MPSC(Most Probable Spin Configs). 
**Steps:**
1. 利用$H$建立Krylov subspace, 在这个subspace里面表示ket. 
$$
\text{span}\{|\psi_{0}>,H|\psi_{0}>,H^{2}|\psi_{0}>,H^{3}|\psi_{0}>,\text{etc}\}
$$
2. 在建立subspace的同时, 动态调整**basis**, 优化表示. 具体而言, 指的只保留最低的几个能态. 
**Principle:**
-  为什么IVM可以找到最低几个本征值? 
	首先, subspace内的最低能态一定高于真实最低能态. 
$$
E_{0}(\text{subspace}) = \min_{\psi \in \text{subspace}} \frac{<\psi|H|\psi>}{<\psi|\psi>} \geq E_{0}(\text{real})
$$
	其次, 每次$H^{n+1}|\psi_{0>}$的过程都给Krylov subspace引入了新的维度. 
	我们相信不断引入的新维度可以逼近整个Hilbert space, 故相信它可以找到最低的几个本征值. 
	这也要求我们每次截断只保留最低的几个能态. 
- 前提prerequisite: 
	初始猜测态$|\psi_{0}>$与GS$|\text{Ground State}>$之间有重叠即
$$
<\psi_{0}|\text{Ground State}> \neq 0
$$
**Ad and Disad:**
- 效率很高, subspace维度可控. 
- 对于$L\geq 30$的系统效果不好, subspace dim仍旧会快速增长. (**$\mathcal{L\sim 30}$已经是一个非常巨大的1D quantum system了. **)
- gapless & highentropy & topological long range需要较大的迭代次数. 





