一直以来, 我从未真正好好地理解过量子系统里的Green Func, 早晚有一天得学习一下的. 
Papers: 
- [Machine learning for Many-Body Physics: the case of the Anderson impurity model](https://doi.org/10.1103/PhysRevB.90.155136)
# 1. Theory of Green Func
**definition**: 
$G(\mathbf{r},t;\mathbf{r}^{\prime},t^{\prime})=-\mathrm{i}\langle\mathcal{T}\hat{\psi}(\mathbf{r},t)\hat{\psi}^{\dagger}(\mathbf{r}^{\prime},t^{\prime})\rangle$
**Notations**:
- $r',t'$ are original timespace point while $r,t$ are eventual timespace point.  
- $\hat{\psi}(r,t)$ is op of fermion field. here the fermions are quasiparticles. 
- $\mathcal{T}$ is time order op
- $G$'s physical meaning: quantum amplitude of opeator **create**$\hat{\psi}^{^{\dagger}}$ a fermion at $(r',t')$ and then **annihilate**$\hat{\psi}$ it at $(r, t)$. 
- $\hat{\psi}(r,t)$ here we have a op dependent on time. this means all of the obj is in **Hesisenberg Picture**. 
- $<>$ means $<0|\cdot|0>$ where $|0>$ mean ground state for zero temp or equilbrium state for finite temp. 
$$
\hat{\psi}_{H}(r,t) = e^{ iHt }\hat{\psi}_{S}(r)e^{ -iHt }
$$
$$
\hat{\psi}_{S}(r) = \sum_{n\text{ for band index},i\text{ for wannier or bloch basis}} \phi_{n,i}(r)\hat{c}_{ni}
$$
$$
\hat{\psi} = \hat{\psi}_{\text{filled }} + \hat{ \psi}_{\text{empty}}
$$
$$G^R(t,t^{\prime})=-i\theta(t-t^{\prime})\langle0|\{\hat{\psi}_{\mathrm{filled}}+\hat{\psi}_{\mathrm{empty}},\hat{\psi}_{\mathrm{filled}}^\dagger+\hat{\psi}_{\mathrm{empty}}^\dagger\}|0\rangle.$$
filled means the valance band while empty means the conduction band. 
only $\hat{\psi}_{\mathrm{empty}}(t)\hat{\psi}_{\mathrm{empty}}^\dagger(t^{\prime})$ is not zero. 
for a GS, we can see: 
$$
\begin{align}
\hat{\psi}_{H}(r,t)|0> &= e^{ iHt }\hat{\psi}_{S}(r)e^{ -iHt } |0>\\  
 &= e^{ iHt }\hat{\psi}_{S}(r)|0(t)>_{S}

\end{align}
$$
	thus, the Green function
$$
G(\mathbf{r},t;\mathbf{r}^{\prime},t^{\prime})=-\mathrm{i}\langle\mathcal{T}\hat{\psi}(\mathbf{r},t)\hat{\psi}^{\dagger}(\mathbf{r}^{\prime},t^{\prime})\rangle
$$
	shows the property of both the ***Hilbert Space*** and the ***Hamiltonian***.  

## 1.1 Retarded Green Func and Advanced Green Func. 
$$G^R(\mathbf{r},t;\mathbf{r}^{\prime},t^{\prime})=-\operatorname{i}\theta(t-t^{\prime})\left\langle\{\hat{\psi}(\mathbf{r},t),\hat{\psi}^\dagger(\mathbf{r}^{\prime},t^{\prime})\}\right\rangle$$$$G^A(\mathbf{r},t;\mathbf{r}^{\prime},t^{\prime})=+\operatorname{i}\theta(t^{\prime}-t)\langle\{\hat{\psi}(\mathbf{r},t),\hat{\psi}^{\dagger}(\mathbf{r}^{\prime},t^{\prime})\}\rangle$$ for the above formulas, $\theta(t-t')$ is **step function**, which means **casuality** for the retarded green func, and inverse **casuality** for the advanced green func. 
for the advanced green function, it means 

- physical meaning of retarded GF: 
	first create a fermion at $(r',t')$, then annihilate a fermion at $(r,t)$ 
- physical meaning of Advanced GF: 
	first annilate a fermion at $(r,t)$ and then find create this fermion at $(r',t')$. **Notice**: $t'>t$ in math, which means really strange effect cuz $t', t$ means the original and eventual event in physics. 
$$G(\mathbf{r},t;\mathbf{r}^{\prime},t^{\prime})=-\mathrm{i}\left \langle\mathcal{T}\hat{\psi}(\mathbf{r},t)\hat{\psi}^{\dagger}(\mathbf{r}^{\prime},t^{\prime})\right\rangle = G^{A} + G^{R}$$ 
use formula
$$\mathcal{T}\left[\hat{A}(t)\hat{B}(t^{\prime})\right]=\begin{cases}\hat{A}(t)\hat{B}(t^{\prime}),&t>t^{\prime},\\\pm\hat{B}(t^{\prime})\hat{A}(t),&t^{\prime}<t^{\prime},&&\end{cases}$$
 $+$ for bosons and $-$ for fermions. 
 $$\begin{aligned}G(t,t^{\prime})&=G^R(t,t^{\prime})\left.\theta(t-t^{\prime})+G^A(t,t^{\prime})\right.\theta(t^{\prime}-t)\\G^R(t,t^{\prime})&=-i\left\langle0|\hat{\psi}_{\mathrm{empty}}(t)\right.\hat{\psi}_{\mathrm{empty}}^{\dagger}(t^{\prime})|0\rangle,\\G^A(t,t^{\prime})&=+i\left\langle0|\hat{\psi}_{\mathrm{filled}}^{\dagger}(t^{\prime})\right.\hat{\psi}_{\mathrm{filled}}(t)|0\rangle.\end{aligned}$$$G^{R}$ shows the evolution of electrons while $G^{A}$ shows the evolution of holes(create a hole and then annihilate it) 



- In a mathematics perspective: for **linear differential equation**, we have here the derivation of the Green Function.  
	![[Pasted image 20250411234002.png]]

# 2. Physics of Green Function
In principle, Green Func shows the motion of electrons in a many body system. 
## 2.1 Dyson's revision

## 2.2 spectra of Green Function
