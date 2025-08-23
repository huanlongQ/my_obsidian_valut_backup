- [[XTRG Exponential thermal tensor network approach for quantum lattice models]] is its predecessor. 
- [chat with gemini on tdvp tebd and this paper](https://g.co/gemini/share/ade65cb0ecee) 

# TDVP: tanTRG needs ***TDVP***
- [[Tensor Network Representation (General)]]
- My comment: **you need just project the exact Hamiltonian into a MPO version Hamiltonian in the tangent space of MPS**. 
## TDVP introduction: 
Of course. The Time-Dependent Variational Principle (TDVP) is a powerful and elegant framework for simulating the time evolution of quantum many-body systems. Let's break it down into a conceptual explanation, its mathematical formulism, and a practical pseudocode.

### 1. The Idea in Words

Imagine the vast space of all possible quantum states for a system (the Hilbert space). It's astronomically large. Now, imagine a much smaller, manageable "map" or submanifold within this space that you can efficiently describe with a specific structure, like a Matrix Product State (MPS). This MPS manifold contains states with a limited amount of entanglement, which are often excellent approximations for the physically relevant states (like ground states or states not too far from equilibrium).

The problem is, when you apply the time evolution operator $e^{-iHt}$ to a state on your MPS map, the resulting state is almost guaranteed to be "knocked off" the map, into the full, unmanageable Hilbert space.

This is where TDVP comes in. **TDVP provides a principled way to find the *best possible approximation* of the true time-evolved state that still lies on your chosen manifold.**

Instead of evolving the state and then trying to force it back onto the map (which can be inaccurate), TDVP projects the *direction* of the time evolution (given by the action of the Hamiltonian, $H|\Psi\rangle$) onto the "tangent space" of the manifold at the current state's position. Think of the tangent space as the set of all possible directions you can move in without immediately leaving the map.

By following this projected direction for a small time step, you evolve the state to a new point that is still on (or very close to) your manifold. This makes the evolution stable, accurate, and computationally feasible. For the single-site version of TDVP, it has the remarkable properties of conserving both the norm of the state and the energy of the system.

### 2. The Formulism in Math

The core of quantum dynamics is the time-dependent Schrödinger equation:
$$i \frac{d}{dt} |\Psi(t)\rangle = H |\Psi(t)\rangle$$
Here, $|\Psi(t)\rangle$ is the exact wavefunction.

Now, we restrict our wavefunction to a specific variational manifold, parametrized by a set of tensors $\{A_i\}$. Let's denote such a state as $|\Psi(\{A_i\})\rangle$. The fundamental problem is that if $|\Psi(\{A_i\})\rangle$ is on the manifold, $H|\Psi(\{A_i\})\rangle$ is generally not.

The TDVP solves this by demanding that the time evolution of our variational state, $|\dot{\Psi}(\{A_i\})\rangle$, is the best possible approximation of the "true" evolution direction, $-iH|\Psi(\{A_i\})\rangle$, within the tangent space of the manifold. This is achieved via an orthogonal projection.

Let $P_{T}(\{|\Psi\rangle\})$ be the projector onto the tangent space of the manifold $\mathcal{M}$ at the point $|\Psi\rangle$. The TDVP equation of motion is:
$$i \frac{d}{dt} |\Psi(\{A_i\})\rangle = P_{T}(|\Psi(\{A_i\})\rangle) H |\Psi(\{A_i\})\rangle$$

This abstract equation becomes concrete when we consider a specific tensor network, like an MPS. For an MPS, the tangent space can be constructed by infinitesimal variations of the individual tensors. A clever insight by Haegeman et al. (2011, 2016) showed that this projection can be decomposed into a sum of local terms, which makes the problem tractable.

Instead of solving the full differential equation at once, we can use a Lie-Trotter splitting. The evolution for a small time step $\delta t$ is broken down into a sequence of smaller, local updates that sweep back and forth across the MPS chain.

For an MPS in the "mixed canonical form" with the orthogonality center at site $j$, the evolution is split into two parts:

1.  **Forward sweep (j=1 to N-1):**
    * **Evolve the site tensor $A_j$**: This involves solving a local effective Schrödinger equation for the "center site" tensor. You essentially evolve the tensor $A_j$ forward in time by $\delta t/2$ using an effective Hamiltonian for that site.
    * **Absorb and move the center**: The evolved tensor is then decomposed (e.g., using QR decomposition) to restore the left-canonical form of the new $A_j$ and update the center tensor $C_{j+1}$ for the next site.

2.  **Backward sweep (j=N to 2):**
    * **Evolve the site tensor $A_j$**: Similarly, evolve the current center tensor backward in time by $\delta t/2$.
    * **Absorb and move the center**: Decompose the result (e.g., using LQ decomposition) to restore the right-canonical form of $A_j$ and update the center tensor $C_{j-1}$.

This sweep-based procedure is highly efficient and numerically stable.

### 3. The Algorithm in Pseudocode

Here is a pseudocode for the widely used **one-site finite TDVP algorithm**. This version keeps the bond dimension fixed.

**Input:**
* An MPS $|\Psi\rangle = \{A_1, A_2, ..., A_N\}$ in right-canonical form ($A_i$ are right-isometric).
* A Hamiltonian $H$ represented as an MPO.
* A small time step $\delta t$.
* Total evolution time $T$.

**Initialization:**
1.  Bring the MPS to mixed-canonical form with the center at site 1. This means $A_1$ is the center tensor $C_1$, and $A_2, ..., A_N$ are right-canonical.
2.  Pre-calculate the right environment tensors $\{R_j\}$ for the MPO $H$ from right to left. $R_{N+1} = 1$.

```pseudocode
function TDVP_Evolve(MPS, H_MPO, dt, T):
    num_steps = T / dt
    
    // Initial setup
    bring_MPS_to_right_canonical_form(MPS)
    C = MPS[0] // Center tensor at the beginning
    MPS[0] = null // Placeholder

    // Pre-calculate right MPO environments
    R_envs = calculate_right_environments(MPS, H_MPO)
    L_envs = array of size N+1
    L_envs[0] = 1 // Left environment identity at the boundary

    for step = 1 to num_steps:
        
        // FORWARD SWEEP (evolve by +dt/2)
        for j = 1 to N-1:
            // 1. Construct effective Hamiltonian for the center site C
            H_eff = build_effective_H(L_envs[j-1], R_envs[j+1], H_MPO[j])
            
            // 2. Evolve the center tensor C
            C_evolved = solve_linear_equation(exp(-i * H_eff * dt/2), C) // e.g., using Krylov method
            
            // 3. Absorb C into the next site's tensor to move the center
            //    Perform QR decomposition on the evolved tensor
            A_new, C_new = qr_decomposition(C_evolved)
            
            MPS[j] = A_new        // Update the now left-canonical tensor at site j
            C = C_new             // This is the new center tensor for site j+1
            
            // 4. Update the left environment for the next step
            L_envs[j] = update_left_environment(L_envs[j-1], MPS[j], H_MPO[j])

        // At this point, j=N. Evolve the last site
        H_eff_N = build_effective_H(L_envs[N-1], R_envs[N+1], H_MPO[N])
        C_evolved = solve_linear_equation(exp(-i * H_eff_N * dt), C) // Full dt step for the turn-around
        MPS[N] = C_evolved // The whole MPS is now left-canonical

        // BACKWARD SWEEP (evolve by -dt/2, but we implement it as a forward evolution of another dt/2)
        C = MPS[N] // Center is now at the last site
        MPS[N] = null

        for j = N down to 2:
            // 1. Construct effective Hamiltonian
            H_eff = build_effective_H(L_envs[j-1], R_envs[j+1], H_MPO[j])

            // 2. Evolve the center tensor C
            C_evolved = solve_linear_equation(exp(-i * H_eff * dt/2), C)
            
            // 3. Absorb C into the previous site's tensor
            //    Perform LQ decomposition on the evolved tensor
            C_new, A_new = lq_decomposition(C_evolved)

            MPS[j] = A_new       // Update the now right-canonical tensor at site j
            C = C_new            // This is the new center tensor for site j-1

            // 4. Update the right environment for the next sweep
            R_envs[j] = update_right_environment(R_envs[j+1], MPS[j], H_MPO[j])

        // At this point, j=1. Evolve the first site
        H_eff_1 = build_effective_H(L_envs[0], R_envs[2], H_MPO[1])
        C_evolved = solve_linear_equation(exp(-i * H_eff_1 * dt/2), C)
        MPS[1] = C_evolved // The whole MPS is now right-canonical again
        
        // For the next full time step, reset the center to the left
        C = MPS[0]
        MPS[0] = null

    return MPS
```

# TDVP vs. TEBD

This document summarizes our conversation comparing the Time-Dependent Variational Principle (TDVP) and the Time-Evolving Block Decimation (TEBD) algorithms for simulating time evolution in tensor networks.

## 1. High-Level Overview

Both TDVP and TEBD are powerful algorithms for evolving Matrix Product States (MPS) in time. However, they are built on fundamentally different principles.

* **TDVP** is a **variational** method that evolves the state by projecting the Schrödinger equation onto the MPS manifold. It is more general and powerful, especially for complex Hamiltonians.
* **TEBD** is a **direct simulation** method based on decomposing the time-evolution operator ($e^{-iHt}$) into a sequence of local gates using a Trotter-Suzuki approximation. It is simpler and faster for its specific use case.

## 2. Core Principles: Projection vs. Decomposition

The primary difference lies in their approach to the evolution.

### TDVP: Variational Projection
* **The Idea:** Instead of evolving the state and having it leave the manageable MPS manifold, TDVP finds the *best possible approximation* of the evolution that remains on the manifold at all times.
* **The Formulism:** It solves the projected Schrödinger equation: 
    $$i \frac{d}{dt} |\Psi\rangle = P_{T} H |\Psi\rangle$$
    where $P_{T}$ is the projector onto the tangent space of the MPS manifold.
* **The Implementation:** This minimization problem is analytically solved by the projection. The resulting differential equation is then solved numerically via a sweep-based algorithm (similar to DMRG) that applies local effective Hamiltonians.

### TEBD: Trotter Decomposition
* **The Idea:** Directly approximate the global time-evolution operator as a product of simple, local operators (gates) that are easier to apply.
* **The Formulism:** It uses the Lie-Trotter-Suzuki decomposition. For a nearest-neighbor Hamiltonian $H = H_{even} + H_{odd}$, the approximation is:
    $$e^{-iHt} \approx \left( e^{-iH_{even}\delta t} e^{-iH_{odd}\delta t} \right)^{t/\delta t}$$
* **The Implementation:** This becomes a quantum circuit applied to the MPS. The algorithm applies two-site gates sequentially across the chain, truncating the bond dimension via SVD after each step to keep the state manageable.

## 3. Detailed Comparison Table

| Feature                | **TDVP (Time-Dependent Variational Principle)**                                              | **TEBD (Time-Evolving Block Decimation)**                                                                                                                        |
| :--------------------- | :------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Hamiltonian Type**   | **General (Long-Range)**. Naturally handles any Hamiltonian representable as an MPO.         | **Nearest-Neighbor**. Standard version is restricted to local interactions.                                                                                      |
| **MPO Role**           | ***Essential Input.*** The Hamiltonian must be provided as an MPO.                           | ***Not Strictly Necessary.*** Basic TEBD only needs a list of local `h` terms. The MPO is a formal framework, not a practical requirement for the standard case. |
| **Source(s) of Error** | **Projection Error:** From approximating the true evolution within a fixed manifold.         | 1. **Trotter Error:** From the operator decomposition.<br>2. **Truncation Error:** From the SVD at each step.                                                    |
| **Conservation Laws**  | **Excellent.** 1-site TDVP exactly conserves energy and norm by construction.                | **Approximate.** Energy is not strictly conserved due to Trotterization and truncation.                                                                          |
| **Main Advantage**     | **Generality & Accuracy.** The go-to method for complex Hamiltonians.                        | **Simplicity & Speed.** Very efficient for 1D nearest-neighbor models.                                                                                           |
| **Main Disadvantage**  | **Complexity.** Can be harder to implement and reason about. 1-site version can get "stuck." | **Limited Scope.** Fails for long-range interactions without significant modifications.                                                                          |

## 4. When to Use Which?

* **Use TEBD if:**
    * You are simulating a 1D system.
    * Your Hamiltonian has **only nearest-neighbor interactions**.
    * You want a fast and conceptually straightforward implementation for this case.

* **Use TDVP if:**
    * Your Hamiltonian has **long-range or multi-site interactions**.
    * You need to simulate systems in 2D (by mapping them to a 1D path).
    * Precise **energy conservation** is a critical requirement for your simulation.

In essence, TDVP is the more modern, powerful, and versatile tool, whereas TEBD remains an elegant and efficient algorithm for the important subset of problems for which it was designed.

# Main body of paper
![[Pasted image 20250606114708.png]]
