- [**_量子多体理论到底在干嘛？（观大黄猫老师新文章有感）_**](https://zhuanlan.zhihu.com/p/694940083)
    
- [**_灌水 · 凝聚态口一些蒙卡相关的学习笔记。_**](https://www.zhihu.com/column/c_167741624)
    

# 1. 重温经典MCMC(Markov Chain Monte Carlo)

- **Statistical approach to quantum field theory: An introduction: Chapter 04 Monte Carlo Simulations in Quantum Mechanics**
    

## 1.1 detailed balance condition

configuration distribution: $\pi(i)$ 

configuration distribution in **_equilbrium_**: $\pi_0(i)$

transfer matrix: $P(i \to j)$

detailed balance condition: $\pi(i)P(i \to j) = \pi(j)P(j \to i)$

**detialed balance condition is sufficient condition of global balance condition. (balance means _equilbrium_)**

- The derivation of 2 kind of balance condition:
    

  

## 1.2 Metropolis Hastings Algorithm

---
***Forget this***
The overall seneraio: we first choose a **update procedure** to generate new config from a initial config, then regard this update procedure as an **Adding Process(with no )**, regard the former configs as a 'bath' of proper configs. **Cite the conception of _Acceptance Rate \alpha_** which makes detailed balance chondition satisfied.
![[Pasted image 20250328111134.png]] 
 
**Add** a config with Acceptance Rate.

---

Stochastic vector: P_i

Stochastic Matrix:W_ij

Fixed Point of W_ij: **equilbrium**

**P_iWij = P_j**

Acceptance Rate:
$W(\omega,\omega^{\prime})=T(\omega,\omega^{\prime})A(\omega,\omega^{\prime})$ 

 $T$ Matrix is the probability of testing the new configs

A Matrix is the Acceptance Rate

**Regard the Metorpolis Hastings Procedure as a update procedure of a group of N configs(like 10k configs), every group of configs' generation is a matrix product procedure of W_ij^N. This makes the thermalization of MCMC reliable.**

**_Demonstration:_**

Every group actually means a stochastic vector **P** while generation of new groups means stochastic matrix **M^N**. (to some degree)

Group 1       Group 2       Group 3       Group 4      Group 5   ...

**CCCCCC**

**CCCCCC CCCCCC**

**CCCCCC CCCCCC CCCCCC**

**CCCCCC CCCCCC CCCCCC CCCCCC**

**CCCCCC CCCCCC CCCCCC CCCCCC CCCCCC ...**

  

- **Limitations:**
    

1. the acceptance rate is not 1, which means a much lower updating efficiency, higher self corelations and **critical slowing down**, which means more consumption of money: We need **cluster algorithm**.
    
2. low parallelization. We need **checkboard algorithm**.
    

## 1.3 Wolff Algorithm

- [Wolff Cluster Monte Carlo for 2D Ising Model](https://zhuanlan.zhihu.com/p/374610139)
    

### 1.3.1 Critical Slowing Down

Critical Slowing Down means that at the neiborhood of the critical temperature, fluaturation occurs dramatically. This leads to a longer relaxtion time, in other words, more steps needed for MCMC procedure. Critical Slowing Down would leads to larger autocorrelation essentially.

- Wolff and checkboard has weaken CSD greatly, but it's still a problem deserve attention.
    
- Other algorithm like Worm algorithm(useful for many quantum many body system). Worm represents for 2 defects, head and tail of a worm moving on the config. The acceptance strategy of Worm is similar to Metropolis'. And it's low parallelized.
    

### 1.3.2 Wolff

Refine the update strategy, let the changed part grow.

The stochastic matrix should be separated by the testing matrix T and the acceptance rate acceptance A.T means the probability of finding another config from the origional config while A represent for the acceptance rate.

The strategy of Wolff is to make A = 1. This, through complex math, would lead to a probability of growth of p = 1-exp(-2 beta J), with the constraints that the grown spin should be the same as its borner.

[**Proof of Wolff Algorithm**](https://hef.ru.nl/~tbudd/mct/lectures/cluster_algorithms.html)

  ![[Pasted image 20250328111233.png]]



- **History of this finding:** Wolff is not a genius but a genius. He implemented the condition of demanding for same spin direction of borner and grown spins. This makes the probability of finding the same cluster with 'DFS algorithm' the same and differences only occurs at the boundary.
    
- **Limitations:** It's very hard for Wolff algorithm to be implemented to other models
    

## 1.4 Checkboard Trick

[**checkboard GPU parallelization**](https://zhuanlan.zhihu.com/p/697577868?utm_psn=1869087184071565312)

**Choose independent events to parallelize.**

  

# 2. Quantum Monte Carlo

For a quantum model H = H_0 + gH_1, [H_0,H_1] is not **0**.

**Partition function:** Z = Tr{exp(-beta H)}

For a **complete basis** phi, we have:

![](file:///C:/Users/可爱的~1/AppData/Local/Temp/enhtmlclip/Image(9).png)![](data:image/png;base64,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)

---

**d dimentional quantum model = (d+1) dimensional calssical model**

**_Quantum Field Theory and Condensed Matter An Introduction_ R. Shankar**
![[Pasted image 20250328111249.png]] 
![[Pasted image 20250328111300.png]]
Thus, while both can be described as “integrals,” **they are very different in nature.** The quantum version is a functional integral over paths, which is why we say it “resembles” a (d+1)‐dimensional classical system in a discretized sense—but the extra dimension is not physically the same as a spatial one, and the corresponding measure D[x(τ)]\mathcal{D}[x(\tau)]D[x(τ)] reflects that difference.

---

- **Related Works:**
    

Below is a list of several quantum Monte Carlo (QMC) algorithms along with brief descriptions for each:

1. **Determinantal Quantum Monte Carlo (DQMC)**
    

- Uses auxiliary fields to decouple interactions, resulting in determinants that are evaluated over configurations. Widely used for **lattice fermion systems**.
    

3. **Auxiliary Field Quantum Monte Carlo (AFQMC)**
    

- Similar in spirit to DQMC, this approach introduces auxiliary fields to handle interactions, with applications in **both lattice and continuum fermionic systems**.
    

5. **World-Line Quantum Monte Carlo**
    

- Based on path-integral formulations in discrete imaginary time, this method samples “world-lines” of particles. It is especially useful for **bosonic and spin systems**.
    

7. **Path Integral Monte Carlo (PIMC)**
    

- Directly implements the path-integral representation of the quantum partition function. Often used for bosonic systems and for studying finite-temperature properties.
    

9. **Continuous-Time Quantum Monte Carlo (CT-QMC)**
    

- Avoids Trotter discretization errors by sampling directly in continuous imaginary time. Variants include CT-AUX (auxiliary field) and CT-INT (interaction expansion).
    

11. **Stochastic Series Expansion (SSE)**
    

- Expands the partition function as a power series in inverse temperature, then samples terms in the series. Particularly effective for spin systems.
    

13. **Variational Monte Carlo (VMC)**
    

- Uses a trial wave function with variational parameters and evaluates expectation values via Monte Carlo sampling. It’s a useful starting point for many-body wave function studies.
    

15. **Diffusion Monte Carlo (DMC)**
    

- A projector Monte Carlo method that projects out the ground state by simulating a diffusion process in imaginary time. Commonly used for continuum systems (e.g., electrons in molecules).
    

17. **Reptation Monte Carlo**
    

- A variant of projector methods that focuses on “reptating” (or sliding) paths to sample ground-state properties more efficiently.
    

19. **Worm Algorithm**
    

- Particularly designed to overcome ergodicity problems in world-line QMC, the worm algorithm introduces “worms” (defects) to sample off-diagonal correlations effectively.
    

Each of these algorithms has its strengths and limitations depending on the type of quantum system (fermionic, bosonic, or spin) and the physical properties (ground state, finite temperature, dynamics) you are interested in exploring.

---

# 3. Determinant Quantum Monte Carlo (DQMC)

DQMC(Determinant Quantum Monte Carlo) is a QMC algorithm suitable for quantum models with 2 fermions interaction. The Hubbard Model after Hubbard-Stratonovich Transformation is a example.

## 3.1 Hubbard Model after Hubbard-Stratonovich Transformation
https://www.zhihu.com/answer/1805794600
[H-S变换是凝聚态场论里最常用的技巧之一，主要用法是对四费米子相互作用进行解耦，我这里从数学和物理两个角度聊一下。](https://www.zhihu.com/question/421481863/answer/3458216150?utm_psn=1889279224503838287)



