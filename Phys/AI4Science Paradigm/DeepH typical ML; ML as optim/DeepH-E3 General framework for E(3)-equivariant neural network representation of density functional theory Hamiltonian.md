
# Contents:
## 1. Arch: 
- ***E3 property is deployed to solve the problem of DeepH-1's incontinunity.***   
DeepH-E3 is very different from DeepH. It contains **spin-orbital** coupling and E3 covariance. 
**DeepH E3 is much more complex.**  
![[Pasted image 20250513145250.png]]
DeepH seek for a invariant basis: **local coordinate basis**, while DeepH-E3 wanna to realize true covariance. 
**You have to read the raw paper in detail to understand it.**

ENN is equivariant neural network, it obeys
$$
\mathrm{ENN}(\mathcal{D}(\mathbf{R})\cdot x) = \mathcal D (\mathbf{R}) \cdot \mathrm{ENN}(x)
$$
**there should be a dimension that related to $\mathcal D(\mathbf{R})$ but not related to $\mathrm{ENN}$**. genius! 
specifically, normal layers of DeepH-E3 do not touch $l,m$ indices. 
by the way, $x$ obeys
$$
x_{lm} = \sum_{m' =-l}^{l} D_{mm'}^{l}(\mathbf{R})x'_{lm'}
$$
**Core Block: EquiConv** 
![[Pasted image 20250513163202.png]]
```
eB shape (NeB,1) l=0 type vector
vi shape (Nv,2l+1) l=l type vector
eij shape (Ne,2l+1) l=l type vector
x^(l)_cm shape (2Nv+Ne,2l+1) l=l type vector
z^(l+1)_cm shape (2Nv+Ne,2(l+1)+1) l=l+1 type vector
```

complex but too complex. 
![[Pasted image 20250513221812.png]] 

`Irreps` is a python pkg in `e3nn`, account for different channels of each $l$ indexed tensor slice. 

**$e_{ij}$ has a shape of `(ij_indexed_edga, num_l, num_channel_of_l,num_m = 2*l+1)`.** 
**this would account for** $H_{ij,\alpha \beta,l_{\alpha}l_{\beta},m_{\alpha}m_{\beta}}$, **where $\alpha \beta$ are different main quantum number states, totally acounts for the hopping between $(\alpha,l_{\alpha},m_{\alpha})$ and $(\beta,l_{\beta},m_{\beta})$.** 
there would add a $s$ spin quantum number if needed. 
**from now on, you should take care of the dimension index and dimension num, they are totally different but stupidly, ambiguously written.** 
[with gemini non overall succeed chat](https://g.co/gemini/share/82bd70582753) 
