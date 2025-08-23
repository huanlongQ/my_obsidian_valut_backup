The key feature of Tensor Network Representation is to ***reduce the complexity of quantum problem***  $O(2^{ \text{Scale} }) \to O(\text{Poly}(\text{Scale}))$ . 
* Examples: **Matrix Product State, Tree TN, projected entangled pair state**
	![[Pasted image 20250328133712.png]]

# 1. Matrix Product State (MPS)
Thank MPS, I have learnt the trick of **tensor diagram**. 
## 1.1 Theory of MPS
The normal form of a quantum state: 
$$
∣\Psi⟩=\sum_{i_1​,i_2​,…,i_N}​​C_{i_1​,i_2​,…,i_N}​​​∣i_1​⟩∣i_2​⟩⋯∣i_N​⟩
$$
while the MPS is: 
$$
∣\Psi⟩=\sum_{i1​,i2​,…,iN}A^{[1]}_{i_1} ​A^{[2]}_{i_{2}}​ \dots|i_{1},i_{2},i_{3}\dots\rangle
$$
$A^{[k]}_{i_{k}}$ is a group of  $D_{k-1}\times D_{k}$  matrix, $D_{k}$ is bond dimension. Bond dimension controls the amount of entanglement MPS can capture. 
The translation from MPS to normal quantum states is just contraction law of tensor: 
$$
C_{i_{1}i_{2}i_{3}\dots} = \Pi_{i_{1}i_{2}i_{3}\dots} A^{[1]}_{i_{1}}A^{[2]}_{i_{2}}\dots
$$
**Efficiency:**
The efficiency of MPS, from exp complexity to poly, owe to **sparsity*** nature of quantum states, AKA **Area Law**.
The scale of Hilbert space is reduced from $O(d^{N})$ to $O(NdD^{2})$ Where $d$ is the **local dimension** of a lattice state. 
- physical meaning of bond dimensions
	bond dim shows the amount of entanglement entropy
	![[b69d313c0cc0b56efb854d1366c4b83.jpg]]![[240f1cdeacc2268e98cd1d1e530a44b.jpg]] 





## 1.2 Orthogonalization and Canonical Forms of MPS
Normally, we use singular value decomposition (**SVD**) or QR decomposition to orthogonalize a MPS. If we add a truncation process, this means **depressing storage**. 
![[Pasted image 20250329171011.png]]**Canonical Form:**
MPS is a non-unique representation of quantum states. Thus we need canonical forms to confirm a certain state. 
orthogonalization method like SVD and QR is used to establish a canonical form from a casual arranged(or any) MPS. 
![[Pasted image 20250329172816.png]]

## 1.3 Entanglement Entropy of a MPS
### **2 site MPS**
$\psi_{s_{1}s_{2}} =^{\mathrm{SVD}} A_{s_{1}\alpha}\Lambda_{\alpha \beta}B_{\beta s_{2}}$
for a left canonical form MPS, we have $A^{^{\dagger} }A = I, A_{ab}^{*}A_{ac} = \delta_{bc}$
for a right canonical form MPS, we have $B^{\dagger}B = I,B_{ab}^{*}B_{ac}=\delta_{bc}$ 
so we have (**ps,** $\psi$ **is a vector so no changing order of index**)
$$
\begin{align}
\rho_{s_{1}s_{2},s_{1}'s_{2}'} = &  (\psi_{s_{1}'s_{2}'})^{\dagger}\psi_{s_{1}s_{2}} \\ \\
= & A_{s_{1}'\alpha'}^{*}\Lambda_{\alpha'\beta'}^{*}B_{\beta's_{2}'}^{*}A_{s_{1}\alpha}\Lambda_{\alpha \beta}B_{\beta s_{2}} \\
= & A_{s_{1}'\alpha'}^{*}A_{s_{1}\alpha}\Lambda^{*}_{\alpha'\beta'}\Lambda_{\alpha \beta}B^{*}_{\beta's_{2}'}B_{\beta s_{2}} \\

\end{align}
$$
$$
\begin{align}
\rho^{(2)}_{s_{2}s_{2}'}= & \mathbf{Tr_{1}}(\rho_{s_{1}s_{2},s_{1}'s_{2}'})=\delta_{s_{1}s_{1}'}A_{s_{1}'\alpha'}^{*}A_{s_{1}\alpha}\Lambda^{*}_{\alpha'\beta'}\Lambda_{\alpha \beta}B^{*}_{\beta's_{2}'}B_{\beta s_{2}} \\
 & = \delta_{\alpha'\alpha}\Lambda^{*}_{\alpha'\beta'}\Lambda_{\alpha \beta}B^{*}_{\beta's_{2}'}B_{\beta s_{2}} \\
 & =\Lambda^{*}_{\alpha\beta'}\Lambda_{\alpha \beta}B^{*}_{\beta's_{2}'}B_{\beta s_{2}}  \\
 & =|\lambda_{\beta}|^2\delta_{\beta \beta'}B^{*}_{\beta's_{2}'}B_{\beta s_{2}}  \\
 & =|\lambda_{\beta}|^2B^{*}_{\beta s_{2}'}B_{\beta s_{2}}
\end{align}
$$
so here we have a entropy:
$$
S(\rho) = -\sum |\lambda_{\beta}|^2 \log(|\lambda_{\beta}|^2)
$$

for normal 2 site MPS, the SVD algo gives a left and right canonical form MPS, so we have similar algebra for $\mathbf{Tr_{2}}(\rho_{s_{1}s_{2},s_{1}'s_{2}'})$. so entropy is entropy for both calculation direction. 

### **multi-site MPS**
$\psi_{s_{1}s_{2}s_{3}} =^{\mathrm{SVD}} A_{s_{1}\alpha}\Lambda_{\alpha \beta}B_{\beta s_{2}\gamma}\Theta_{\gamma \zeta}C_{\zeta s_{3}}$
assume that we have a left or right canonical form MPS SVD. entanglement between subsys 1 and subsys 2+3 is similar. then we need to concat the second subsys 2+3: 
$$
\psi_{s_{1}s_{2}s_{3}}=\psi_{s_{1}(s_{2}s_{3})} 
$$
then we have 
$$
\begin{align}
\rho_{s_{1}(s_{2}s_{3}),s_{1}'(s_{2}'s_{3}')}  & = \psi_{s_{1}'(s_{2}'s_{3}')}^{*}\psi_{s_{1}(s_{2}s_{3})} \\
 & =  A_{s_{1}'\alpha'}\Lambda_{\alpha' \beta'}B_{\beta' s_{2}'\gamma'}\Theta_{\gamma' \zeta'}C_{\zeta' s_{3}'} A_{s_{1}\alpha}\Lambda_{\alpha \beta}B_{\beta s_{2}\gamma}\Theta_{\gamma \zeta}C_{\zeta s_{3}} \\
 & =A_{s_{1}'\alpha'}A_{s_{1}\alpha}\Lambda_{\alpha' \beta'}\Lambda_{\alpha \beta}B_{\beta' s_{2}'\gamma'}B_{\beta s_{2}\gamma}\Theta_{\gamma' \zeta'}\Theta_{\gamma \zeta}C_{\zeta' s_{3}'}C_{\zeta s_{3}}
\end{align}
$$
then we do trace over subsys 1 (under left canonical form)
$$
\begin{align}
\rho^{(2+3)}_{s_{2}s_{3},s_{2}'s_{3}'} & =\mathbf{Tr_{1}}\rho_{s_{1}(s_{2}s_{3}),s_{1}'(s_{2}'s_{3}')} \\
& =  \delta_{s_{1}s_{1}'}A_{s_{1}'\alpha'}A_{s_{1}\alpha}\Lambda_{\alpha' \beta'}\Lambda_{\alpha \beta}B_{\beta' s_{2}'\gamma'}B_{\beta s_{2}\gamma}\Theta_{\gamma' \zeta'}\Theta_{\gamma \zeta}C_{\zeta' s_{3}'}C_{\zeta s_{3}} \\
 & =\delta_{\alpha \alpha'}\Lambda_{\alpha' \beta'}\Lambda_{\alpha \beta}B_{\beta' s_{2}'\gamma'}B_{\beta s_{2}\gamma}\Theta_{\gamma' \zeta'}\Theta_{\gamma \zeta}C_{\zeta' s_{3}'}C_{\zeta s_{3}} \\
 & =|\lambda_{\beta}|^{2}\delta_{\beta \beta'}B_{\beta' s_{2}'\gamma'}B_{\beta s_{2}\gamma}\Theta_{\gamma' \zeta'}\Theta_{\gamma \zeta}C_{\zeta' s_{3}'}C_{\zeta s_{3}} \\
 & =|\lambda_{\beta}|^{2} B_{\beta s_{2}'\gamma'}B_{\beta s_{2}\gamma}\Theta_{\gamma' \zeta'}\Theta_{\gamma \zeta}C_{\zeta' s_{3}'}C_{\zeta s_{3}}
\end{align}
$$
well, hard to see. 
but the entropy is 
$$
S(\rho) = -\sum |\lambda_{\beta}|^2  \log(|\lambda_{\beta}|^2 )
$$
do similar trace but over subsys 2+3 
$$
\begin{align}
\rho^{(1)}_{s_{2}s_{3},s_{2}'s_{3}'} & =\mathbf{Tr_{2+3}}\rho_{s_{1}(s_{2}s_{3}),s_{1}'(s_{2}'s_{3}')} \\
& =  \delta_{s_{2}s_{2}'}\delta_{s_{3}s_{3}'}A_{s_{1}'\alpha'}A_{s_{1}\alpha}\Lambda_{\alpha' \beta'}\Lambda_{\alpha \beta}B_{\beta' s_{2}'\gamma'}B_{\beta s_{2}\gamma}\Theta_{\gamma' \zeta'}\Theta_{\gamma \zeta}C_{\zeta' s_{3}'}C_{\zeta s_{3}} \\  
 & = A_{s_{1}'\alpha'}A_{s_{1}\alpha}\Lambda_{\alpha' \beta'}\Lambda_{\alpha \beta}(B_{\beta' s_{2}'\gamma'}\delta_{s_{2}s_{2}'}B_{\beta s_{2}\gamma})\Theta_{\gamma' \zeta'}\Theta_{\gamma \zeta}(C_{\zeta' s_{3}'}\delta_{s_{3}s_{3}'}C_{\zeta s_{3}} ) \\
 & =A_{s_{1}'\alpha'}A_{s_{1}\alpha}\Lambda_{\alpha' \beta'}\Lambda_{\alpha \beta} 
(\delta_{\beta \beta'}\delta_{\gamma \gamma'})\Theta_{\gamma' \zeta'}\Theta_{\gamma \zeta}(\delta_{\zeta \zeta'}) \\
 & =A_{s_{1}'\alpha'}A_{s_{1}\alpha}|\lambda_{\alpha}|^{2}\delta_{\alpha \alpha'}\delta_{\gamma \gamma'}|\theta_{\gamma}|^{2 } \delta_{\gamma \gamma'}  \\
 & =A_{s_{1}'\alpha}A_{s_{1}\alpha}|\lambda_{\alpha}|^{2}\sum_{\gamma}|\theta_{\gamma}|^{2 }  \\
 & =A_{s_{1}'\alpha}A_{s_{1}\alpha}|\lambda_{\alpha}|^{2}
\end{align}
$$
so the entropy is 
$$
S(\rho) = -\sum |\lambda_{\alpha}|^2  \log(|\lambda_{\alpha}|^2 )
$$
so the next question is whether or not the $\lambda$s are the same? 
Yes, the spetrum of a decomposition is unique: 
$$
\begin{align}
|\psi\rangle & = a_{ijk}|ijk\rangle \\
 & =^{\mathrm{SVD}}U_{ii}\lambda_{i}\delta_{ij}V_{jj}\theta_{j}\delta_{jk}W_{kk}|ijk\rangle \\
 & = \lambda_{i}\theta_{j}\delta_{ij}\delta_{jk} U_{ii}V_{jj}W_{kk}|ijk\rangle \\
 & =\lambda_{i}\theta_{j}\delta_{ij}\delta_{jk} |i'j'k'\rangle
\end{align}
$$
if we have 2 kinds of this decomposition, then we have
$$
\begin{align}
|\psi\rangle  & = \lambda_{i}'\theta_{j}'\delta_{ij}\delta_{jk} |i''j''k''\rangle\\
 & = U'_{ii}V'_{jj}W'_{kk}\lambda_{i}'\theta_{j}'\delta_{ij}\delta_{jk} |i'j'k'\rangle \\
 & =U'_{ii}\lambda_{i}'V'_{jj}\theta_{j}'W'_{kk}\delta_{ij}\delta_{jk}|i'j'k'\rangle
\end{align}
$$
then we have 
$$
\begin{align}
 \lambda_{i} &  =   U'_{ii}\lambda_{i}' \\
 \theta_{j} & =  V'_{jj}\theta_{j}' \\
 1_{kk}  & =   W'_{kk}
\end{align}
$$
so we can see that no matter what decomposition under any general MPS form, its spectrum is unique. 
$$
\begin{align}
|\lambda_{i} | & = |U'_{ii}\lambda_{i}'| \\
|\theta_{j}| & =|V'_{jj}\theta_{j}'| \\
I  & = W'
\end{align}
$$

# 2. DMRG
DMRG is a nice technical method to calculate the ground state of a particular quantum system. It suits well for 1D system for $10^{2\sim {3}}$ level size, which is really big. DMRG-X is a good method for cal the low energy states. 
## 2.1 DMRG Density Matrix Renormalization Group
[DMRG 的原理](https://zhuanlan.zhihu.com/p/1920278979)
**[[拉格朗日的忧郁, 一只冰牙喵](https://www.zhihu.com/people/li-hui-53-72)](https://www.zhihu.com/question/426281684)** **this is the most crucial website to learn DMRG and other series of MPS technique.** 
DMRG is worked only for ground state calculation primarily. It's also a iterative convergence algorithm. 
DMRG sweep the MPS iteratively, choosing ground state in every blocked local tensor states. Effective Hamiltonian is constructed from MPO(Matrix Product Operator) representation of the overall Hamiltonian. 

## 2.2 MPO in DMRG (Matrix Product Operator)
MPO is constructed by a **finite states automaton(有限状态机)** normally. 
[密度矩阵重整化群中哈密顿量的MPO构造方法](https://zhuanlan.zhihu.com/p/686289388)
The big obj is a Hamiltonian. 
![[Pasted image 20250330152954.png]]  

**DMRG** $H_{\text{eff}}:$ As you should know, if a state is the ground state of a quantum system, this $H_{\text{eff}}$ would be just a identify mapping for the 2-site MPS. 
![[Pasted image 20250330172436.png]]



## 2.3 DMRG-X
















# 3. Time Dependent Evolution of Tensor Network TEBD and TDVP
TEDB and TDVP are protable methods for the time evolution of MPS.
## 3.1 Intorduction to TEBD: Schrodinger Eq under MPS representation
 TEBD obeys the philosophy of DMRG to act on 2 site each step. 

**Time Evolving Block Decimation: Trotter Decomposion of propagatior + SVD + Truncation**   
	![[Pasted image 20250329193614.png]]
	![[Pasted image 20250328141712.png]]
This method is genius, totally genius. It shows an art of alignment. 



## 3.2 TDVP(Time Dependent Variational Principle) another genius method
regard the MPS math struct as a **manifold**, projecting the $\psi$ and $H$ into this MPS manifold. Update the whole MPS with this projection method. 
	![[Pasted image 20250410211722.png]]
