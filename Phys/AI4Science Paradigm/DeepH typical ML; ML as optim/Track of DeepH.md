
![[Pasted image 20250517223659.png]]

**Perspective of Machine Learning Mechanism:**
- DeepH-1 has a singularity problem
- DeepH-E3 solved the singularity problem, introduced E(3) equivariance but has problem of efficiency-params dilemma. 
- DeepH-2 introduced ELCT, which transfer SO(3) to SO(2) via proper local coordinate selection and this solved the dilemma. Meanwhile, it introduce transformer arch, providing much more learnable params to accommodate. 
**To summary, module efficiency, learnable params and parallelization matters.**
jump out of the yard, DeepH-1 has solved the problem of effective data. 
thus, for a machine learning mechanism, **module efficiency(including parallelization), effective params(or learnable params) and effective data matter!** 
**Big is Beauty, More is Better(大就是美, 多就是好).** 
[chat with gemini](https://g.co/gemini/share/1c1b8cea6b18) 

# DeepH-1

- [[DeepH-1 Deep-Learning Density Functional Theory Hamiltonian for Efficient ab initio Electronic-Structure Calculation]] 
- [[Code Review of DeepH-1]]

![[Pasted image 20250512162721.png]]
gives a `MP` and `LCMP` mechanism. `LCMP` avoid discontinuity. 

# DeepH-E3

- [[DeepH-E3 General framework for E(3)-equivariant neural network representation of density functional theory Hamiltonian]] 
- [[e3nn Python Package]] 
![[Pasted image 20250513221812.png]] 
utiltize `e3nn.o3`'s $\mathrm{E(3)}$ sym. `e3nn` realized a global coordinate arch, which saved much computation and compeletely ***eliminated singularity*** in DeepH-1. 
here we introduced gate and **equivariant-tensorproduct**, 2 kinds of nonlinearity. the latter gives a diversity. 

# DeepH-2

- [[DeepH-2  Enhancing deep-learning electronic structure via an equivariant local-coordinate transformer]]
add transformer and Local Coordinate with $\mathrm{SO(2)}$ sym. this align the $z$ axis with its edges, leading to a better efficiency and accuracy. 
the Local Coordinates Selection tactics and $\mathrm{SO(3)}$ allow a ***much larger amount of learnable params***. meanwhile, **ELCT permits better parallelization**. 

# DeepH-r

- [[DeepH-r Deep learning density functional theory Hamiltonian in real space]]
this output $V_{\mathrm{KS}}(\vec{r})$ directly, which gives a freedom of basis. 

# DeepH-Zero

- [[DeepH-Zero Neural-network Density Functional Theory Based on Variational Energy Minimization]] 

here Xu introduced the **Variational Method**. they jumped out of the yard. 

# Others

## DeepH-hybrid

## xDeepH
