# 1. Kohn thm
[# 密度泛函理论之 Hohenberg-Kohn 定理的证明](https://zhuanlan.zhihu.com/p/475254000)
## Kohn 1 thm
From the perspective of a electron sys with external potential. 
$$
H = T + V_{\mathrm{ext}} + V_{\mathrm{ele-ele}}
$$
The $\rho_{\mathrm{ele}}$ of GS(Ground State) and its external potential $V_{\mathrm{ext}}(\vec{r})$ has one to one correspondence. 
AKA $H$ is a functional of $\rho(\vec{r})$, $H[\rho(\vec{r})]$. 

AKA if you have a $H$, its GS $\rho$ is unique
AKA This theorem states that the ground-state electron density of a many-electron system uniquely determines the external potential. Since the external potential (the potential due to the nuclei) uniquely determines the Hamiltonian of the system, and the Hamiltonian in turn determines all properties of the system (including the ground-state wavefunction), this theorem implies that all ground-state properties of a many-electron system are uniquely determined by its ground-state electron density.
## Kohn 2 thm
For a electron sys with external potential, Its Energy functional $E[\rho (\vec{r})]$ get minmum $E_{0}$ when  $\rho$ is the GS $\rho_{\mathrm{GS}}$ of the functional $H[\rho(\vec{r})]$ 

AKA, if you have a GS $\rho$ and a $H$, and $\rho$ is the GS of $H[\rho(\vec{r})]$, then $E[\rho(\vec{r})]$ can get GS energy. 
AKA This theorem states that for any given external potential, the ground-state energy of the system can be obtained by minimizing a universal functional of the electron density. This functional, known as the Hohenberg-Kohn functional ($F[ρ]$), is valid for any many-electron system and contains the kinetic energy of the electrons and the electron-electron interaction energy.

## why is thm2 needed? 
thm2 guaranteed that if you get minmum $E[\rho(\vec{r})]$, you should get $\rho_{\mathrm{GS}}(\vec{r})$. 
Thus, thm1 is just a principle without utility but thm2 is such a useful thm. 


# 2. Pesudo Code and Precedure
Nice pesudo code. 
```
// Input: Atomic positions, nuclear charges, number of electrons, choice of exchange-correlation functional, basis set (or grid), convergence criteria.

// 1. Initialization
Initialize:
  Generate an initial guess for the electron density, ρ_in(r).
  (Common methods: superposition of atomic densities, or calculate from initial guess orbitals)

// 2. Self-Consistent Field (SCF) Loop
Loop Until Convergence:

  // a. Calculate the Kohn-Sham Potential
  Construct the effective Kohn-Sham potential, V_KS(r), from ρ_in(r):
    V_KS(r) = V_ext(r) + V_Hartree[ρ_in](r) + V_xc[ρ_in](r)

    Where:
      V_ext(r)     is the external potential (from atomic nuclei).
      V_Hartree[ρ] is the Hartree potential (classical Coulomb repulsion between electrons), calculated from ρ.
      V_xc[ρ]      is the exchange-correlation potential, derived as the functional derivative of the chosen E_xc[ρ] approximation with respect to ρ.

  // b. Solve the Kohn-Sham Equations
  Solve the single-particle Kohn-Sham equations:
    [-ħ²/2m ∇² + V_KS(r)] φ_i(r) = ε_i φ_i(r)
    (This is the most computationally expensive step, typically involving matrix diagonalization or other eigenvalue solvers, depending on the basis set/representation)

    Obtain the Kohn-Sham orbitals {φ_i} and their energies {ε_i}.
    Select the lowest energy orbitals up to filling the number of electrons (obeying the Pauli exclusion principle).

  // c. Calculate New Electron Density
  Calculate the output electron density, ρ_out(r), from the occupied Kohn-Sham orbitals:
    ρ_out(r) = Σ_i |φ_i(r)|²  (sum over occupied orbitals)

  // d. Check for Convergence
  Check if the new density ρ_out(r) is sufficiently close to the input density ρ_in(r).
  (Convergence criteria can be based on the change in density, total energy, or potential between iterations).

  If (ρ_out is converged with respect to ρ_in):
    Break Loop

  // e. Update Density for Next Iteration (Mixing/Damping)
  If not converged, prepare the input density for the next iteration.
  Simple mixing: ρ_in_next(r) = α * ρ_out(r) + (1 - α) * ρ_in(r) (where α is a mixing parameter, 0 < α <= 1)
  More sophisticated mixing schemes (e.g., Pulay mixing, DIIS) are used in real codes to accelerate and stabilize convergence.
  Set ρ_in(r) = ρ_in_next(r)

// 3. Post-Convergence Calculations
Once converged (at ρ_GS, φ_i_GS, ε_i_GS):

  Calculate the total ground-state energy, E_0, using the converged density and orbitals in the Kohn-Sham energy functional:
    E_0 = T_s[ρ_GS] + E_Hartree[ρ_GS] + E_xc[ρ_GS] + E_ext[ρ_GS] + E_ion-ion

    Where:
      T_s[ρ_GS] is the kinetic energy of the non-interacting electrons (calculated from φ_i_GS).
      E_Hartree[ρ_GS] is the classical Coulomb electron-electron repulsion.
      E_xc[ρ_GS] is the exchange-correlation energy (calculated using the chosen functional approximation).
      E_ext[ρ_GS] is the electron-nucleus interaction energy.
      E_ion-ion is the nucleus-nucleus repulsion energy.

  Calculate other desired ground-state properties (e.g., forces on atoms, pressure, dipole moment, band structure, etc.) using the converged density and orbitals.

// Output: Ground-state energy, ground-state density, Kohn-Sham orbitals and energies, forces, other requested properties.
```

## $V_{xc}(\vec{r})$ intorduction: 

**Components of $V_{xc}$:** 
- Exchange(Pauli Exclusion Principle)
	eletron with same spin can not occupy the same state. this create a **Fermi Hole**. 
- Correlation: 
	Beyond Pali principle, electrons dynamically avoid each other non-mean-fieldly. this creates a **Coulomb Hole**. 

**Formulism:** 
$$
V_{xc} = \frac{\delta E_{xc}[\rho]}{\delta \rho(\vec{r})}
$$
this is a functional derivative. $E_{xc}[\rho]$ is excange correlation energy functional of $\rho(\vec{r})$. 

$$
E_{xc}[\rho] = E_{x}[\rho]+E_{c}[\rho]
$$



# 3. DFT for solid state sys electronic band struct
translational sym gives Bloch thm. we go through dft kohn sham approach to calculate electronic band struct. 
## if you have the Kohn Sham potential $V_{\mathrm{KS}}(\vec{r})$ 
wow, it's easy, just put kohn sham eq into reciprocal space: 
$$
[-\frac{1}{2}\nabla^{2} + V_{\mathrm{KS}}(\vec{r})]\psi_{n,k}(\vec{r}) = E_{n,k}\psi_{n,k}(\vec{r})
$$
where $\psi_{n,k}(\vec{r}) = e^{ i \vec{k }\cdot\vec{r} }u_{n,k}(\vec{r})$ due to bloch thm
then 
$$
[-\frac{1}{2}(\nabla+i \vec{k})^{2} + V_{\mathrm{KS}}(\vec{r})]u_{n,k}(\vec{r}) = E_{n,k}u_{n,k}(\vec{r})
$$
and then Fourier the $V_{\mathrm{KS}} = \sum e^{ i \vec{k}\cdot\vec{r} }V_{\vec{k}}$, then separate different freq to calculate for **normal band struct calculation**. 
## How to get $V_{\mathrm{KS}}(\vec{r})$? DFT self consistent field iteration

now we should do kohn sham eq minimize for this Hamiltonian. get GS and calculate $V_{\mathrm{KS}}(\vec{r})$. $V_{\mathrm{KS}}(\vec{r})$ is a complex conception then, in the below chat we dicussed about it. 
[chat with gemini](https://g.co/gemini/share/0b21bb867b93) 


the occupied states' energy is overestimated and the non-occupied states' energy is underestimated. to summary, the fermi gap is underestimated. 
