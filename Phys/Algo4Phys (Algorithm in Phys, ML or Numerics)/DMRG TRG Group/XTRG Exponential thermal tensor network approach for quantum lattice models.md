
- [chat with gemini on XTRG](https://g.co/gemini/share/3395a45e1171) 

**我们不得不承认, 几乎每个idea都是简单的东西, 只是有些简单的东西非常重要.** 

$$
\rho_{n+1}  = \rho_{n}\cdot \rho_{n}
$$
$$
\rho_{n} = \rho(2^{n}\beta) = e^{ -2^n\beta  \hat{H} }
$$

## XTRG (Exponential Thermal Tensor Network) Procedure ⚙️

The Exponential Thermal Tensor Network (XTRG) approach is a numerical method for simulating quantum lattice models at finite temperatures with high efficiency[cite: 2]. The overall procedure involves the following steps:

---

### 1. Initialization at High Temperature (Small $\tau_0$) 🌡️
* The process begins by preparing a Matrix Product Operator (MPO) representation of the unnormalized thermal state $\rho(\tau_0) = e^{-\tau_0 H}$ at an exponentially small initial inverse temperature $\tau_0$[cite: 111]. This corresponds to a very high actual temperature.
* For very small $\tau_0$ values (e.g., $\tau_0 J \approx 10^{-6}$), a simple linear expansion like $\rho(\tau_0) \approx I - \tau_0 H$ can be sufficient and extremely simplifies initialization[cite: 116].
* For slightly larger initial $\tau_0$ values (e.g., $\tau_0 J \approx 10^{-3}$), an efficient series expansion scheme like SETTN (Series Expansion Thermal Tensor Network) can be employed[cite: 115, 116].

---

### 2. Iterative Doubling of Inverse Temperature ❄️
* Starting with $\rho_0 \equiv \rho(\tau_0)$, the system is cooled down exponentially by iteratively computing $\rho_n \equiv \rho(\tau_n) = \rho_{n-1} \cdot \rho_{n-1}$, where $\tau_n = 2\tau_{n-1} = 2^n \tau_0$[cite: 113].
* Each iteration involves multiplying the MPO $\rho_{n-1}$ by itself [see Fig. 2(b) for a visual representation of a single step, source: 65].
* A crucial part of this step is the compression of the resulting MPO (from the product $\rho_{n-1} \cdot \rho_{n-1}$) back to a manageable bond dimension $D^*$[cite: 171]. For XTRG, a variational MPO compression technique is typically used.

---

### 3. Obtaining the Physical Density Matrix and Partition Function 📊
* The MPO $\rho(\tau_n)$ obtained at iteration $n$ represents $e^{-\beta H/2}$ if the target inverse temperature is $\beta = 2\tau_n$[cite: 120, 121].
* The (unnormalized) physical thermal state $\rho(\beta)$ at this target $\beta$ is computed as $\rho(\beta) = \rho(\tau_n)^{\dagger} \rho(\tau_n)$[cite: 119]. This ensures the positivity of the density matrix, even in the presence of MPO truncations[cite: 119].
* The partition function $\mathcal{Z}(\beta)$ is then calculated as $\mathcal{Z}(\beta) = \text{Tr}[\rho(\tau_n)^{\dagger} \rho(\tau_n)]$[cite: 120]. This can be obtained by computing the squared Frobenius norm of $\rho(\tau_n)$[cite: 121].

---

### 4. Achieving Finer Temperature Resolution (Optional) 촘촘하게
* If the logarithmic grid of $\beta$ values produced by the doubling scheme is too sparse, intermediate temperature points can be obtained[cite: 5, 124].
* One method is to use "z-shifts," which involves running independent XTRG simulations starting with slightly shifted initial values, $\tau_0' = \tau_0 \cdot 2^z$, where $z \in [0,1)$[cite: 124]. These different "z-shifts" can be computed independently and thus efficiently parallelized[cite: 125].
* Alternatively, intermediate $\beta$ values can be obtained by computing products of MPOs from different steps, e.g., $\rho_{n-1} \cdot \rho_{n'-1}$ for various $n' \le n$[cite: 127].

---

### 5. Exploitation of Symmetries 🛡️
* Throughout the entire XTRG procedure, symmetries of the Hamiltonian (both Abelian, like U(1), and non-Abelian, like SU(2)) are fully implemented and exploited within the MPO framework[cite: 8, 85, 86]. This is crucial for enhancing numerical performance and is detailed in Sec. II.A and Appendix B of the paper.



