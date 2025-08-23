# 1. Information Theory
## 1.1 **Entropg as a measurement of information.** 
In information theory, entropy quantifies the average amount of information produced by a source of data, or equivalently, how unpredictable that source is. Imagine you’re flipping a coin. If it’s a fair coin (50% heads, 50% tails), you’re maximally uncertain about the outcome—there’s a lot of "information" in each flip because you can’t predict it. If the coin is biased (say, 99% heads), you’re less surprised by the result, so there’s less information per flip. Entropy measures this.
$$
p(0) =p(1)= \frac{1}{2}
$$
then $$
H = -\sum_{i}p(x_{i})\log_{2}p(x_{i}) = -\sum_{0,1} \frac{1}{2}\log_{2}\left( \frac{1}{2} \right) = 1
$$
for a $3$ faces coin, it would be below amount of information if you know the consequence in prior
$$
H = -\sum_{0,1,2} \frac{1}{3}\log_{2}\left( \frac{1}{3} \right) = \log_{2}3
$$
for a $n$ faces coin, it would be below amount of information if you know the consequence in prior
$$
H = -\sum_{0 \dots n-1 } \frac{1}{n}\log_{2}\left( \frac{1}{n} \right) = \log_{2}n
$$
if it's a bi-distrubute, with $p,1-p$, it would be a convex function $H(p)$
$$
H(p) = -p\log_{2}p - (1-p)\log_{2}(1-p)
$$
**to summary, the more average, the larger entropy, the more possible results, the larger entropy.** 


# 2. Quantum Entanglement, Entanglement Entropy and Information Entorpy
## 2.1 A Narrative Description: 
commonly we use a vector in Hilbert space (or MPS, whatever) to represent a state. however, density matrix is also used: 
$$
\rho = |\psi\rangle\langle \psi |

$$
for a quantum system splited into 2 subsystem $A$ and $B$: 
$$
\rho = |a,b\rangle\langle a,b|
$$
and the above things are a non-entangled state. 
for a more complicated version: 
$$
|a,b\rangle = |a\rangle \otimes \sum|\beta_{i}\rangle
$$
then $$
\rho = |a\rangle \otimes \sum|\beta_{i}\rangle\langle a| \otimes \sum\langle \beta_{i}| = |a\rangle \langle  a| \otimes \sum|\beta_{i} \rangle \sum\langle \beta_{i}|
$$
then Trace over $B$ would be
$$
\rho_{A} = \text{Tr}_{B}(\rho) = |a\rangle \langle  a| \otimes  \text{Tr}_{B}\sum|\beta_{i} \rangle \sum\langle \beta_{i}| = |a\rangle\langle a|
$$ 
this, intrinsicly, for any basis of $A$ Hilbert subspace, is a $0$ entanglement entropy state. 

**Thus, we realize that the non-entangled state is a state that can be constructed by outer product of 2 states from each subsystem.**

For a entangled state: 
$$
|\psi\rangle =( |00\rangle + |11\rangle )/ \sqrt{ 2 }
$$
which is a (0,2) tensor(means take into 2 vector and 0 covector in dual space, and give a number). 
then outer product
$$
\begin{align}
\rho = |\psi\rangle \langle \psi| &= 1/2 (|00\rangle + |11\rangle )\otimes(\langle 00| +\langle 11|) \\&
 = \frac{1}{2}( |00\rangle\langle 00| + |00\rangle\langle 11| + 
|11\rangle\langle 00| + |11\rangle\langle 11|)
\end{align}
$$

which is a (2,2) tensor(take into 2 vectors and 2 covectors, and give a number)
then: 
$$
\rho_{A} =\text{Tr}_{B} \rho = \frac{1}{2} \text{Tr}_{B}( |00\rangle\langle 00| + |00\rangle\langle 11| + \\
|11\rangle\langle 00| + |11\rangle\langle 11|)
$$
$$
 = \frac{1}{2} \text{Tr}_{B}( |0\textcolor{red}{0}\rangle\langle 0\textcolor{red}{0}| + |0\textcolor{red}{0}\rangle\langle 1\textcolor{red}{1}|) + \text{Tr}_{B}(\\
|1\textcolor{red}{1}\rangle\langle 0\textcolor{red}{0}| + |1\textcolor{red}{1}\rangle\langle 1\textcolor{red}{1}|)
$$
$$
 =  \frac{1}{2} \text{Tr}_{B}( |00\rangle\langle 00| + 0) + \text{Tr}_{B}(\\
0 + |11\rangle\langle 11|)
$$
$$
=\frac{1}{2 }( |0\rangle\langle 0 | )_{A}+ \frac{1}{2}( |1\rangle\langle 1 | )_{A}
$$
---
**p.s.** $$
\text{Tr}_{ab}T_{ab,cd\dots} = \delta_{ab}T_{ab,cd\dots}
$$
---
this shows entangle entropy: 
$$
S(\rho_{A}) = -\text{Tr}_{A} \rho_{A}\log_{2}\rho_{A}
$$
This entanglement entropy measures the information i get for $A$ when I know the measure result of subspace $B$. For example, in the above case, if I know the measure result of subspace $B$ is $0$, for the $S = \text{Tr}_{B} (-\rho_{A}\log_{2}\rho_{A}) = 1$ entanglement entropy, I can immediately know that the result of subspace $A$ is $0$.  




