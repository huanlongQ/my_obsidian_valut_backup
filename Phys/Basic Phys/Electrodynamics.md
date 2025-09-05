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
-  [Del in cylindrical and spherical coordinates - Wikipedia](https://en.wikipedia.org/wiki/Del_in_cylindrical_and_spherical_coordinates) ⭐
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
\nabla^{2}\varphi  & = \frac{1}{r^{2}}\frac{ \partial  }{ \partial r } \left( r^{2}\frac{ \partial \varphi }{ \partial r }  \right) + \frac{1}{r^{2}\sin\theta}\frac{ \partial  }{ \partial \theta } \left( \sin \theta \frac{ \partial \varphi }{ \partial \theta  }  \right) + \frac{1}{r^{2}\sin ^{2}\theta}\frac{ \partial^{2}\varphi }{ \partial \phi^{2} }  \\
 & =\underline{\underline{\underline{\frac{1}{r}  \frac{ \partial^{2} }{ \partial r^{2} } (r\varphi)}}}  + \dots 
\end{align}
$$
- [Spherical harmonics - Wikipedia](https://en.wikipedia.org/wiki/Spherical_harmonics) ⭐
$$
\begin{align}
L & =\vec{r}\times \vec{p} \iff \hat{L}=\vec{r}\times(-i\hbar \nabla)  = \hbar \hat{l}\\
\hat{l}^{2}  & = -\left( \frac{1}{\sin \theta}\frac{ \partial  }{ \partial \theta } \left( \sin \theta \frac{ \partial  }{ \partial \theta }  \right) + \frac{1}{\sin ^{2}\theta}\frac{ \partial^{2}  }{ \partial \phi^{2} }  \right)  \tag{eigenvalue: $l(l+1)$}\\
\nabla^{2} &  = \frac{1}{r^{2}}\frac{ \partial  }{ \partial r } \left( r^{2}\frac{ \partial  }{ \partial r }  \right) - \frac{\hat{l}^{2}}{r^{2}} = \underline{\underline{\underline{    \frac{1}{r}  \frac{ \partial^{2} }{ \partial r^{2} } (r\cdot) - \frac{\hat{l}^{2}}{r^{2}} \cdot  }}} 
\end{align}
$$

# General Electrodynamics

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
\text{Electron Conservation Law:} \oint_{  \partial V } \vec{j} \cdot \mathrm{d}\vec{S} + \int_{V} \frac{ \partial \rho }{ \partial t } \mathrm{d}V = 0 \iff \nabla \cdot \vec{j} + \frac{ \partial \rho }{ \partial t } =0
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
$$
\begin{align}
\text{EM Force:} \begin{cases}
\vec{F} & =q\vec{E}+q\vec{v}\times \vec{B} \\
\vec{f} & =\rho \vec{E}+\vec{j}\times \vec{B}
\end{cases}
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
-\nabla^{2}\phi - \frac{ \partial  }{ \partial t } (\underline{\underline{\underline{\nabla \cdot \vec{A}}}})& = \frac{\rho}{\epsilon_{0}}  \\
\nabla(\underline{\underline{\underline{\nabla \cdot \vec{A}}}})-\nabla^{2}\vec{A} & =\mu_{0}\vec{j} +\mu_{0}\epsilon_{0}  \frac{ \partial \left(  \underline{\underline{\underline{-\nabla \phi}}} - \frac{ \partial \vec{A} }{ \partial t }  \right) }{ \partial t }  
\end{cases} \\
 & \text{let Lorentz Gauge: }\frac{ \partial  }{ \partial t } \phi + \nabla \cdot \vec{A}  =0 \\
 & \text{then: }\begin{cases}
\frac{1}{c^{2}}\frac{ \partial^{2} }{ \partial t^{2} } \phi - \nabla^{2}\phi  & = \frac{\rho}{\epsilon_{0}} \\
\frac{1}{c^{2}}\frac{ \partial^{2} }{ \partial t^{2} } \vec{A}-\nabla^{2}\vec{A} & = \mu_{0}\vec{j}
\end{cases} \\
 & \text{AKA:}     \partial^{\nu} \partial_{\nu}A^{\mu} = \mu_{0}J^{\mu } \text{ where: }J^{\mu} = \left[ \begin{array}{cccccccccc} c\rho   \\ j_{x} \\ j_{y} \\ j_{z} \end{array} \right]  , A^{\mu}=\left[ \begin{array}{cccccccccc}   \frac{\phi}{c} \\ A_{x} \\ A_{y} \\A_{z}  \end{array} \right]  
\end{align}
$$ 
we can solve these wave eqs with **Green Func Method**. in next - we introduce it. 

$\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}\frac{\mathrm{d}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}}{\mathrm{d}}$ ???why no outline???

- **Green Func Method in EM wave**: 
$$
\begin{align}
 & \text{under Lorentz Gauge: }\frac{ \partial  }{ \partial t } \phi + \nabla \cdot \vec{A}  =0 \\
 & \text{then: }\begin{cases}
\frac{1}{c^{2}}\frac{ \partial^{2} }{ \partial t^{2} } \phi - \nabla^{2}\phi  & = \frac{\rho}{\epsilon_{0}} \\
\frac{1}{c^{2}}\frac{ \partial^{2} }{ \partial t^{2} } \vec{A}-\nabla^{2}\vec{A} & = \mu_{0}\vec{j}
\end{cases} \\
\end{align}
$$
let $\psi \sim \left(  {\phi} ,\vec{A} \right),4\pi f\sim\left( \frac{\rho}{\epsilon_{0}},\mu_{0}\vec{j} \right)$ 
then: 
$$
\begin{align}
\frac{1}{c^{2}}\frac{ \partial^{2} }{ \partial t^{2} } \psi(\vec{r},t) - \nabla^{2}\psi (\vec{r},t) & = -4\pi f(\vec{r},t)
\end{align}
$$
do time domain **Fourier Transformation**:
$$
\begin{align}
 & \begin{cases}
\psi(\vec{r},t) \to \psi(\vec{r},\omega) = \int \psi(\vec{r},t)\exp(\underline{\underline{\underline{ +i }}}\omega t)\mathrm{d}t \\
f(\vec{r},t) \to f(\vec{r},\omega) = \int f(\vec{r},t)\exp(\underline{\underline{\underline{ +i }}}\omega t)\mathrm{d}t 
\end{cases}\tag{+{i} match phase formula}\\
 & \begin{cases}
\psi(\vec{r},t ) = \frac{1}{2\pi}\int \psi(\vec{r},\omega )\exp( \underline{\underline{\underline{ -i }}}\omega t)\mathrm{d}t \\
f(\vec{r},t ) = \frac{1}{2\pi}\int f(\vec{r},\omega )\exp(\underline{\underline{\underline{ -i }}}\omega t)\mathrm{d}t
\end{cases}\tag{- i match phase formula}
\end{align}
$$
then we have the PDE: 
$$
\begin{align}
\left(\nabla^{2} - \left( \frac{i\omega}{c} \right)^{2}\right)\psi(\vec{r},\omega) = -4\pi f(\vec{r},\omega )
\end{align}
$$
then $\delta$ func introduced: 
$$
\begin{align}
\left(\nabla^{2} + \left( \frac{\omega}{c} \right)^{2}\right)g_{\omega}(\vec{r},\vec{\xi}) = -4\pi \delta(\vec{r}-\vec{\xi})
\end{align}
$$
its solution is 
$$
\begin{align}
g_{\omega}(\vec{r},\vec{\xi}) = A \times\frac{\exp{\left( + i \frac{\omega}{c} |\vec{r}-\vec{\xi}| \right)}}{|\vec{r}-\vec{\xi}|} + B\times\frac{\exp{\left( - i \frac{\omega}{c} |\vec{r}-\vec{\xi}| \right)}}{|\vec{r}-\vec{\xi}|}, (A+B = 1)
\end{align}
$$
then **Fourier Transformation**: 
$$
\begin{align}
g(\vec{r},\xi,t) = \frac{1}{2\pi}\int \mathrm{d}\omega g_{\omega}(\vec{r},\vec{\xi})\exp(i\omega t)
\end{align}
$$
we want to find a $g$ green func that can match the time $\delta$ func, then we introduce: 
$$
\begin{align}
g(\vec{r},\vec{\xi},t,\tau ) & = \frac{1}{2\pi}\int \mathrm{d}\omega g_{\omega}(\vec{r},\vec{\xi})\exp(-i\omega|t-\tau|) \\
  & = \frac{1}{2\pi}\int \mathrm{d} \omega \left( A \times\frac{\exp{\left( + i \frac{\omega}{c} |\vec{r}-\vec{\xi}| \right)}}{|\vec{r}-\vec{\xi}|} + B\times\frac{\exp{\left( - i \frac{\omega}{c} |\vec{r}-\vec{\xi}| \right)}}{|\vec{r}-\vec{\xi}|} \right)\times \exp(-\underline{\underline{\underline{ i }}}\omega|t-\tau|) \\
 & = A\times \frac{\delta(t-\tau-\frac{|\vec{r}-\vec{\xi}|}{ c })}{|\vec{r}-\vec{\xi}|} + B\times \frac{\delta(t-\tau+\frac{|\vec{r}-\vec{\xi}|}{ c })}{|\vec{r}-\vec{\xi}|} , (A = 1 , B = 0 \text{ if delay potential})
\end{align}
$$
 then we have: 
 
$$
\begin{align}
\psi(\vec{r},t) & = \frac{1}{4\pi} \int \mathrm{d}^{3}\vec{\xi}\mathrm{d}\tau g(\vec{r},\vec{\xi},t,\tau )\times f(\vec{\xi},\tau) \\
 & = \frac{1}{4\pi}\int \mathrm{d}^{3}\vec{\xi}\mathrm{d}\tau \frac{\delta\left( t-\tau-\frac{|\vec{r}-\vec{\xi}|}{c} \right)}{|\vec{r}-\vec{\xi}|}\times f(\vec{\xi},\tau) \\
 & =\frac{1}{4\pi}\int \mathrm{d}^{3}\vec{\xi} \frac{f\left( \vec{\xi},t-\frac{|\vec{r}-\vec{\xi}|}{c} \right)}{|\vec{r}-\vec{\xi}|} \\

 & \begin{cases}
\phi(\vec{r},t) & = \frac{1}{4\pi \epsilon_{0}} & \int \mathrm{d}^{3}\vec{\xi} \frac{\rho\left( \vec{\xi},t-\frac{|\vec{r}-\vec{\xi}|}{c} \right)}{|\vec{r}-\vec{\xi}|} \\
\vec{A}(\vec{r},t) & = \frac{\mu_{0}}{4\pi} & \int \mathrm{d}^{3}\vec{\xi} \frac{\vec{j}\left( \vec{\xi},t-\frac{|\vec{r}-\vec{\xi}|}{c} \right)}{|\vec{r}-\vec{\xi}|}
\end{cases} \text{ (this match static potential)}
\end{align}
$$

## EM radiation

follow the **Green Func Method** in EM wave, we conclude that: 
$$
\begin{align}
 & \begin{cases}
\phi(\vec{r},t) & = \frac{1}{4\pi \epsilon_{0}} & \int \mathrm{d}^{3}\vec{\xi} \frac{\rho\left( \vec{\xi},t-\frac{|\vec{r}-\vec{\xi}|}{c} \right)}{|\vec{r}-\vec{\xi}|} \\
\vec{A}(\vec{r},t) & = \frac{\mu_{0}}{4\pi} & \int \mathrm{d}^{3}\vec{\xi} \frac{\vec{j}\left( \vec{\xi},t-\frac{|\vec{r}-\vec{\xi}|}{c} \right)}{|\vec{r}-\vec{\xi}|}
\end{cases} \text{ (which match static potential)}
\end{align}
$$
futher, we do approximation for different kind of field condition:
$$
\begin{align}
 \text{field condition:}& \begin{cases}
\text{far field: } & \vec{r}\gg \frac{c}{\omega } \\
\text{medium field:} & \vec{r} \sim \frac{c}{\omega} \\
\text{near field:} & \vec{r} \ll \frac{c}{\omega}
\end{cases} \\

  \text{far field approximation:} & \begin{cases}
\frac{1}{|\vec{r}-\vec{\xi}|} & = \frac{1}{|\vec{r}|} + (-\vec{\xi})\cdot \nabla \frac{1}{|\vec{r}|} + ((-\vec{\xi})\cdot \nabla)^{2} \frac{1}{|\vec{r}|} + \dots & \sim\frac{{1}}{|r|}\\
\frac{\omega}{c}|\vec{r}-\vec{\xi} | & = \frac{\omega}{c}\times(|\vec{r}| + (-\vec{\xi})\cdot \nabla |\vec{r}| + \dots) & \\
 & \sim \overset{\text{Electrical Dipole} }{\vec{k}\cdot \vec{r}} - \overset{\text{Magnetic Dipole and Electrical quadrupole}}{\underline{\underline{\underline{ \vec{k}\cdot \vec{\xi} }}}}
\end{cases}
\end{align}
$$
 
then we have EM potential under far field approximation: 
$$
\begin{align} \\
 & \begin{cases}

\phi(\vec{r},t) & = \frac{1}{4\pi \epsilon_{0}}\int \mathrm{d}^{3}\vec{\xi} \frac{\rho(\vec{\xi})\exp(-\omega(t-|\vec{r}-\vec{\xi}|))}{|\vec{r}-\vec{\xi}|} \\
 & \sim \left( \frac{ {1}}{4\pi \epsilon_{0}} \int \mathrm{d}^{3}\vec{\xi}\frac{\rho(\vec{\xi})\exp(-\vec{k}\cdot \vec{\xi})}{|\vec{r}|} \right)\times \exp(i(\vec{k}\cdot \vec{r} - \omega t)) \\
 & \equiv \phi (\vec{n}) \frac{\exp(i(\vec{k}\cdot \vec{r}-\omega t))}{|\vec{r}|} \\

\vec{A}(\vec{r},t) & = \frac{\mu_{0}}{4\pi }\int \mathrm{d}^{3}\vec{\xi} \frac{\vec{j}(\vec{\xi})\exp(-\omega(t-|\vec{r}-\vec{\xi}|))}{|\vec{r}-\vec{\xi}|} \\
 & \sim \left( \frac{ {\mu_{0}}}{4\pi } \int \mathrm{d}^{3}\vec{\xi}\frac{\vec{j}\exp(-\vec{k}\cdot \vec{\xi})}{|\vec{r}|} \right)\times \exp(i(\vec{k}\cdot \vec{r} - \omega t)) \\
 & \equiv \vec{A}(\vec{n})\frac{\exp(i(\vec{k}\cdot \vec{r}-\omega t))}{|\vec{r}|}
\end{cases}
 \\
 & \text{where:} \begin{cases} 
\phi(\vec{n}) = \left( \frac{ {1}}{4\pi \epsilon_{0}} \int \mathrm{d}^{3}\vec{\xi}\frac{\rho(\vec{\xi})\exp(-\vec{k}\cdot \vec{\xi})}{\underline{\underline{\underline{ 1 }}}} \right) \\
\vec{A}(\vec{n}) = \left( \frac{ {\mu_{0}}}{4\pi } \int \mathrm{d}^{3}\vec{\xi}\frac{\vec{j}\exp(-\vec{k}\cdot \vec{\xi})}{\underline{\underline{\underline{ 1 }}}} \right)
\end{cases}
\end{align}
$$
 then we can calc the EM field: 
$$
\begin{align}
\vec{B} & = \nabla \times \vec{A} = \nabla \times (\vec{A}(\vec{n})\exp(i(\vec{k}\cdot \vec{r}-\omega t))) \\ 
 & = i\vec{k}\times \vec{A}(\vec{n}) \exp(i(\vec{k}\cdot \vec{r}-\omega t)) \\
 & = \vec{B}_0(\vec{n})\exp(i(\vec{k}\cdot \vec{r}-\omega t))\\
\frac{ \partial }{ \partial t } \vec{E} & = -i\omega \vec{E} = \frac{1}{\mu_{0}\epsilon_{0}} \nabla \times \vec{B} =c^{2}i\vec{k}\times(i\vec{k}\times \vec{A}(\vec{n})) \exp(i(\vec{k}\cdot \vec{r}-\omega t)) \\
\vec{E} & =\frac{c^{2}}{\omega} \times (-\vec{k}\times \vec{B}_{0}) \exp(\dots)= c\vec{B}_{0} \times \hat{e}_{{r}} \exp(i(\vec{k}\cdot \vec{r}-\omega t))
\end{align}
$$
- **Electrical Dipole Oscillation**: 
**dipole - current relation**: 
$$
\begin{align}
\vec{P}(t) & = \int_{V'}\mathrm{d}^{3}\vec{\xi}\times( \rho(\vec{\xi},t)\vec{\xi}) \\
\frac{\mathrm{d}}{\mathrm{d}t}\vec{P}(t) & =\int_{V'}\mathrm{d}^{3}\vec{\xi}\times \left( \frac{ \partial \rho(\vec{\xi},t) }{ \partial t } \vec{\xi} \right) \overset{\text{Conservation Law}}{=}-\int_{V'}\mathrm{d}^{3}\vec{\xi}\times(\nabla_{\vec{\xi}}\cdot\vec{j}(\vec{\xi},t)\vec{\xi} ) \\
 & =-\int_{V'}\mathrm{d}^{3}\vec{\xi}\left[ \nabla_{\vec{\xi}}\cdot(\vec{j}(\vec{\xi},t)\vec{\xi}) - (\vec{j}(\vec{\xi},t)\cdot\nabla_{\vec{\xi}} )\vec{\xi} \right] \\
 & =0 + \int_{V'}\mathrm{d}^{3}\vec{\xi}\vec{j}(\vec{\xi},t) \sim \text{Electrical Dipole, leading term of far field approximation}
\end{align}
$$
then we have: 
$$
\begin{align}
\vec{A}(\vec{r},t) & = \frac{\mu_{0}}{4\pi}\int \mathrm{d}^{3}\vec{\xi} \vec{j}(\vec{\xi},t) \times \frac{\exp(i(\vec{k}\cdot \vec{r}-\omega t))}{|\vec{r}|} \\
 & = \frac{\mu_{0}}{4\pi} \frac{\mathrm{d}\vec{P}}{\mathrm{d}t} \frac{\exp(i(\vec{k}\cdot \vec{r}-\omega t))}{|\vec{r}|}
\end{align}
$$
if $\vec{P}(t) = \vec{P}_{0}\exp(-i\omega t)$, then we have: 
$$
\begin{align}
\vec{A}(\vec{r},t) & = \frac{\mu_{0}}{4\pi}(-i\omega)\vec{P}_{0} \frac{\exp(i(\vec{k}\cdot \vec{r}-\omega t))}{| \vec{r} |}\\
 & = \frac{\mu_{0}}{4\pi}\frac{\mathrm{d}\vec{P}\left( t-\frac{| \vec{r} |}{c} \right)}{\mathrm{d}t} \frac{1}{| \vec{r} |}, \left( \text{exp phase term in } \frac{\mathrm{d}\vec{P}\left( t-\frac{|\vec{r}|}{c} \right)}{\mathrm{d}t} \right)
\end{align}
$$
then we have: 
$$
\begin{align}
\vec{B}(\vec{r},t) & = \frac{\mu_{0}}{4\pi} \nabla \times \left( (-i\omega)\vec{P}_{0} \frac{\exp(i(\vec{k}\cdot \vec{r}-\omega t))}{|\vec{r}|} \right) \\
 & = \frac{\mu_{0}}{4\pi} i\vec{k}\times(-i\omega)\vec{P}_{0} \frac{\exp(i(\vec{k}\cdot \vec{r}-\omega t))}{|\vec{r}|} + 0 \\
 & = \frac{\mu_{0}}{4\pi}i\vec{k}\times \frac{\mathrm{d}\vec{P}(t)}{\mathrm{d}t} \frac{\exp(i\vec{k}\cdot \vec{r})}{|\vec{r}|} \\
 & = \frac{\mu_{0}}{4\pi} \frac{\exp(i\vec{k}\cdot \vec{r})}{|\vec{r}|} i |\vec{k}|\hat{e}_{r}\times \dot{\vec{P}}(t) \\
 & =-\frac{\mu_{0}}{4\pi} \frac{\exp(i\vec{k}\cdot \vec{r})}{|\vec{r}|} \frac{1}{c} \hat{e}_{r}\times \ddot{\vec{P}} \\
 & =\frac{1}{4\pi \epsilon_{0}c^{3}} \frac{\exp(i\vec{k}\cdot \vec{r})}{|\vec{r}|} \ddot{\vec{P}}\times \hat{e}_r \\
\vec{E}(\vec{r},t) & = c\vec{B}\times \hat{e}_{r} \\
 & =\frac{1}{4\pi \epsilon_{0}c^{2}} \frac{\exp(i\vec{k}\cdot \vec{r})}{|\vec{r}|} (\ddot{\vec{P}}\times \hat{e}_{r})\times \hat{e}_{r}
\end{align}
$$
 ![[Pasted image 20250905135224.png|393]] 

## Energy Perspective

- for Vaccum Maxwell Eqs
$$
\begin{align}
\varepsilon = \frac{\mathrm{d}E}{\mathrm{d}V} = \frac{1}{2}\epsilon_{0}|\vec{E}|^{2} + \frac{1}{2\mu_{0}}|\vec{B}|^{2} = \frac{1}{2}\vec{E}\cdot \vec{D} + \frac{1}{2 }\vec{B}\cdot \vec{H}
\end{align}
$$
Energy Conservation Law: 
$$
\begin{align}
\oint_{ \partial V } \vec{S}\cdot \mathrm{d}\vec{A} + \frac{ \partial }{ \partial t } \int_{V}\varepsilon\mathrm{d}V = 0 \iff \nabla \cdot \vec{S} + \frac{ \partial \varepsilon }{ \partial t } = 0
\end{align}
$$
then we have
$$
\begin{align}
\vec{S} = \vec{E}\times \vec{H} \overset{\text{Vaccum senario}}{=} \vec{E}\times \frac{\vec{B}}{\mu_{0}}
\end{align}
$$
- non-Vaccum Maxwell Eqs go to 刘川电动力学
$$
\begin{align}
\oint_{ \partial V }\vec{S}\cdot \mathrm{d}\vec{A} + \underline{\underline{\underline{ \overset{\text{Power toward outside}}{\int_{V}\mathrm{d}V \vec{j}\cdot \vec{E}} }}} + \frac{ \partial }{ \partial t } \int_{V}\mathrm{d}V \varepsilon
 = 0\end{align}
$$
...

# Symmetry in Maxwell Eqs (Special Relativitistic Electrodynamics and Gauge Symmetry)

- [Narrow Relativitistic Electiodynamics](https://zhuanlan.zhihu.com/p/29540507240?share_code=ETFJ05NDBFqJ&utm_psn=1946943152301772846) 
- [same as above](https://zhuanlan.zhihu.com/p/174833787?share_code=q0D2yegRqo28&utm_psn=1946943543647113471) 
- [same](https://zhuanlan.zhihu.com/p/602635631?share_code=12J6ULnryqYck&utm_psn=1946957131862509123) 

## Lorentz covariance and invariance 4-Tensor 

$$
\begin{align}
 & \Lambda^{\mu}_{\nu} \text{ is a (1,1) tensor}\iff \left[ \begin{array}{cccccccccc} \gamma & -\gamma \beta & 0 & 0 \\-\gamma \beta & \gamma & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{array} \right] \\
 & \underline{\underline{\underline{ \Lambda^{\mu}_{\alpha}\Lambda^{\beta}_{\mu}=\delta^{\beta}_{\alpha} }}}, \text{ this match: } x'^{\mu}x'_{\mu}=\Lambda^{\mu}_{\alpha}x^{\alpha}\Lambda^{\beta}_{\mu}x_{\beta}=\Lambda^{\mu}_{\alpha}\Lambda^{\beta}_{\mu}x^{\alpha}x_{\beta} \overset{\text{invariance}}{=}x^{\alpha}x_{\alpha} \\
 & \text{let: } g^{\mu \nu} \iff \left[ \begin{array}{cccccccccc} 1 & & & \\ & -1 & & \\ & & -1 & \\ & & & -1 \end{array} \right]  
\end{align}
$$ 

### 4-scalar 

$$
\begin{align}
\tau,\mathrm{d}\tau ,m_{0},q,\mathrm{d}s^{2}=\mathrm{d}x^{\mu}\mathrm{d}x_{\mu},\mathrm{d}^{4}V=\mathrm{d}^{4}x^{\mu} , F^{\mu \nu}F_{\mu \nu}=2\left( \vec{B}^{2}-\frac{\vec{E}^{2}}{c^{}} \right),\epsilon_{abcd}F^{ab}F^{cd} = \frac{8i}{c} \vec{E}\cdot \vec{B}, \phi=-k^{\mu}x_{\mu}, 
\end{align}
$$

### 4-Vector

$$
\begin{align}
x_{\mu}=\left[ \begin{array}{cccccccccc} ct \\ x \\ y \\ z \end{array} \right] ,u^{\mu}=\gamma\left[ \begin{array}{cccccccccc} c \\ v_{x} \\ v_{y} \\v_{z} \end{array} \right] ,p^{\mu} = \gamma m_{0}\left[ \begin{array}{cccccccccc} c \\ v_{x} \\ v_{y} \\v_{z} \end{array} \right] , k^{\mu}=\left[ \begin{array}{cccccccccc} \frac{\omega}{c} \\ k_{x} \\ k_{y}\\k_{z} \end{array} \right] , \partial_{\mu}=\left[ \begin{array}{cccccccccc} \frac{1}{c}\partial_{t} \\ \partial_{x} \\ \partial_{x} \\ \partial_{z} \end{array} \right] ,\underline{\underline{\underline{ J^{\mu} = \rho_{0} u^{\mu} = \gamma \rho_{0}\frac{u^{\mu}}{\gamma}=\left[ \begin{array}{cccccccccc} c\rho \\ j_{x} \\ j_{y} \\ j_{z} \end{array} \right] }}}  
\end{align}
$$

### 4-Tensor (Matrix) 

$$
\begin{align}
F^{\mu \nu}=\left[ \begin{array}{cccccccccc} 0 & -\frac{E_{x}}{c} & -\frac{E_{y}}{c} & -\frac{E_{z}}{c} \\ \frac{E_{x}}{c} & 0 & -B_{z} & B_{y} \\ \frac{E_{y}}{c} & B_{z} & 0 & -B_x \\ \frac{E_z}{c} & -B_{y} & B_{x} & 0 \end{array} \right]  
\end{align}
$$

## EM Laws ⭐

$$
\begin{align}
  & \text{Current Conservation Law: } & \partial_{\mu}J^{\mu} & = 0 \\  
 & \text{Gauge Transformation:} & A^{\mu} & \to A^{\mu} + \partial^{\mu}\chi \\
 & \text{Lorentz Gauge: } & \partial_{\mu}A^{\mu} & =0 \\  
 & \text{EM potential:}  &    \partial^{\nu}  \partial_{\nu}A^{\mu}  & = -\mu_{0}J^{\mu} + (  \partial^{\nu}  \partial_{\nu}  )\partial^{\mu}\chi   \text{ ( this tell us EM potential is 4-Vector)}\\
 & \text{EM potential under Lorentz: } & ( \partial^{\nu} \partial_{\nu} ) A^{\mu} & = -\mu_{0}J^{\mu} \text{ ( this tell us EM potential is 4-Vector)}\\
 & \text{Faraday Tensor:} & F^{\mu \nu} & = \partial^{\mu}A^{\nu}- \partial^{\nu}A^{\mu} \\
 & & & \overset{\text{Gauge Trans}}{\implies} ( \partial^{\mu}A^{\nu} + \partial^{\mu} \partial_{\nu}\chi )- ( \partial^{\nu}A^{\mu} + \partial^{\nu} \partial_{\mu}\chi ) \\
 & & & = \partial^{\mu}A^{\nu}- \partial^{\nu}A^{\mu} + \underset{0}{\underline{\underline{\underline{ {( \partial^{\mu} \partial_{\nu}- \partial^{\nu} \partial_{\mu} )\chi }}}}}= \partial^{\mu}A^{\nu}- \partial^{\nu}A^{\mu} \\
 & \text{Maxwell Eqs}: & & \begin{cases}
 & \begin{cases}
\nabla \cdot \vec{E} & = \frac{\rho}{\epsilon_{0}} \\
\nabla \times \vec{B} & = \mu_{0}\vec{j}+\mu_{0}\epsilon_{0}\frac{ \partial \vec{E} }{ \partial t } 
\end{cases} & \implies \partial_{\mu }F^{\mu \nu} = -\mu_{0}J^{\nu} \\
 & \begin{cases}
 \nabla \cdot \vec{B} & =0 \\
\nabla \times \vec{E} & =-\frac{ \partial \vec{B} }{ \partial t } 
\end{cases} & \implies \partial_{\alpha}F^{\beta \gamma} + \partial_{\beta }F^{\gamma \alpha} +\partial_{\gamma}F^{\alpha \beta} = 0 
\end{cases} \\
 & \text{EM Force:} & f^{\mu} & =F^{\mu \nu}J_{\nu} = \left[ \begin{array}{cccccccccc} \frac{1}{c}\vec{j}\cdot \vec{E}   \\ \rho E_{x}+j_{y}B_{z}-j_{z}B_{y} \\ \rho E_{y}+j_{z}B_{x}-j_{x}B_{z} \\ \rho E_{z}+j_{x}B_{y}-j_{y}B_{x}
 \end{array} \right]  
\end{align}
$$

# Analytical Mechanics Perspective 

2 assumption: 
- **$S$ should be Lorentz invariance**
- **$S$ should be gauge invariance** 

## Special Relativity Mechanics under Analytical Mechanics Perspective 

$$
\begin{align}
 S  & = \int \mathrm{d}t L(q,\dot{q},t) \\
  & =\int \mathrm{d}\tau \underset{  \text{Lorentz invariance}  }{\underline{\underline{\underline{  (\gamma L(q,\dot{q},t))    }}}}  \\
  & \overset{\frac{\dot{q}}{c}\to_{0}}{=}\int \mathrm{d}\tau (T-V), T = \frac{1}{2}m\vec{v}^{2} \\
  \text{then, we have: } \gamma L_{\text{free}}(q,\dot{q},t )  & = -\gamma m_{0}c^{2} \to  C+\frac{1}{2}m\vec{v}^{2} \\
\text{then: } S  & = \int \mathrm{d}\tau \times(-\gamma m_{0}c^{2}) 
\end{align}
$$

## EM theory under Analytical Mechanics Perspective 

when think about EM theory in Analytical Mechanics Perspective, the path is constructed with $\mathrm{d}^{4}x^{\mu}$, the coordinates, the velosities, the momentums become **field**.  

set EM potential as general coordinates
$$
\begin{align}
\mathcal{L}(A^{\mu},  \partial_{\nu }A^{\mu},t )  & = \underset{\text{free EM field Energy}}{\underline{\underline{\underline{  -\frac{1}{4\mu_{0}}F^{\mu \nu}F_{\mu \nu}    }}}} -\underset{  \text{ EM potential Energy}  }{\underline{\underline{\underline{   J^{\mu}A_{\mu}   }}}} 
 \\
 L&=\int \mathrm{d}^{4}x^{\mu} \mathcal{L}(A^{\mu},  \partial_{\nu }A^{\mu},t )
\end{align}
$$
apply variation principle we conclude Euler Lagrangian Eq and Hamiltonian Canonical Eqs: 
$$
\begin{align}
   \frac{ \partial  }{ \partial x^{\mu} } \left( \frac{ \partial \mathcal{L} }{ \partial (  \partial_{\mu}A^{\nu} ) }  \right) - \frac{ \partial \mathcal{L} }{ \partial A^{\nu} }  & =0  \\
   \pi_{\mu}^{\nu} & \equiv \frac{ \partial \mathcal{L} }{ \partial (  \partial_{\mu}A^{\nu} ) }   = - F^{\nu}_{\mu} \\
   \pi^{\mu \nu} & =-F^{\mu \nu} ,\text{ generalized momentum is field} \\
\mathcal{H}  & \equiv \pi^{0}_{\mu}A^{\mu}-\mathcal{L}, \left( \pi_{\mu}=\pi^{0}_{\mu}=\frac{ \partial \mathcal{L} }{ \partial  ( \partial_{0} A^{\mu} ) } =   \text{ is time derivative momentum}\right) \\
 & =\frac{1}{2}\left( \epsilon_{0}\vec{E}^{2}+\frac{1}{\mu_{0}}\vec{B}^{2} \right) + J^{\mu}A_{\mu} 
\end{align}
$$ 

# Static Electromagnetism

## Electrostatics

$$
\begin{align}
\begin{cases}
\nabla \cdot \vec{E} & =\frac{\rho}{\epsilon_{0}} \\
\nabla \times \vec{E} & =0
\end{cases}
\end{align}
$$
with the second formula, we conclude that $\vec{E}=-\nabla \phi$, then we have
$$
\begin{align}
\begin{cases}
\nabla^{2}\phi = - \frac{1}{\epsilon_{0}}\rho(\vec{r}) \\ 
\phi| _ {\partial V} \dots \text{ and } \partial_{n} \phi |_{ \partial V } \dots
\end{cases} \tag{Electrostatics Problem}
\end{align}
$$
1) **Green Func Method** $\delta$ 
devide the nonlinear Electrostatics problem into **General Solution + Particular Solution** 
$$
\begin{align} \\
 & \text{particular solution: }\begin{cases}
\nabla^{2}G(\vec{r},\vec{\xi}) = -\frac{1}{\epsilon_{0}}\delta(\vec{r}-\vec{\xi}) \\
G(\vec{r},\vec{\xi}) |_{ \partial V } = 0 \text{ and } \partial_{n}G(\vec{r},\vec{\xi}) = 0 
\end{cases} \\
 & \text{general solution: }\begin{cases}
\nabla^{2}\phi_{0} = 0 \\
\phi_{0} |_{ \partial V } \dots\text{ and } \partial_{n}\phi_{0} |_{ \partial V } \dots
\end{cases} \tag{a eigen problem}\\
 & \text{final solution: } \phi = \phi_{0} + \int_{V'} \mathrm{d}V' \rho(\vec{r'}) G(\vec{r},\vec{r'})
\end{align}
$$
 
2) **Seperation Variables Method** 
$$
\begin{align}
\nabla^{2}\cdot & = \frac{1}{r} \left( \frac{ \partial }{ \partial r } \right)^{2}(r\cdot) - \frac{\hat{l}^{2}}{r^{2}}\cdot \\
\varphi(\vec{r}) & = R( {r})Y_{lm}(\theta,\phi) 
\end{align}
$$
 
then we have 
$$
\begin{align}
 & \frac{1}{r} \left( \frac{ \partial }{ \partial r } \right)^{2}(r\cdot R(r) ) - \frac{l(l+1)}{r^{2}}R(r) = 0 \\
 & \text{let: }u(r) = rR(r) \\
 & \left( \frac{\mathrm{d}}{\mathrm{d}r} \right)^{2} u(r) = \frac{l(l+1)}{r^{2}}u(r) \\
 & \text{give trial solution: } u(r) = r^{\alpha} \\
 & \dots \\
 & R(r) = \underline{\underline{\underline{ A\times r^{l} + B\times \frac{1}{r^{l+1}} }}} \overset{l=0}{\to}A + \frac{B}{r}, \text{which is static electric potential}
\end{align}
$$

### Uniqueness Theorem

### Conductor 

## Magnetostatics

$$
\begin{align}
\begin{cases}
\nabla \cdot \vec{B} & =0 \\
\nabla \times \vec{B} & =\mu_{0}\vec{j}
\end{cases}
\end{align}
$$
 apply $\nabla \times\vec{A} = \vec{B}$, choose coloumb gauge $\nabla \cdot \vec{A}=0$, we have: 
$$
\begin{align}
\begin{cases}
\nabla^{2}\vec{A} = -\mu_{0}\vec{j} \\
\vec{A}|_{ \partial V }\dots \text{ and } \partial \vec{A}|_{ \partial V }\dots \text{(very complex...)}
\end{cases} \tag{Magnetostatics Problem}
\end{align}
$$
1) **Green Func Method** 
2) **Seperation Variables Method**
3) **Scalar Magenetic Potential Method(if no free current)**
$$
\begin{align}
\begin{cases}
\nabla \cdot \vec{B} & =\nabla \cdot[\mu_{0}(\vec{H}+\vec{M})] & =0 \\
\nabla \times \vec{H} & =\vec{j}_{\mathrm{f}} & = 0
\end{cases}
\end{align}
$$
then we have: 
$$
\begin{align}
\begin{cases}
\nabla \cdot \vec{H} & = -\nabla \cdot \vec{M} \\
\nabla \times \vec{H} & = 0
\end{cases}
\end{align}
$$
then give a scalar magnetic potential $\phi_{m}$ with $\vec{H}=-\nabla \phi_{m}$
$$
\begin{align}
\begin{cases}
\nabla^{2}\phi & = \nabla \cdot \vec{M} \\
\phi_{m}|_{ \partial V} \dots
\end{cases}
\end{align}
$$ 

### Fe Magnetor 
