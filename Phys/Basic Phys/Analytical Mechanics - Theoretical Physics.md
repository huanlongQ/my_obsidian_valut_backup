# From Newton to Euler Lagrange 

- [拉格朗日力学](https://zhuanlan.zhihu.com/p/689698377) 

从牛顿力学出发, 我们首先由达朗贝尔原理消除了非主动力(约束力)的影响. 而后, 在多元微积分和变分理论的帮助下, 我们给出欧拉-拉格朗日方程. 

1) **from Newton to d'Almbert Principle** 
$$
\begin{align}
 & \vec{F} = m \ddot{ \vec{r}} \\
 & \vec{F} - m  \ddot{ \vec{r}}  = 0\\
 & \sum_{i=1}^{3} F_{i} - m \ddot{x}_{i} = 0 \\
 & \sum_{i=1}^{3} (F_{i}^{A} - m \ddot{x}_{i})\cdot \delta x_{i}=0 \\
\end{align}
$$
2) **utilitize multi variate calculus** 
$$
\begin{align}
 & \sum_{i=1}^{3} (F_{i}^{A} - m \ddot{x}_{i})\cdot \delta x_{i}=0 \\ \\
 &   \sum_{i=1}^{3}(F_{i}^{A} - m \ddot{x}_{i})\cdot \sum_{j=1}^{N} \frac{\partial x_{i}}{\partial q_{j}}\delta q_{j} \\
 &  =\sum_{i=1}^{3}\sum_{j=1}^{N}  (F_{i}^{A} - m \ddot{x}_{i}) \frac{\partial x_{i}}{\partial q_{j}} \delta q_{j} = 0 \tag{0} \\  
\end{align}
$$
3) **utilize the property of Apply Force:** z
$$
\begin{align}
F_{i}^{A} = - \frac{\partial}{\partial x_{i}} V(\vec{x}) = - \sum_{j=1}^{N} \frac{\partial}{\partial q_{j}} V(\vec{x}) \times \frac{\partial q_{j}}{\partial x_{i}}
\end{align}
$$

4) **[Several properties of Multi Variables Calculus:]** 

- for function $y = f(x,\text{others},t)$ and its counterpart $x = g(x, \text{others},t)$
$$
\begin{align}
\frac{ \partial y  }{ \partial  x} \times \frac{ \partial x }{ \partial y }  = 1   
\end{align}
$$
easy to prove

- time derivative $\frac{\mathrm{d}}{\mathrm{d}t}$ has below when $\vec{x} = \vec{x}(t), q_{j} = q_{j}(t)$ 
$$
\begin{align}
\frac{\mathrm{d}}{\mathrm{d}t } =  \frac{ \partial  }{ \partial t }  + \sum_{j=1}^{N}  \frac{ \partial  }{ \partial q_{j} }  \times \frac{ \mathrm{d} q_{j} }{\mathrm{d} t } 
\end{align}
$$

- when time and space(or params space) couples: 
$$
\begin{align}
\frac{ \partial \dot A  }{ \partial \dot B  } =\frac{ \partial \frac{\mathrm{d}}{\mathrm{d}t}A  }{ \partial \frac{\mathrm{d}}{\mathrm{d}t} B  }  = \frac{ \partial A }{ \partial B } 
\end{align}
$$
**Proof:** 
$$
\begin{align}
 & \frac{\mathrm{d}}{\mathrm{d}t} A = \frac{ \partial  }{ \partial t } A + [\frac{ \partial  A}{ \partial B } ] \frac{\mathrm{d}}{\mathrm{d}t}B +  \sum_{j=1}^{N} \frac{ \partial  }{ \partial q_{j} }   A \frac{\mathrm{d}}{\mathrm{d}t}q_{j}  \\
 & \text{then we have: } \frac{ \partial \frac{\mathrm{d}}{\mathrm{d}t}A  }{ \partial \frac{\mathrm{d}}{\mathrm{d}t}B  }  = \frac{ \partial \dot A  }{ \partial  \dot{B} } = \frac{ \partial A }{ \partial B }   
\end{align}
$$

apply these formulas into (0), we have 
Force part: 
$$
\begin{align}
 & \sum_{i=1}^{3}\sum_{j=1}^{N}  F_{i}^{A} \frac{ \partial x_{i}  }{ \partial q_{j} } \delta q_{j}  \\
  & \text{then:} \sum_{i=1}^{3}\sum_{j=1}^{N} F_{i}^{A} \frac{ \partial x_{i}  }{ \partial q_{j} } \delta  q_{j } = -\sum_{j=1}^{N} \sum_{i=1}^{3} \frac{ \partial V }{ \partial x_{i}  } \frac{ \partial x_{i} }{ \partial q_{j} } \delta q_{j}  \\
 & = -\sum_{j=1}^{N} \frac{ \partial V }{ \partial q_{j} } \delta q_{j}
\end{align}
$$ 
**[Kinetic part]:** 
$$
\begin{align}
 & \sum_{i=1}^{3}\sum_{j=1}^{N} m  \ddot{x}  \frac{ \partial x_{i} }{ \partial q_{j} } \delta q_{j}  \\
 & = \sum_{i=1}^{3}\sum_{j=1}^{N} m \frac{\mathrm{d}\dot{x}_{i}}{\mathrm{d}t} \frac{ \partial x_{i} }{ \partial q_{j} } \delta q_{j }  =  \\
 & \left[\frac{\mathrm{d}}{\mathrm{d}t} \left(  \sum_{i=1}^{3}\sum_{j=1}^{N} m  \dot{x}_{i} \times \frac{ \partial x_{i} }{ \partial q_{j} }   \right) - \sum_{i=1}^{3}\sum_{j=1}^{N} m \dot{x}_{i} \times \frac{\mathrm{d}}{\mathrm{d}t}\left( \frac{ \partial x_{i} }{ \partial q_{j} }   \right)  \right]\delta q_{j}   \\
 & = \left[   \frac{\mathrm{d}}{\mathrm{d}t} \sum_{i=1}^{3}\sum_{j=1}^{N} m \dot{x}_{i} \times \frac{ \partial \dot {x}_{i}  }{ \partial \dot{q}_{j} } - \sum_{i=1}^{3}\sum_{j=1}^{N} m \dot{x}_{i} \times \frac{ \partial  \dot{x} }{ \partial q_{j} }      \right] \delta q_{j}  \\
 & =\sum_{j=1}^{N} \left[\frac{\mathrm{d}}{\mathrm{d}t}  \frac{ \partial \left( \frac{1}{2}m {\dot{\vec{x}}}^{2} \right) }{ \partial \dot{q}_{j} }   - \frac{ \partial \left( \frac{1}{2}m {\dot{\vec{x}}}^{2} \right) }{ \partial q_{j}  } \right]  \delta q_{j}
\end{align}
$$ 
then combine them, we have: 
$$
\begin{align}
\sum_{j=1}^{N} \left[-\frac{ \partial V }{ \partial q_{j} }  -\frac{\mathrm{d}}{\mathrm{d}t}\frac{ \partial T }{ \partial \dot{q}_{j}  } +\frac{ \partial T }{ \partial q_{j} }    \right] \delta q_{j} = 0
\end{align}
$$
devide into $j$ dimensions: 
$$
\begin{align}
\frac{\mathrm{d}}{\mathrm{d}t}\frac{ \partial T }{ \partial \dot{q}_{j} }  - \frac{ \partial (T-V) }{ \partial q_{j} }  = 0 \\
\end{align}
$$
then let $L = T-V$, with $\frac{ \partial V }{ \partial \dot{ q }_{j}} = 0$ 
we have Euler Lagrange Equation: 
$$
\begin{align}
\frac{\mathrm{d}}{\mathrm{d}t} \frac{ \partial L }{\partial \dot{q}_{j} } - \frac{ \partial L }{ \partial q_{j} }  = 0 \tag{Euler Lagrange}  
\end{align}
$$

# From Euler Lagrange to Principle of Minimum Action and vice versa

Definition: 
$$
\begin{align}
S = \int_{t_{1};\text{path:}q(t) }^{t_{2}} \mathrm{d}t L(q,\dot{q},t)
\end{align}
$$
do variation: 
$$
\begin{align}
 \delta S  & = \int_{t_{1}}^{t_{2}} \mathrm{d}t L(q+\delta q,\dot{q} + \delta \dot{q}  ,t) - \int_{t_{1}}^{t_{2}} \mathrm{d}t L(q,\dot{q},t)  \\ 
 & = \int_{t_{1}}^{t_{2}} \mathrm{d}t \sum_{j=1}^{N} \left( \frac{ \partial  }{ \partial q_{j} } L(q,\dot{q},t) \delta q_{j} + \frac{ \partial  }{ \partial \dot{q}_{j}  }L(q,\dot{q},t) \delta \dot{q}   \right) \\
 & =  \int_{t_{1}}^{t_{2}} \mathrm{d}t \sum_{j=1}^{N} \left( \frac{ \partial  }{ \partial q_{j} } L(q,\dot{q},t) \delta q_{j} +\frac{\mathrm{d}}{\mathrm{d}t}\left(  \frac{ \partial  }{ \partial \dot{q}_{j}  }L(q,\dot{q},t) \delta  q_{j}  \right)  - \frac{\mathrm{d}}{\mathrm{d}t} \left( \frac{ \partial  }{ \partial \dot{q}_{j}  }L(q,\dot{q},t) \right) \delta q_{j}\right)  \\
 & =\int_{t_{1}}^{t_{2}} \mathrm{d}t \sum_{j=1}^{N}\frac{\mathrm{d}}{\mathrm{d}t}\left(  \frac{ \partial  }{ \partial \dot{q}_{j}  }L(q,\dot{q},t) \delta  q_{j}  \right) \\
 & + \int_{t_{1}}^{t_{2}} \mathrm{d}t \sum_{j=1}^{N}\left( \frac{ \partial  }{ \partial q_{j} } L(q,\dot{q},t) \delta q_{j}  - \frac{\mathrm{d}}{\mathrm{d}t} \left( \frac{ \partial  }{ \partial \dot{q}_{j}  }L(q,\dot{q},t) \right) \delta q_{j}\right) \\
 & \underset{q(t) \text{ ends fixed}}=0 +   \int_{t_{1}}^{t_{2}} \mathrm{d}t \sum_{j=1}^{N}\left( \frac{ \partial L(q,\dot{q},t)   }{ \partial q_{j} }  - \frac{\mathrm{d}}{\mathrm{d}t} \left( \frac{ \partial  L(q,\dot{q},t) }{ \partial \dot{q}_{j}  }\right) \right)\delta q_{j} 
\end{align}
$$
then we have 
$$
\begin{align}
\delta S = 0 \leftrightarrow \frac{ \partial L(q,\dot{q},t)   }{ \partial q_{j} }  - \frac{\mathrm{d}}{\mathrm{d}t} \left( \frac{ \partial  L(q,\dot{q},t) }{ \partial \dot{q}_{j}  }\right) = 0 
\end{align}
$$

# From Principle of Minimum Action to Hamiltonian Principle 

[Legendre transformation and Hamiltonian Principle](https://zhuanlan.zhihu.com/p/51903123)
first we have: 
$$
\begin{align}
S = \int_{\text{path:}q(t) } \mathrm{d}t L(q,\dot{q},t) 
\end{align}
$$
then we do **[Legendre Transformation]**: 
$$
\begin{align}
H(q,\dot{q},t) = \dot{q} \frac{ \partial L(q,\dot{q},t) }{ \partial \dot{q} }  - L(q,\dot{q},t) = \dot{q}\times p -L(q,\dot{q},t)
\end{align}
$$
then we find: 
$$
\begin{align} 
\mathrm{d}H  & = \mathrm{d}\dot{q}\frac{ \partial L }{ \partial \dot{q} }  + \mathrm{d}\left( \frac{ \partial L }{ \partial \dot{q} }  \right)\times \dot{q} - \mathrm{d}L \\
 & = \mathrm{d}\dot{q}\frac{ \partial L }{ \partial \dot{q} } -\frac{ \partial L }{ \partial q } \mathrm{d}q - \frac{ \partial L }{ \partial \dot{q} } \mathrm{d}\dot{q} +\dot{q}\times \mathrm{d}\left( \frac{ \partial L }{ \partial \dot{q} }  \right) -\frac{ \partial L }{ \partial t } \mathrm{d}t \\
 & =\mathrm{d}\dot{q}\times 0 + \dot{q}\mathrm{d}\left( \frac{ \partial L }{ \partial \dot{q} }  \right) - \frac{ \partial L }{ \partial  {q} } \mathrm{d} {q}-\frac{ \partial L }{ \partial t } \mathrm{d}t  \\
 & =\dot{q} \mathrm{d}\left( \frac{ \partial L }{ \partial \dot{q} }  \right) - \frac{ \partial L }{ \partial  {q} } \mathrm{d}q - \frac{ \partial L }{ \partial t } \mathrm{d}t
\end{align}
$$
note $p\equiv \frac{ \partial L }{ \partial \dot{q} }$, then we have: 
$$
\begin{align}
\mathrm{d}H   & = \dot{q}\mathrm{d}p -\frac{ \partial L }{ \partial q } \mathrm{d}q - \frac{ \partial L }{ \partial t } \mathrm{d}t \\
 & \underset{\frac{ \partial L }{ \partial q } =\frac{\mathrm{d}}{\mathrm{d}t}\left( \frac{ \partial L }{ \partial \dot{q} }  \right) }{\overset{\text{Euler Lagrange}}{=}} \dot{q}\mathrm{d}p - \frac{\mathrm{d}}{\mathrm{d}t}\frac{ \partial L }{ \partial \dot{q} } \mathrm{d}q -\frac{ \partial L }{ \partial t } \mathrm{d}t  \\
 & = \dot{q}\mathrm{d}p - \dot{p}\mathrm{d}q-\frac{ \partial L }{ \partial t } \mathrm{d}t \tag{Hamiltonian Principle}
\end{align}
$$
this also means **Hamiltionian Canonical Eqs**: 
$$
\begin{align}
\dot{q} & =\frac{ \partial H }{ \partial p }  \\
\dot{p}  & =-\frac{ \partial H }{ \partial \dot{q} } 
\end{align}
$$

# Canonical Transformation Principle of Minimal Action 

- [Canonical Transformation and H-J eq](https://zhuanlan.zhihu.com/p/85001265)

## Principle of Minimal Action under $q,p,t$ variables

$$
\begin{align}
S  & = \int_{\text{path:}q(t)} L(q,\dot{q},t)\mathrm{d}t = \int_{\text{path:}q(t)}(\dot{q}\times p-H(q,\dot{q},t))\mathrm{d}t  \\
 &\underset{q(t)\to q(t),p(t)}{\overset{\text{Path transformation}}{=}}\int_{\text{path}: q(t),p(t)}\mathrm{d}q\times p - H(q,p,t)\mathrm{d}t
\end{align}
$$
then we can see delta of $S$: 
$$
\begin{align}
\delta S  & = \delta \int_{\text{path}: q(t),p(t)} \mathrm{d}q\times p - H(q,p,t)\mathrm{d}t  \\
 & = \int_{\text{path:}q(t),p(t)} \delta \mathrm{d}q \times p + \delta p\times \mathrm{d}q - \delta H \mathrm{d}t \\
 & = \int_{\text{path:}q(t),p(t) } \delta \mathrm{d}q\times p+\delta p\times \mathrm{d}q - \frac{ \partial H }{ \partial q } \delta q\mathrm{d}t - \frac{ \partial H }{ \partial p } \delta p\mathrm{d}t \\
 &  = \int_{\dots} \mathrm{d}(\delta q\times p)-\delta q\mathrm{d}p + \delta p\times \mathrm{d}q - \frac{ \partial H }{ \partial q } \delta q\mathrm{d}t - \frac{ \partial H }{ \partial p } \delta p\mathrm{d}t  \\
 & =\int_{\dots}\mathrm{d}(\delta q\times p) + \delta q\times\left( -\mathrm{d}p-\frac{ \partial H }{ \partial q } \mathrm{d}t \right) + \delta p\times\left( \mathrm{d}q-\frac{ \partial H }{ \partial p } \mathrm{d}t \right) \\
 & \underset{q(t)\text{ ends fixed}, p(t) \text{ not needed}}=0  \\
 & +\int_{\text{path:}q(t),p(t)}\mathrm{d}t\times\left( \delta q\times\left( -\dot{p}-\frac{ \partial H }{ \partial q }  \right) + \delta p \times\left( \dot{q}-\frac{ \partial H }{ \partial p }  \right) \right)
\end{align}
$$
then if we have $\delta S = 0$, then we have **Hamiltionian Canonical Eqs**. 

## Canonical Transformation

first we have a $q,p,H$ version action and add a condition: [both varibale]$q,p$ [ends fixed] : 
$$
\begin{align}
S = \int_{\text{path: }q(t),p(t)}^ \text{[both variables ends fixed]}p\mathrm{d}q - H\mathrm{d}t 
\end{align}
$$
then if you add a **total differential**: 
$$
\begin{align}
S' = \int_{\dots}p\mathrm{d}q-H\mathrm{d}t + \mathrm{d}F
\end{align}
$$
then we calculate delta: 
$$
\begin{align}
\delta S  & = \dots \\
\delta S'  & = \delta S + F|^{q^{*},p^{*},t^{*}}_{q^{-},p^{-},t^{-}}
\end{align}
$$
which gives out same physics. then we can asume we have a **transformation**, $F$ could be a chain between the path. 
$$
\begin{align}
  Q &   = Q(q,p,t) \\
  P &  = P(q,p,t)\\
 \text{ends fixed path:}q(t),p(t) &  \to \text{ends fixed path:}Q(t),P(t)
\end{align}
$$
we assume: 
$$
\begin{align}
p\mathrm{d}q-H\mathrm{d}t + \mathrm{d}F = P\mathrm{d}Q - K\mathrm{d}t
\end{align}
$$
let $F = F(q,Q,t)$
$$
\begin{align}
\mathrm{d}F  & = \frac{ \partial F  }{ \partial q  }\mathrm{d}q + \frac{ \partial F }{ \partial Q } \mathrm{d}Q + \frac{ \partial F }{ \partial t } \mathrm{d}t \\
\mathrm{d}q \text{ term:} & \mathrm{d}q\times\left( p+\frac{ \partial F }{ \partial q }  \right) = 0 \\
\mathrm{d}Q \text{ term:} & \mathrm{d}Q\times\left( \frac{ \partial F }{ \partial Q }  \right) = \mathrm{d}Q\times P \\
\mathrm{d}t \text{term:}  & \mathrm{d}t\times\left( -H + \frac{ \partial F }{ \partial t }\right)  = \mathrm{d}t \times(-K) \\
\end{align}
$$
others: 
$$
\begin{align}
F = F(q,P,t)\dots \\
F = F(p,Q,t)  \dots\\
F = F(q,Q,t)\dots \\
\end{align}
$$

## Hamiltion - Jacobian Equation

let $F$ be $S$, in new coordinates side: 
$$
\begin{align}
S  & = \int_{\text{path},q^{*},p^{*},t}p\mathrm{d}q - H\mathrm{d}t  \\
\mathrm{d}S &  = p\mathrm{d}q - H\mathrm{d}t = \frac{ \partial S }{ \partial q } \mathrm{d}q + \frac{ \partial S }{ \partial p } \mathrm{d}p  - \frac{ \partial S }{ \partial t } \mathrm{d}t\\
  \text{then the canonical relation: } &  p\mathrm{d}q - H\mathrm{d}t = \mathbf{0} + \mathrm{d}S\\  
\end{align}
$$
then we have [**Hamiltonian Jacobian Eq**]: 
$$
\begin{align}
 & \frac{ \partial S(q^{*},p^{*},t) }{ \partial t } + H(q^{*},p^{*},t)  = 0  \\
 & \frac{ \partial S }{ \partial q }    = p\\
 & \frac{ \partial S }{ \partial p }  = 0
\end{align}
$$
then we have: 
$$
\begin{align}
\frac{ \partial S\left( q,\frac{ \partial S }{ \partial q } ,t \right) }{ \partial  t} + H\left( q,\frac{ \partial S }{ \partial q } ,t \right) = 0
\end{align}
$$

### Solving the System with the HJ Equation

Solving the Hamilton-Jacobi equation means finding a "complete integral," which is a solution that contains n independent constants of integration, say $P_1​,P_2​,...,P_n$​. These constants are the new, constant momenta.

1. **Solve the PDE**: Find the function $S(q_1​,...,q_n​,P_1​,...,P_n​,t)$ that satisfies the HJ equation.
    
2. **Find the trajectory**: The new constant positions $Q_k​$ are found by differentiating the solution S with respect to the new momenta $P_k​\text{:   } \  Q_k​=\frac{​∂S}{∂P_k​}=$constant
    
3. **Invert to find the motion**: These n equations relate the old coordinates qk​ to time and the constants Pk​ and $Q_k​$. Inverting these equations gives the full trajectory $q_k​(t)$ and $p_k​(t)$.

This method is incredibly powerful because it replaces the task of **solving 2n coupled first-order ordinary differential equations (Hamilton's equations)** with solving **a single first-order partial differential equation**. It is especially useful for systems where the variables can be separated. 

# Symplectic(辛) Algebra in Hamiltonian Canonical Eqs

first we rewrite Hamiltonian Canonical Eqs with Symplectic Algebra
$$
\begin{align}
\mathcal J  &  = \left[ \begin{array}{cccccccccc}  \mathbf0& \mathbf{1} \\ - \mathbf{1}&  \mathbf{0}\end{array} \right]  \\
\xi &  = \left[ \begin{array}{cccccccccc} q   \\ p \end{array} \right]  
\end{align}
$$
then we have Hamiltonian Canonical Eq:
$$
\begin{align}
\dot{\xi}=\mathcal{J} \frac{ \partial H }{ \partial \xi } 
\end{align}
$$
if we have some **Transformation**:
$$
\begin{align}
\mathbf{M}  & = \frac{ \partial \xi }{ \partial \eta }  \\
% \mathbf{M}^{-1}  & = \frac{ \partial \eta }{ \partial \xi } 
\end{align}
$$
then we have: 
$$
\begin{align}
\dot{\xi} = \frac{ \partial \xi }{ \partial \eta } \dot{\eta} \\
\frac{ \partial H }{ \partial \xi }  \overset{\star \star \star}= \left( \frac{ \partial \eta }{ \partial \xi } \right)^T \frac{ \partial H }{ \partial \eta } 
\end{align}
$$
then do left side Transformation to above 2 eqs: 
$$
\begin{align}
  \frac{ \partial \eta }{ \partial \xi }  \dot{\xi}  & = \dot{\eta} \tag{left side transformation}\\
  \frac{ \partial \eta }{ \partial \xi } \mathcal{J}\left( \frac{ \partial \eta }{ \partial \xi } \right)^{T} \frac{ \partial H }{ \partial \eta}    &  = \left( \frac{ \partial \eta }{ \partial \xi }\mathcal{J}\left( \frac{ \partial \eta }{ \partial \xi } \right)^T   \right) \frac{ \partial H }{ \partial \eta }  \tag{left side transformation}
\end{align}
$$
if we have $\mathbf{M}$ as a **canonical transformation**: 
$$
\begin{align}
 \frac{ \partial \eta }{ \partial \xi }\mathcal{J}\left( \frac{ \partial \eta }{ \partial \xi } \right)^T     = \mathcal{J}
\end{align}
$$
then: 
$$
\begin{align}
\dot{\eta} = \mathcal{J}\frac{ \partial H }{ \partial \eta } 
\end{align}
$$ 

# Possion Bracket

assume we have 2 variables: $u = u(q,p,t),v=v(q,p,t)$, then define a bracket: 
$$
\begin{align}
\{ u,v \}_{q,p} \equiv \frac{ \partial u }{ \partial q } \frac{ \partial v }{ \partial p } -\frac{ \partial u }{ \partial p } \frac{ \partial v }{ \partial q } 
\end{align}
$$
 [possion bracket](https://www.zhihu.com/question/52691484/answer/131650955?share_code=1bwNhnuToh2FN&utm_psn=1947369134896686566) 