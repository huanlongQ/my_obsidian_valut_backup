# 1. Hubbard Model

## 1.1 The model itself

Hubbard Model shows the competition between the kinetic energy(t) and the interaction energy(U) at **half filling circumstance**.

$$
H=\sum_{<ij>,\sigma}-tc_{i,\sigma}c^{\dagger}_{j,\sigma }+h.c. + \sum_{i}Uc_{i,\uparrow}^{\dagger}c_{i,\uparrow}c_{i,\downarrow}^{\dagger}c_{i,\downarrow}
$$
 


## 1.2 The derivation of Hubbard Model

[O空O扬O 如何理解Hubbard Model](https://www.zhihu.com/question/27482740/answer/2134058563)

[Essler 2005 1.2 Hubbard模型——凝聚态物理的范式](https://zhuanlan.zhihu.com/p/536485018) 

The overall Hamiltonian of electrons in solid system include 3 parts, the **kinetic energy of electrons, the electron-lattice interaction and the electron-electron interaction.**

Drude Sommerfeld Model: neglect electron-lattice and electron-electron interaction.

Bloch Theory: mix kinetic energy of electrons and electron-lattice interaction as a new 'electron'(as a second quantization consequence). Bloch introduced the energy band theory.

**Hubbard Model: consider both kinetic energy, electron-lattice interaction for parameter t and electron-electron interaction for parameter U.**

# 2. Related Fields

## 2.1 Neel Transition

Neel transition is a transition between a paramagnetic ordered phase and a antiferromagnetic ordered phase. The **order parameter** of Neel transition is **m, the staggered magnetism:**
![[Pasted image 20250328111323.png]]
 

- **Mean Field Approximation Solution:**
    
- **Critical temperature:**
	$T_c \approx 0.3$ over this temp, model is paramagnetic, below it, model becomes antiferromagnetic. 
- **Strange order parameter: staggered magnetism:**
    

The "strangeness" of the staggered magnetization as an order parameter stems from the very nature of antiferromagnetic order. Unlike ferromagnets, where all spins align uniformly to give a net magnetization, antiferromagnets feature neighboring spins that are oppositely aligned. This means that if you simply sum up the magnetic moments over the whole lattice, the contributions cancel, resulting in zero net magnetization.

**only if we choose a staggered magnetism,  we can see a non zero m.**

- Dimensionality Matters!
    

1. In high dimensional circumstance, Mean Field Theory becomes accurate, whicn indicate that the thermal flucataion is less important.
    
2. Density of states varies in power law across different dimensionalities, thus the energy spectra.
    

The analogy ties directly to the concept of the density of states (DoS). In lower-dimensional systems, **the DoS at low energies (or long wavelengths) is higher compared to higher dimensions. This means there are relatively more available low-energy modes that can be excited when you add thermal energy.** In the canal analogy, the limited geometry forces the energy into a few coherent long-wavelength modes, much like how a high DoS at low energy in low dimensions leads to stronger, more coherent fluctuations. Conversely, in higher dimensions, the energy is spread over many more modes, diluting the effect of any single long-wavelength excitation.
![[Pasted image 20250328111335.png]]  
In high dimensions, most of the thermal energy goes to the higher energy modes rather than a low energy mode. You can think with the usage of partition function calculation: 
$$
Z = \int \text{DoS}(E)dE e^{ -\beta E }
$$
higher DoS in low energy makes a bigger partition func aka a bigger and steep changing in temperature free energy $F$.
