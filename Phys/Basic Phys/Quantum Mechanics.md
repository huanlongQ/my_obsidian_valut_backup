# Algebra of Commutor

$$
\begin{align}
 & \text{1) Linear: } & [aA+bB,cC+dD]  & = ac[A,C]+ad[A,D]+bc[B,C]+bd[B,D] \\  
 & \text{2) Leibniz Law:} & [AB,C ] & = A[B,C] + [A,C]B \\
 & \text{3) QM}\iff \text{CM counterpart} & \frac{[A,B]}{i\hbar} & \iff \{ A,B \}_{q,p}
\end{align}
$$

# From Classical Mechanics to Quantum Mechanics: Schrodinger Eq 

$$
\begin{align}
i\frac{\mathrm{d}}{\mathrm{d}t}\ket{\psi} = H\ket{\psi} 
\end{align}
$$

# Basic Properties of Wave Func 

1) normalization 
2) uncertainty principle 

$$
\begin{align}
( \langle A-\langle A \rangle  \rangle \times\langle B-\langle B \rangle  \rangle )^{2} \geq \frac{1}{4}\langle [A,B] \rangle  ^{2 } 
\end{align}
$$
**Proof**: 
$$
\begin{align}
 & \text{let: } &  f  =A-\langle A \rangle ,  & g=B-\langle B  \rangle  \\
 & \text{then: }  & \langle A-\langle A \rangle  \rangle    = \langle f \rangle ,  & \langle B-\langle B \rangle  \rangle = \langle g \rangle  \\
 & \text{square: }  & \langle f \rangle ^{2}= \bra{\psi} f\cdot f\ket{\psi}= \bra{f\psi}f\psi\rangle, & \langle g \rangle ^{2} = \langle \psi|g\cdot g|\psi \rangle = \langle g\psi| g\psi\rangle  \\
 & \text{Cauchy inequality:} & \langle f \rangle ^{2}\langle g \rangle ^{2}\geq \langle f\psi|g\psi \rangle ^{2}  & = |\underset{  \in \mathbf{R}  }{\underline{\underline{\underline{      \frac{ \langle f\psi|g\psi \rangle +\langle g\psi|f\psi \rangle  }{2}}}}}+\underset{  \in \text{ pure }\mathbf{C} ,\mathbf{I} }{\underline{\underline{\underline{    \frac{\langle f\psi|g\psi \rangle -\langle g\psi|f\psi \rangle }{2}  }}}}| ^{2} \\
 &  & &   = \frac{1}{4}(|\langle \psi| fg+gf|\psi \rangle |^{2}+|\langle \psi|fg-gf |\psi  \rangle |^{2}) \\
 &  &  & =\frac{1}{4} (|\langle [A-\langle A \rangle,B-\langle B \rangle  ] \rangle| ^{2} +|\langle [A-\langle A \rangle,B-\langle B \rangle  ]_{+} \rangle| ^{2} )  \\
 &  &  & =\frac{1}{4} |\langle [A,B] \rangle  |^{2} + \frac{1}{4}|\langle [A,B]_{+} \rangle |^{2} \\
 &  &  & \geq \frac{1}{4}|\langle [A,B ]\rangle |^{2} \\
 & \text{then we have:} & \langle A-\langle A \rangle  \rangle ^{2}\langle B-\langle B \rangle  \rangle ^{2} & \geq  \frac{1}{4}|\langle [A,B] \rangle  |^{2}
\end{align}
$$

**Time Energy Uncertainty**: 
...
3) orthogonality 

# Integrable System

## Free Electron

$$
\begin{align} 
H & =\frac{p^{2}}{2m} \\
\ket{\psi}   & = \ket{\vec{k}}
\end{align}
$$

## Harmonic Oscillation ⭐ 

$$
\begin{align}
 &  & H  & = \frac{1}{2m}p^{2}+\frac{1}{2}m\omega^{2}x^{2} \\
 & \text{let:}  & a = Ax+iBp\ ,\  & a^{\dagger} =Ax-iBp  \\
 & \text{then:} & A = \sqrt{ \frac{1}{2} \frac{m\omega^{2}}{\hbar \omega}}, & B = \sqrt{ \frac{1}{2m} \frac{1}{\hbar \omega} }  \\
 & \text{then: } & a^{\dagger}a  & \sim (x-ip)(x+ip)=x^{2}+p^{2}+i(xp-px) =x^{2}+p^{2}-\hbar \omega  \\
 &  &  & \sim H - \frac{1}{2}\hbar \omega \\
 & \text{then: } & H & = \hbar \omega\left( a^{\dagger}a + \frac{1}{2} \right)
\end{align}
$$
$a,a^{\dagger}$ are annihilation and creation operation: 
$$
\begin{align} 
[a,a^{\dagger}]  & = 1 \\
a^{\dagger}\ket{n}  & = \sqrt{ n+1 }\ket{n+1} \\
a\ket{n}  & =\sqrt{ n }\ket{n-1}  
\end{align}
$$
**Proof**: 
$$
\begin{align}
[a,a^{\dagger}] & \overset{\text{path 1}}{=} aa^{\dagger}-a^{\dagger}a = \dots = \frac{[x,p]}{i\hbar}=1 \\
 & \overset{\text{path 2}}{\sim} i\hbar \{ x+ip,x-ip \}_{x,p}=1\\
\langle an|an \rangle  &  = \langle n|a^{\dagger} a| n \rangle = n\langle n|n \rangle  \\
 & =K^{2}\langle n-1|n-1 \rangle = K^{2} \\
\implies  & K = \sqrt{ n }, a\ket{n} = \sqrt{ n }\ket{n-1} \\
\implies & a^{\dagger} \ket{n} = \sqrt{ n+1 }\ket{n+1}
\end{align}
$$

## $\delta$ potential

## Hydrogen Atom

$$
\begin{align}
  H  & = \frac{p^{2}}{2m} + V(r) \\
  & =-\frac{\hbar^{2}}{2m}\nabla^{2} + \frac{1}{4\pi \epsilon_{0}} \frac{e^{2}}{r} \\
 & \text{where: } \nabla^{2} = \frac{1}{r}\left( \frac{ \partial  }{ \partial r } \right)^{2}(r\cdot) - \frac{L^{2}}{\hbar^{2}r^{2}} 
\end{align}
$$

### $\nabla^2$ and Spherical Harmonic Func $Y_{lm}$

$$
\begin{align}
\nabla^{2}  & = \frac{1}{r}\left( \frac{ \partial  }{ \partial r }  \right)^{2}(r\cdot)-\frac{L^{2}}{\hbar^{2}r^{2}}  \\
L^{2} & \implies \hbar^{2}l(l+1) \\
L_{z} & \implies \hbar m  \\
\end{align}
$$ 

### Angular Momentum and its operators 

### Other effects

# Spin and Angular Momentum $\iff$ $\mathrm{SU}(2)$ or $\mathrm{SO(3)}$ Algebra⭐ 

Spin: 
$$
\begin{align}
 \sigma_{x} = \left[ \begin{array}{cccccccccc}  0 & 1 \\ 1 & 0 \end{array} \right] ,  & \sigma_{y}= \left[ \begin{array}{cccccccccc}  0 & -i \\ i & 0 \end{array} \right] , \sigma_{z} = \left[ \begin{array}{cccccccccc}  1 & 0 \\ 0 & -1 \end{array} \right]   \\
 & S_{i} = \frac{\hbar}{2}\sigma_{i}  
\end{align}
$$
Angular Momentum: 
$$
\begin{align}
L = r\times p  = \left[ \begin{array}{cccccccccc}    yp_{z}-zp_{y}\\ zp_{x}-xp_{z}\\xp_{y}-yp_{x} \end{array} \right]   
\end{align}
$$
**note both as** 
$$
\begin{align}
S = \left[ \begin{array}{cccccccccc} S_{x}   \\ S_{y} \\ S_{z} \end{array} \right]  
\end{align}
$$
1) **Commution Relation**⭐: 
$$
\begin{align}
[S_{i},S_{j}] = i\hbar\epsilon_{ijk} S_{k} \\
\end{align}
$$
then let $S^{2} = S_{x}^{2}+S_{y}^{2}+S^{2}_{z}$, we have: 
$$
\begin{align}
[S^{2},S_{i}] &  = \left( \sum_{i=1}^{3} S_{i}^{2}  \right)S_{i} - S_{i}\left( \sum_{i=1}^{3} S_{i}^{2} 
 \right) = S_{j}^{2} S_{i} + S_{k}^{2}S_{i} - S_{i}S_{j}^{2} - S_{i}S_{k}^{2} \\
 & = S_{j}S_{i}S_{j} + S_{j}[ S_{j},S_{i}] - S_{j}S_{i}S_{j} - [S_{i},S_{j}]S_{j} + \dots \\
 & =0 + S_{j}i\hbar \epsilon_{jik}S_{k} - i\hbar \epsilon_{ijk}S_{k}S_{j} + \dots \\
 & = i\hbar( \epsilon_{jik}S_{j}S_{k}-\epsilon_{ijk}S_{k}S_{j}) + \dots \\
 & =0 + 0 \\
 & =0\end{align}
$$
2) up and down (creation and annihilation) operators:
$$
\begin{align}
S_{+} = S_{x} + iS_{y} \\
S_{-} = S_{x} - iS_{y}
\end{align}
$$
to be up and down operators, it means: 
$$
\begin{align}
[S_{z},S_{+}] = +\hbar S_{+} \\
[S_{z},S_{-}] = -\hbar S_{-}
\end{align}
$$
they means that for any ket psi, we have:
$$
\begin{align}
S_{z}S_{+}\ket{\psi}  = (S_{+}S_{z} + [S_{z},S_{+}])\ket{\psi}  = S_{+}(S_{z}+\hbar)\ket{\psi}  \\
S_{z}S_{-}\ket{\psi}  = (S_{-}S_{z } + [S_{z},S_{-}])\ket{\psi} = S_{-}(S_{z}-\hbar)\ket{\psi}
\end{align}
$$
3) eigenvalues and eigenvectors of operators: 
$$
\begin{align}
\text{main operators: } S^{2}, S_{z}, S_{\pm}
\end{align}
$$

## Angular Momentum Coupling and CG coeff

- [CG coeff](https://www.zhihu.com/question/271044965/answer/361887639?share_code=CyRIzSxnrSm&utm_psn=1946931252356714995) 

$$
\begin{align}
 & \text{operator: }  & S ^{1+2}= S^{1}+S^{2}  \\
 & \text{state: }  & \ket{s_{1}m_{1}s_{2}m_{2}} \\
 & \text{observor: }  & m = m_{1}+m_{2} \tag{can be proved by apply operator}
\end{align}
$$
up and down (creation and annihilation) operator: 
$$
\begin{align}
 & S^{+} = S_{x}+ iS_{y},\  \ S^{+}\ket{sm} = \ket{s(m+1)} \\
 & S^{-} = S_{x}-iS_{y}, \ \ S^{-}\ket{sm} = \ket{s(m-1)} \\
 & \text{can be proved by apply commution relation}
\end{align}
$$

# Time Independent Perturbation Theory  

-  [Gemini - Quantum Mechanics Perturbation Theory **coeffs sign** Explained](https://g.co/gemini/share/5d935eaa9ebe) ⭐

**Formulas**: 
$$
\begin{align} 
H  & = H_{0}+V ,\text{ with } |\frac{V}{H_{0}}|\ll 1 \\
\ket{\psi}  & = \ket{\psi^{0}} +\sum_{i=1}^{\infty} \ket{\psi^{i}} \\
 E & = E^{0} + \sum_{i=1}^{\infty} E^{i}\\
  E^{1}_{n}  & = \langle n|V| n \rangle \\
\ket{\psi_{n}^{1}}  & = \sum_{m\neq n}\ket{m}\times\underset{  \text{above energy decrease, below energy increase.} }{\underline{\underline{\underline{   \frac{\langle m|V|n \rangle}{\pmb{E_{n}-E_{m}}}     }}}} ,\text{go to the above ⭐ Gemini chat} \\
E_{n}^{2} & =\sum_{m\neq n}\frac{\langle n|V|m \rangle\langle m|V| n\rangle}{E_n-E_m}   \\
\end{align}
$$

# Time Dependent Perturbation Theory

## Theory

**Formulas**: 
$$
\begin{align}
H & =H_{0}+V(t), \text{ with } \frac{|V(t)}{H_{0}}|\ll 1 \\
\ket{\psi}  & = c_{i}\exp\left( -i \frac{E_{i}}{\hbar}t \right)\ket{i} , \text{  apply EinSum rule} \\
\dot{c}_{i}  & = -\frac{i}{\hbar} \bra{i} V(t)\ket{j}c_{j}\times\underset{ \text{belike Rabi term, match and dismatch } V(t) \text{'s freq, } }{\underline{\underline{\underline{\exp\left( i \frac{E_{i}-E_{j}}{\hbar} t \right)}}}}  \\
 & =\pmb{-\frac{i}{\hbar}\bra{i(t)}V(t)\ket{j(t)} c_{j}} \\ 
i\hbar \frac{ \partial  }{ \partial t } \underset{ c_{i} }{\underline{\underline{\underline{
\left[ \begin{array}{cccccccccc}    \\  \\  \end{array} \right]  }}}}  & = \underset{ \bra{i(t)}V(t)\ket{j(t)}  }{\underline{\underline{\underline{\left[ \begin{array}{cccccccccc}   &  \\  &  \end{array} \right]   }}}} \underset{  c_{j}  }{\underline{\underline{\underline{   \left[ \begin{array}{cccccccccc}    \\  \\  \end{array} \right]     }}}}
\end{align}
$$

## Applications

### Sine Perturbation

for Two Level System, we have $H(t)=V\cos(\omega t)$ 
$$
\begin{align}
 & \text{initial state:} &  c_{0}=1, &c_{1}=0  \\
 & \text{then:} & i\hbar \frac{ \partial c_{1} }{ \partial t }  & = \bra{0}V\ket{1} \cos(\omega t) \exp\left( i\frac{ (E_{0}-E_{1})}{\hbar}t \right)c_{0}\\
 & \text{then:} &    \dot{c}_{1}  & = -\frac{i}{\hbar}V_{01} \frac{\exp(i\omega t)+\exp(-i\omega t)}{2} \exp\left( i\frac{(E_{0}-E_{1})}{\hbar}t \right) c_{0}  \\
 &  &  & =-\frac{i}{2\hbar}V_{01}c_{0}\left(  \exp\left( i\left( \omega - \frac{E_{1}-E_{0}}{\hbar} \right)t \right) +  \exp\left( i\left( \omega + \frac{E_{1}-E_{0}}{\hbar} \right)t \right)  \right) \\ 
 &  &  & \approx -\frac{i}{2\hbar}V_{01}   \exp\left( i\left( \omega - \frac{E_{1}-E_{0}}{\hbar} \right)t \right) + \underset{ \text{rotating wave approximation} }{\underline{\underline{\underline{\pmb{0} }}}}  \\
& \text{then:} & c_{1}(t) & = -i\frac{V_{01}}{\hbar} \times \frac{\sin\left( \frac{(\omega_{0}-\omega)t}{2} \right)}{\omega_{0}-\omega} \times \exp\left( i\frac{(\omega_{0}-\omega)}{2} t\right)  \\
& \text{then:}& |c_{1}(t)|^{2}  & =\pmb{\frac{|V_{01}|^{2}}{\hbar^{2}} \left[ \frac{\sin\left( \frac{(\omega_{0}-\omega)}{2} t\right)}{\omega_{0}-\omega}  \right]^{2} }= \boxed{\pmb{\frac{|V_{01}|^{2}}{\hbar^{2}(\omega_{0}-\omega)^{2}} \sin ^{2}\left( \frac{(\omega_{0}-\omega)}{2} t \right)}}
\end{align}
$$

### EM radiation

for single freq $\vec{E}=\hat{z}E_{z}\cos(\omega t)$. 

$$
\begin{align} 
V(t)  & = -qE_{z}z \cos(\omega t) \\
|c_{1}(t)|^{2}  & = \frac{|\bra{1}-qE_{z}z\ket{0} |^{2}}{\hbar^{2}} \left[ \frac{\sin\left( \frac{\omega -\omega_{0}}{2}t \right)}{\omega-\omega_{0}} \right]^{2} = \frac{|\bra{1}\vec{p}\ket{0} \cdot \vec{E}|^{2}}{\hbar^{2}} \left[ \frac{\sin\left( \frac{\omega-\omega_{0}}{2}t \right)}{\omega-\omega_{0}} \right]^{2} \\
 &  = \frac{E_{0}^{2}|\bra{1}p_{z}\ket{0}|^{2}}{\hbar^{2}} \left[ \frac{\sin\left( \frac{\omega -\omega_{0}}{2}t \right)}{\omega-\omega_{0}} \right]^{2}
\end{align}
$$

for energy density $\rho(\omega )\mathrm{d}\omega = \frac{1}{2}\epsilon_{0}E^{2}(\omega)\mathrm{d}\omega$, then: 
$$
\begin{align}
|c_{1}|^{2}(\omega)\mathrm{d}\omega & =\frac{2\rho(\omega)\mathrm{d}\omega}{\epsilon_{0}\hbar^{2}} |\bra{0}p_{z}\ket{1}|^{2} \left[ \frac{\sin\left( \frac{\omega-\omega_{0}}{2}t \right)}{\omega-\omega_{0}} \right]^{2} \\
|c_{1}|^{2}  & = \int|c_{1}|^{2}\mathrm{d}\omega \approx \frac{2|\bra{0}p_{z}\ket{1} |^{2}}{\epsilon_{0}\hbar^{2}}\rho(\omega_{0})\int_{0}^{\infty}\left[ \frac{\sin\left( \frac{\omega-\omega_{0}}{2}t \right)}{\omega-\omega_{0}} \right]^{2}\mathrm{d}\omega \\
  & \approx \frac{\pi|\bra{0}p_{z}\ket{1}|^{2}}{\epsilon_{0}\hbar^{2}}\rho(\omega_{0})\times t  \\
\text{then: } & \pmb{\boxed{ R  \equiv \frac{\mathrm{d}|c_{1}|^{2}}{\mathrm{d}t} = \frac{\pi|\bra{0}p_{z}\ket{1}|^{2} }{\epsilon_{0}\hbar^{2}}\rho(\omega_{0})\propto |\bra{0}p_{z}\ket{1}|^{2}\rho(\omega_{0}) } }
\end{align}
$$

### Selection Rule

$$
\begin{align}
\bra{nlm}\pmb{\vec{r}}\ket{n'l'm'} = \begin{cases}\text{not } 0 & |\Delta l|= \pmb{1} \text{ and }|\Delta m|= \pmb{0}\text{ or } \pmb{1} \\
0 & \text{others}
\end{cases}
\end{align}
$$

## Fermi Golden Rule
$$
\begin{align}
R=\frac{2\pi}{\hbar}|\frac{V_{if}}{2}|^{2}\rho(E_{f})
\end{align}
$$

## Adiabatic Theorem

-  [Gemini - CM QM counterpart of Adia Invar; QM Adia in Modern Phys; Proof of Adia Theorem](https://g.co/gemini/share/c1f07c26d892) ⭐

$$
\begin{align}
 & \text{Hamiltonian:} & H &  = H(\lambda), \frac{\mathrm{d}\lambda}{\mathrm{d}t} \ll 1    \\
 & \text{state:} & \ket{\psi}  & = \sum c_{i}(t)\exp\left( -\frac{i}{\hbar}\int E_{i}(t)\mathrm{d}t \right)\ket{i(t)} \\
 & \text{Schrodinger said:} & i\hbar \frac{ \partial  }{ \partial t } \ket{\psi} & =H(\lambda)\ket{\psi} \\
 & \text{left side: } & i\hbar \frac{ \partial  }{ \partial t } \ket{\psi} & =\sum i\hbar \frac{ \partial c_{i} }{ \partial t } \exp\left( -\frac{i}{\hbar}\int E_{i}(t)\mathrm{d}t \right)\ket{i(t)}  \\
 &  &  & +\sum c_{i}E_{i}(t)\exp\left( -\frac{i}{\hbar}\int E_{i}(t)\mathrm{d}t \right)\ket{i(t)}  \\
 &  &  & + \sum i\hbar c_{i}\exp\left( -\frac{i}{\hbar} \int E_{i}(t)\mathrm{d}t  \right) \frac{ \partial  }{ \partial t } \ket{i(t)} \\
 & \text{right side: } & H\ket{\psi} & =\sum c_{i}E_{i}(t)\ket{i(t)} \\
 &  \text{then: } & 0 & =\sum i\hbar  \dot{c}_{i} \exp\left( -\frac{i}{\hbar} \int E_{i}(t)\mathrm{d}t  \right)\ket{i(t)}  +i\hbar c_{i} \exp\left( -\frac{i}{\hbar} \int E_{i}(t)\mathrm{d}t  \right) \frac{ \partial  }{ \partial t } \ket{i(t)} \\
 & \text{inner product with }\bra{j(t)} & 0 & =   \dot{c}_{j}\exp\left(-\frac{i}{\hbar} \int E_{j}(t)\mathrm{d}t \right) +\sum   c_{i}\exp\left( -\frac{i}{\hbar} \int E_{i}(t)\mathrm{d}t  \right) \pmb{\bra{j(t)}\frac{ \partial  }{ \partial t } \ket{i(t)} }, \text{(⭐)}
\end{align}
$$
apply a algebraic manipulation: 
$$
\begin{align}
\frac{ \partial  }{ \partial t } (H\ket{i(t)})  & = \frac{ \partial  }{ \partial t } (E_{i}(t)\ket{i(t)}) \\
\dot{H}\ket{i(t)} + H\frac{ \partial  }{ \partial t } \ket{i{(t)}}  & = \dot{E}_{i}(t)\ket{i(t)} + E_{i}(t)\frac{ \partial  }{ \partial t } \ket{i(t)} \\
\text{inner product with }\bra{j(t)}\text{:} \bra{j(t)}\dot{H}\ket{i(t)}  + \bra{j(t)}H\frac{ \partial  }{ \partial t } \ket{i(t)} & =\dot{E}_{i}(t)\langle j(t)\ket{i(t)} + E_{i}(t)\bra{j(t)}\frac{ \partial  }{ \partial t } \ket{i(t)} \\
 \text{then:} \quad\bra{j(t)}\dot{H}\ket{i(t)}  &  = (E_{i}(t)-E_{j}(t))\times\bra{j(t)}\frac{ \partial  }{ \partial t } \ket{i(t)}   \\
  \text{then finally:}\ \ \  \boxed{\pmb{\bra{j(t)}\frac{ \partial  }{ \partial t } \ket{i(t)}    =\frac{\bra{j(t)}\dot{H} \ket{i(t)}}{E_{i}(t)-E_{j}(t)} }}
\end{align}
$$
then we have: 
$$
\begin{align}
 \dot{c}_{j}  & = -\sum c_{i}\exp\left( -\frac{i}{\hbar} \int (E_{j}(t)-E_{i}(t))\mathrm{d}t  \right) \frac{\bra{j(t)}\dot{H} \ket{i(t)}}{E_{i}(t)-E_{j}(t)}  \\
 & = \sum c_{i}\exp[i(\theta_{i}(t)-\theta_{j}(t)] \frac{\bra{j(t)}\dot{H} \ket{i(t)}}{E_{j}(t)-E_{i}(t)} 
\end{align}
$$
Because $\dot{H}\approx \frac{\mathrm{d}\lambda}{\mathrm{d}t} \ll {1}$
$$
\begin{align}  
\pmb{ \dot{c}_{j} \approx 0}\\
\end{align}
$$
 but if we have a closed path in the lambda space, then we got **Berry Phase**: (from (⭐) start: )
$$
\begin{align}
 & \text{if we start from j-th state}: & c_{j}=1b,  & \pmb{c_{i\neq j}=0}  \\
 & \text{⭐ formula:}  & \dot{c}_{j} & =-c_{j}\bra{j(t)}\frac{ \partial  }{ \partial t } \ket{j(t)}  =  \\
 &  &  & =-c_{j}\bra{j(\lambda(t)) }\frac{ \partial \lambda }{ \partial t } \frac{ \partial  }{ \partial \lambda } \ket{j(t)} \\
 & \text{then:}  & \frac{ \partial  c_{j}}{ \partial \lambda }  & = \boxed{c_{j} \times i\times i\bra{j(\lambda)}\frac{ \partial  }{ \partial \lambda } \ket{j(\lambda)}  } \\
 & \text{then:}  & \gamma  & = \boxed{\pmb{i\int\bra{j(\lambda)}\frac{ \partial  }{ \partial \lambda } \ket{j(\lambda)}\mathrm{d}\lambda}}  
\end{align}
$$

# Variations Principle  
