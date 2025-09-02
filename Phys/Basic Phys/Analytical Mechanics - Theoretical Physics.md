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
 & =\sum_{j=1}^{N} \left[\frac{\mathrm{d}}{\mathrm{d}t}  \frac{ \partial \left( \frac{1}{2}m {\dot{\vec{x}}}^{2} \right) }{ \partial \dot{q}_{j} }   - \frac{ \partial \left( \frac{1}{2}m {\dot{\vec{x}}}^{2} \right) }{ \partial q_{j}  } \right]  
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
S = \int_{t_{1}}^{t_{2}} \mathrm{d}t L(q,\dot{q},t)
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
 & =0 +   \int_{t_{1}}^{t_{2}} \mathrm{d}t \sum_{j=1}^{N}\left( \frac{ \partial L(q,\dot{q},t)   }{ \partial q_{j} }  - \frac{\mathrm{d}}{\mathrm{d}t} \left( \frac{ \partial  L(q,\dot{q},t) }{ \partial \dot{q}_{j}  }\right) \right)\delta q_{j} 
\end{align}
$$
then we have 
$$
\begin{align}
\delta S = 0 \leftrightarrow \frac{ \partial L(q,\dot{q},t)   }{ \partial q_{j} }  - \frac{\mathrm{d}}{\mathrm{d}t} \left( \frac{ \partial  L(q,\dot{q},t) }{ \partial \dot{q}_{j}  }\right) = 0 
\end{align}
$$

# From Principle of Minimum Action to Hamiltonian Principle
