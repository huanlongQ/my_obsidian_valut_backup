# From Classical Mechanics to Quantum Mechanics: Schrodinger Eq

$$
\begin{align}
i\frac{\mathrm{d}}{\mathrm{d}t}\ket{\psi} = H\ket{\psi} 
\end{align}
$$

# Basic Properties of Wave Func

1) normalization
2) uncertainty principle
3) orthogonality 

# Integrable System

## Free Electron

## Harmonic Oscillation ⭐

## $\delta$ potential

## Hydrogen Atom

### $\nabla^2$ and Spherical Harmonic Func $Y_{lm}$

### Angular Momentum and its operators 

### Other effects

# Spin and Angular Momentum and $\mathrm{SU}(2)$ or $\mathrm{SO(3)}$ Algebra⭐ 

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

- [CG coeff](https://www.zhihu.com/question/271044965/answer/361887639?share_code=CyRIzSxnrSm&utm_psn=1946931252356714995)







# Time Independent Perturbation Theory 

# Time Dependent Perturbation Theory


# Variations Principle ⭐

