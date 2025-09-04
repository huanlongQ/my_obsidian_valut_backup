# Tensor or Vector Analysis 

$$
\begin{align}
\epsilon_{ijk}A_{i}B_{j} = C_{k} \iff \vec{A}\times \vec{B} = \vec{C} \\
\end{align}
$$
$$
\begin{align}
\epsilon_{kij}\epsilon_{klm} = \delta_{il}\delta_{jm} - \delta_{im}\delta_{jl}
\end{align}
$$
$$
\begin{align}
\nabla (\vec{A}\cdot \vec{B}) &  = (\vec{A}\cdot \nabla )\vec{B}  + \vec{A}\times(\nabla \times \vec{B}  ) + (\vec{B}\cdot \nabla)\vec{A}  + \vec{B}\times(\nabla \times \vec{A}) \\
\vec{A}\times(\vec{B}\times \vec{C}) &  = (\vec{A}\cdot \vec{C} )\vec{B} - (\vec{A}\cdot \vec{B})\vec{C}
\end{align}
$$
$$
\begin{align}  
\nabla \frac{1}{r}  & = -\frac{\hat{r}}{r^{2}} \\
\nabla^{2} \frac{1}{r}  & = -4\pi \delta(\vec{r})  \\
 \nabla \times(\nabla \times \vec{A})  & = \nabla(\nabla \cdot \vec{A}) - (\nabla \cdot \nabla )\vec{A} = \nabla(\nabla \cdot \vec{A}) - \nabla^{2}\vec{A}
\end{align}
$$

$$
\begin{align}
\left[ \begin{array}{cccccccccc}  / & h_{1} & h_{2} & h_{3} \\ \text{Cartesian} & x\to1 & y\to1 & z\to1   \\ \text{Cylindrical} & \rho \to1 & \phi \to\rho & z\to 1 \\ \text{Spherical} &r\to 1   & \theta \to r & \phi \to r\sin \theta  \end{array} \right]  
\end{align}
$$

$$
\begin{align}
\text{grad: } \nabla \phi  & \iff \hat{e}_{i} \frac{1}{h_{i}}\frac{ \partial \phi }{ \partial x_{i} }  \\
\text{div: } \nabla \cdot \vec{A} & \iff \frac{1}{h_{1}h_{2}h_{3}} \hat{e}_{i}\frac{ \partial  }{ \partial x_{i} } (A_{i}h_{j}h_{k}) \\
\text{curl: } \nabla \times \vec{A} & \iff \frac{1}{h_{1}h_{2}h_{3}} h_{k}\hat{e}_{k}\epsilon_{ijk}\frac{ \partial  }{ \partial x_{i} } (h_{j}A_{j})
\end{align}
$$
-  [Del in cylindrical and spherical coordinates - Wikipedia](https://en.wikipedia.org/wiki/Del_in_cylindrical_and_spherical_coordinates) 
$$
\begin{align}
 & \text{for Cylindrical Coordinates: } \\
\nabla \varphi &  = \hat{\rho} \frac{ \partial \varphi }{ \partial \rho }  + \hat{\theta} \frac{1}{\rho} \frac{ \partial \varphi }{ \partial \theta } + \hat{z}\frac{ \partial \varphi }{ \partial z }  \\
\nabla \cdot \vec{A} & = \frac{1}{\rho}\frac{ \partial (\rho A_\rho) }{ \partial \rho } + \frac{1}{\rho}\frac{ \partial A_{\phi} }{ \partial \phi } + \frac{ \partial A_{z} }{ \partial z }  \\
\nabla^{2}\varphi  & = \frac{1}{\rho} \frac{ \partial  }{ \partial \rho } \left( \rho \frac{ \partial \varphi }{ \partial \rho }  \right) + \frac{1}{\rho^{2}}\frac{ \partial^{2} \varphi }{ \partial \phi^{2} } + \frac{ \partial^{2} \varphi }{ \partial z^{2} } 
\end{align}
$$
$$
\begin{align}
 & \text{for Spherical Coordinates:} \\
 \nabla \varphi & = \hat{r}\frac{ \partial \varphi }{ \partial r }+ \frac{1}{r}\frac{ \partial \varphi }{ \partial \theta }  +\frac{1}{r\sin \theta}\frac{ \partial \varphi }{ \partial \phi }   \\
\nabla \cdot \vec{A} & = \frac{1}{r^{2}}\frac{ \partial (r^{2}{A}_{r}) }{ \partial r } + \frac{1}{r\sin \theta}\frac{ \partial (A_{\theta}\sin \theta) }{ \partial \theta } + \frac{1}{r\sin \theta}\frac{ \partial A_\phi }{ \partial \phi } \\
\nabla^{2}\varphi  & = \frac{1}{r^{2}}\frac{ \partial  }{ \partial r } \left( r^{2}\frac{ \partial \varphi }{ \partial r }  \right) + \frac{1}{r^{2}\sin\theta}\frac{ \partial  }{ \partial \theta } \left( \sin \theta \frac{ \partial \varphi }{ \partial \theta  }  \right) + \frac{1}{r^{2}\sin ^{2}\theta}\frac{ \partial^{2}\varphi }{ \partial \phi^{2} } 
\end{align}
$$
- [Spherical harmonics - Wikipedia](https://en.wikipedia.org/wiki/Spherical_harmonics) 
$$
\begin{align}
L & =\vec{r}\times \vec{p} \iff \hat{L}=\vec{r}\times(-i\hbar \nabla)  = \hbar \hat{l}\\
\hat{l}^{2}  & = -\left( \frac{1}{\sin \theta}\frac{ \partial  }{ \partial \theta } \left( \sin \theta \frac{ \partial  }{ \partial \theta }  \right) + \frac{1}{\sin ^{2}\theta}\frac{ \partial^{2}  }{ \partial \phi^{2} }  \right)  \tag{eigenvalue: $l(l+1)$}\\
\nabla^{2} &  = \frac{1}{r^{2}}\frac{ \partial  }{ \partial r } \left( r^{2}\frac{ \partial  }{ \partial r }  \right) - \frac{\hat{l}^{2}}{r^{2}}
\end{align}
$$

# Electrodynamics

$$
\begin{align}
\text{Maxwell Eqs: }\begin{cases}
\nabla \cdot \vec{E} & = \frac{\rho}{\epsilon_{0}}  & \iff  \oint_{  \partial V}\vec{E}\cdot \mathrm{d}\vec{S} &  = \frac{1}{\epsilon_{0}}\int_{V}\rho \mathrm{d}V\\
\nabla \times \vec{E} & = -\frac{ \partial \vec{B} }{ \partial t } & \iff    \oint_{L}\vec{E}\cdot \mathrm{d}\vec{l}  &=\int_{S}-\frac{ \partial \vec{B} }{ \partial t } \mathrm{d}\cdot\vec{S} \\
\nabla \cdot \vec{B} & = 0  & \iff \oint_{  \partial V }\vec{B}\cdot \mathrm{d}\vec{S} & =0\\
\nabla \times \vec{B} & = \mu_{0}\vec{j} + \mu_{0}\epsilon_{0}\frac{ \partial \vec{E} }{ \partial t }  & \iff \oint_{L}\vec{B}\cdot \mathrm{d}\vec{l} & =\mu_{0}\int_{S}(\vec{j} + \epsilon_{0}\frac{ \partial \vec{E} }{ \partial t } )\mathrm{d}\vec{S}
\end{cases}
\end{align}
$$
$$
\begin{align}
\text{Electron Conservation Law:} \oint_{  \partial V } \vec{j} \cdot \mathrm{d}\vec{S} + \int_{V} \frac{ \partial \rho }{ \partial t } \mathrm{d}V = 0
\end{align}
$$
$$
\begin{align}
\begin{cases}
\vec{E}  & = -\nabla \varphi - \frac{ \partial \vec{A} }{ \partial t }  \\
\vec{B} &  = \nabla \times \vec{A} 
\end{cases}\tag{potential formula}
\end{align}
$$

## EM wave

- Vaccum Maxwell Eqs: 
$$
\begin{align}
\begin{cases}
\nabla \cdot \vec{E} & = 0 \\
\nabla \times \vec{E} & = -\frac{ \partial \vec{B} }{ \partial t }  \\
\nabla \cdot \vec{B} & = 0 \\
\nabla \times \vec{B} & = 0+\mu_{0}\epsilon_{0}\frac{ \partial \vec{E} }{ \partial t } 
\end{cases}
\end{align}
$$
$$
\begin{align}
\nabla \times(\nabla \times \vec{E}) &  = \nabla(\nabla \cdot \vec{E}) - \nabla^{2}\vec{E}  \\
\nabla \times(\nabla \times \vec{B}) &  = \nabla(\nabla \cdot \vec{B}) - \nabla^{2}\vec{B}  \\
\nabla \times\left( -\frac{ \partial B }{ \partial t }  \right)  & = -\frac{ \partial  }{ \partial t } (\nabla \times \vec{B})   = -\frac{ \partial  }{ \partial t } \left( \mu_{0}\epsilon_{0}\frac{ \partial \vec{E} }{ \partial t } \right)  \\
\nabla \times\left( \mu_{0}\epsilon_{0}  \frac{ \partial \vec{E} }{ \partial t }   \right)  & = \mu_{0}\epsilon_{0} \frac{ \partial  }{ \partial t } (\nabla \times \vec{E}) = -\mu_{0}\epsilon_{0}\frac{ \partial^{2}\vec{B} }{ \partial t^{2} }  \\
 & \left(  \mu_{0}\epsilon_{0}\frac{ \partial^{2} }{ \partial t^{2} }  - \nabla^{2} \right)\vec{E} = 0 \\
 & \left(  \mu_{0}\epsilon_{0}\frac{ \partial^{2} }{ \partial t^{2} }  - \nabla^{2} \right)\vec{B} = 0
\end{align}
$$
then we have $U \sim (\vec{E} ,\vec{B})$
$$
\begin{align}
 & \left(  \mu_{0}\epsilon_{0}\frac{ \partial^{2} }{ \partial t^{2} }  - \nabla^{2} \right){U}=0\\
 & \text{let: } U \sim \exp(i(\vec{k}\cdot \vec{r}-\omega t)) \\
 & \text{then: } (\mu_{0}\epsilon_{0}\times(-\omega^{2}) - (-\vec{k}^{2}) )U = 0 \\
 & \frac{\omega}{|\vec{k}|} = \frac{1}{\sqrt{ \mu_{0}\epsilon_{0}}}
\end{align}
$$

- Maxwell Eqs with sources. 
$$
 
\begin{align}
\text{Maxwell Eqs: }\begin{cases}
\nabla \cdot \vec{E} & = \frac{\rho}{\epsilon_{0}}  & \iff  \oint_{  \partial V}\vec{E}\cdot \mathrm{d}\vec{S} &  = \frac{1}{\epsilon_{0}}\int_{V}\rho \mathrm{d}V\\
\nabla \times \vec{E} & = -\frac{ \partial \vec{B} }{ \partial t } & \iff    \oint_{L}\vec{E}\cdot \mathrm{d}\vec{l}  &=\int_{S}-\frac{ \partial \vec{B} }{ \partial t } \mathrm{d}\cdot\vec{S} \\
\nabla \cdot \vec{B} & = 0  & \iff \oint_{  \partial V }\vec{B}\cdot \mathrm{d}\vec{S} & =0\\
\nabla \times \vec{B} & = \mu_{0}\vec{j} + \mu_{0}\epsilon_{0}\frac{ \partial \vec{E} }{ \partial t }  & \iff \oint_{L}\vec{B}\cdot \mathrm{d}\vec{l} & =\mu_{0}\int_{S}(\vec{j} + \epsilon_{0}\frac{ \partial \vec{E} }{ \partial t } )\mathrm{d}\vec{S}
\end{cases}
\end{align} 
$$
...
apply **Gauge Formulas**: 
$$
\begin{align}
 & \begin{cases}
\nabla \cdot\left( -\nabla \phi - \frac{ \partial \vec{A} }{ \partial t }  \right)  &  = -\nabla^{2}\phi - \frac{ \partial  }{ \partial t } (\nabla \cdot \vec{A})& = \frac{\rho}{\epsilon_{0}} \\
\nabla \times\left(  -\nabla \phi - \frac{ \partial \vec{A} }{ \partial t }   \right)   & =0-  \frac{ \partial  }{ \partial t } (\nabla \times \vec{A}) & = -\frac{ \partial (\nabla \times \vec{A}) }{ \partial t }  \\
\nabla \cdot(\nabla \times \vec{A}) &  = 0 & =0 \\
 \nabla \times(\nabla \times \vec{A}) & =\nabla(\nabla \cdot \vec{A})-\nabla^{2}\vec{A}  & =\mu_{0}\vec{j} +\mu_{0}\epsilon_{0}  \frac{ \partial \left(  -\nabla \phi - \frac{ \partial \vec{A} }{ \partial t }  \right) }{ \partial t }  
\end{cases}
 \\ \\
 & \text{then: }\begin{cases}
-\nabla^{2}\phi - \frac{ \partial  }{ \partial t } (\nabla \cdot \vec{A})& = \frac{\rho}{\epsilon_{0}}  \\
\nabla(\nabla \cdot \vec{A})-\nabla^{2}\vec{A} & =\mu_{0}\vec{j} +\mu_{0}\epsilon_{0}  \frac{ \partial \left(  -\nabla \phi - \frac{ \partial \vec{A} }{ \partial t }  \right) }{ \partial t }  
\end{cases} \\
 & \text{let Lorentz Gauge: }\frac{ \partial  }{ \partial t } \phi + \nabla \cdot \vec{A}  =0 \\
 & \text{then: }\begin{cases}
\frac{ \partial^{2} }{ \partial t^{2} } \phi - \nabla^{2}\phi  & = \frac{\rho}{\epsilon_{0}} \\
\frac{ \partial^{2} }{ \partial t^{2} } \vec{A}-\nabla^{2}\vec{A} & = \mu_{0}\vec{j}
\end{cases} \\
 & \text{AKA:}   \partial_{\mu}A^{\mu} = \mu_{0}J^{\mu } \text{ where: }J^{\mu} = \left[ \begin{array}{cccccccccc} c\rho   \\ j_{x} \\ j_{y} \\ j_{z} \end{array} \right]  , A^{\mu}=\left[ \begin{array}{cccccccccc}   \frac{\phi}{c} \\ A_{x} \\ A_{y} \\A_{z}  \end{array} \right]  
\end{align}
$$ 
we can solve these wave eqs with **Green Func Method**. 

$\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}$ ???why no outline???

# Symmetry in Maxwell Eqs (Narrow Relativitistic Electrodynamics and Gauge Symmetry)

- [Narrow Relativitistic Electiodynamics](https://zhuanlan.zhihu.com/p/29540507240?share_code=ETFJ05NDBFqJ&utm_psn=1946943152301772846) 
- [same as above](https://zhuanlan.zhihu.com/p/174833787?share_code=q0D2yegRqo28&utm_psn=1946943543647113471) 
- [same](https://zhuanlan.zhihu.com/p/602635631?share_code=12J6ULnryqYck&utm_psn=1946957131862509123) 

## Lorentz covariance

# Static Electromagnetism
