# The paper: 
## Supercell Hamiltonian
periodic representation of overall Hamiltonian, replica of many supercells to mimic a overall Hamiltonian. 
$$

\hat{H}_s = -\frac{1}{2} \sum_{i=1}^{N} \nabla_i^2 
- \sum_{i=1}^{N} \sum_{I=1}^{N_{\text{atom}}} \sum_{\mathbf{L}_s} \frac{Z_I}{|\mathbf{r}_i - \mathbf{R}_I + \mathbf{L}_s|}
+ \frac{1}{2} \sum_{i=1}^{N} \sum_{j=1}^{N}{}' \sum_{\mathbf{L}_s} \frac{1}{|\mathbf{r}_i - \mathbf{r}_j + \mathbf{L}_s|}
+ \frac{1}{2} \sum_{I=1}^{N_{\text{atom}}} \sum_{J=1}^{N_{\text{atom}}}{}' \sum_{\mathbf{L}_s} \frac{Z_I Z_J}{|\mathbf{R}_I - \mathbf{R}_J + \mathbf{L}_s|}


$$
where sum over $\mathbf{L_{s}}$ gives the replica of these supercells. 




## Backflow Transformation: reinfrocement of Slater Determinant
- [chat with gemini](https://g.co/gemini/share/157a4d4bdb17) 

Backflow Transformation adds the $\{\verb|\|\mathbf{x_{i}}\}$ terms, which give a stronger expressiveness.
$$
\Psi(\mathbf{x}) = \mathrm{\det}[\phi_{k}(\mathbf{x_{i},\{\verb|\| \mathbf{x}_{i}\}})]
$$

# The PPt: 
![[Pasted image 20250528161607.png]]