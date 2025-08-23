- [chat with gemini](https://g.co/gemini/share/c7d1b7f0ec3c) 

# Bloch's Theorem: Proof from Schrödinger Equation Group Theory Perspective

## I. Premise: The Schrödinger Equation in a Periodic Potential

The time-independent Schrödinger equation for an electron in a crystal:
$$\hat{H}\psi(\mathbf{r}) = E\psi(\mathbf{r})$$
where the Hamiltonian $\hat{H}$ is given by:
$$\hat{H} = -\frac{\hbar^2}{2m}\nabla^2 + V(\mathbf{r})$$
The crucial aspect is the **periodicity of the potential**:
$$V(\mathbf{r} + \mathbf{R}) = V(\mathbf{r}) \quad \text{for any lattice vector } \mathbf{R}$$

## II. Step 1: Introduce the Translation Operator

Define the translation operator $\hat{T}_{\mathbf{R}}$:
$$\hat{T}_{\mathbf{R}}f(\mathbf{r}) = f(\mathbf{r}+\mathbf{R})$$

## III. Step 2: Show that $\hat{T}_{\mathbf{R}}$ Commutes with $\hat{H}$

We need to demonstrate that $[\hat{H}, \hat{T}_{\mathbf{R}}] = 0$.

* **Kinetic Energy Term:**
    The kinetic energy operator $(-\frac{\hbar^2}{2m}\nabla^2)$ acts on the coordinates. Translating the coordinate system ($\mathbf{r} \to \mathbf{r}+\mathbf{R}$) does not change the form of the Laplacian operator itself.
    So, $\hat{T}_{\mathbf{R}}(-\frac{\hbar^2}{2m}\nabla^2)\psi(\mathbf{r}) = -\frac{\hbar^2}{2m}\nabla^2\psi(\mathbf{r}+\mathbf{R}) = (-\frac{\hbar^2}{2m}\nabla^2)\hat{T}_{\mathbf{R}}\psi(\mathbf{r})$.
    Thus, $(-\frac{\hbar^2}{2m}\nabla^2)$ commutes with $\hat{T}_{\mathbf{R}}$.

* **Potential Energy Term:**
    $\hat{T}_{\mathbf{R}}(V(\mathbf{r})\psi(\mathbf{r})) = V(\mathbf{r}+\mathbf{R})\psi(\mathbf{r}+\mathbf{R})$.
    Due to the periodicity of the potential, $V(\mathbf{r}+\mathbf{R}) = V(\mathbf{r})$.
    Therefore, $\hat{T}_{\mathbf{R}}(V(\mathbf{r})\psi(\mathbf{r})) = V(\mathbf{r})\psi(\mathbf{r}+\mathbf{R}) = V(\mathbf{r})\hat{T}_{\mathbf{R}}\psi(\mathbf{r})$.
    Thus, $V(\mathbf{r})$ commutes with $\hat{T}_{\mathbf{R}}$.

Since both parts of the Hamiltonian commute with $\hat{T}_{\mathbf{R}}$, the full Hamiltonian commutes with $\hat{T}_{\mathbf{R}}$:
$$[\hat{H}, \hat{T}_{\mathbf{R}}] = 0$$

## IV. Step 3: Implications of Commutation

If two operators commute, they share a common set of eigenfunctions. This means that the eigenfunctions of $\hat{H}$ (i.e., the crystal wave functions $\psi(\mathbf{r})$) can also be chosen to be eigenfunctions of $\hat{T}_{\mathbf{R}}$.

## V. Step 4: Find the Eigenvalues of $\hat{T}_{\mathbf{R}}$

Let $\psi(\mathbf{r})$ be an eigenfunction of $\hat{T}_{\mathbf{R}}$ with eigenvalue $\lambda_{\mathbf{R}}$:
$$\hat{T}_{\mathbf{R}}\psi(\mathbf{r}) = \lambda_{\mathbf{R}}\psi(\mathbf{r})$$
$$\implies \psi(\mathbf{r}+\mathbf{R}) = \lambda_{\mathbf{R}}\psi(\mathbf{r})$$

Consider successive translations:
$$\hat{T}_{\mathbf{R}_1+\mathbf{R}_2} = \hat{T}_{\mathbf{R}_1}\hat{T}_{\mathbf{R}_2}$$
Applying this to the eigenvalues:
$$\lambda_{\mathbf{R}_1+\mathbf{R}_2} = \lambda_{\mathbf{R}_1}\lambda_{\mathbf{R}_2}$$
This property is characteristic of exponential functions. We can therefore write $\lambda_{\mathbf{R}}$ in the form:
$$\lambda_{\mathbf{R}} = e^{i\mathbf{k} \cdot \mathbf{R}}$$
where $\mathbf{k}$ is a real vector (the wave vector). The magnitude of the eigenvalue must be 1 ($|\lambda_{\mathbf{R}}|^2 = 1$) to preserve the normalization of the wave function under translation, implying the exponent is purely imaginary.

## VI. Step 5: Deriving the Bloch Form

Substitute the eigenvalue back into the equation from Step 4:
$$\psi(\mathbf{r}+\mathbf{R}) = e^{i\mathbf{k} \cdot \mathbf{R}}\psi(\mathbf{r})$$
Now, define a new function $u_k(\mathbf{r})$:
$$u_k(\mathbf{r}) = e^{-i\mathbf{k} \cdot \mathbf{r}}\psi(\mathbf{r})$$
Let's check the periodicity of $u_k(\mathbf{r})$:
$$u_k(\mathbf{r}+\mathbf{R}) = e^{-i\mathbf{k} \cdot (\mathbf{r}+\mathbf{R})}\psi(\mathbf{r}+\mathbf{R})$$
$$u_k(\mathbf{r}+\mathbf{R}) = e^{-i\mathbf{k} \cdot \mathbf{r}}e^{-i\mathbf{k} \cdot \mathbf{R}} (e^{i\mathbf{k} \cdot \mathbf{R}}\psi(\mathbf{r}))$$
$$u_k(\mathbf{r}+\mathbf{R}) = e^{-i\mathbf{k} \cdot \mathbf{r}}\psi(\mathbf{r}) = u_k(\mathbf{r})$$
This confirms that $u_k(\mathbf{r})$ is a periodic function with the same periodicity as the crystal lattice.

Rearranging the definition of $u_k(\mathbf{r})$ gives the famous **Bloch Wave Function**:
$$\psi_k(\mathbf{r}) = e^{i\mathbf{k} \cdot \mathbf{r}} u_k(\mathbf{r})$$

## VII. Conclusion 1: Bloch's Theorem

**Bloch's Theorem states that the eigenfunctions of the Schrödinger equation for a periodic potential can be written as a plane wave $e^{i\mathbf{k} \cdot \mathbf{r}}$ multiplied by a periodic function $u_k(\mathbf{r})$ that has the same periodicity as the crystal lattice.**

## VIII. Conclusion 2: Equivalence of $\mathbf{k}$ and $\mathbf{k}+\mathbf{G}$

Consider a wave vector $\mathbf{k}' = \mathbf{k} + \mathbf{G}$, where $\mathbf{G}$ is a reciprocal lattice vector. By definition of a reciprocal lattice vector:
$$\mathbf{G} \cdot \mathbf{R} = 2\pi n \quad (\text{where } n \text{ is an integer})$$
This implies:
$$e^{i\mathbf{G} \cdot \mathbf{R}} = 1$$

Now, let's examine the translation property for $\psi_{\mathbf{k}+\mathbf{G}}(\mathbf{r})$:
$$\psi_{\mathbf{k}+\mathbf{G}}(\mathbf{r}+\mathbf{R}) = e^{i(\mathbf{k}+\mathbf{G}) \cdot \mathbf{R}} \psi_{\mathbf{k}+\mathbf{G}}(\mathbf{r})$$
$$= e^{i\mathbf{k} \cdot \mathbf{R}} e^{i\mathbf{G} \cdot \mathbf{R}} \psi_{\mathbf{k}+\mathbf{G}}(\mathbf{r})$$
Since $e^{i\mathbf{G} \cdot \mathbf{R}} = 1$:
$$\psi_{\mathbf{k}+\mathbf{G}}(\mathbf{r}+\mathbf{R}) = e^{i\mathbf{k} \cdot \mathbf{R}} \psi_{\mathbf{k}+\mathbf{G}}(\mathbf{r})$$
This shows that $\psi_{\mathbf{k}+\mathbf{G}}(\mathbf{r})$ satisfies the *exact same eigenvalue equation* for the translation operator as $\psi_{\mathbf{k}}(\mathbf{r})$. They correspond to the same set of Bloch eigenvalues ($e^{i\mathbf{k} \cdot \mathbf{R}}$).
specifically, we have
$$
e^{ i (\mathbf{k+G})\cdot (\mathbf{r+R}) } u_{\mathbf{k+G}}(\mathbf{r+R}) = e^{ i \mathbf{k}\cdot \mathbf{R} + (\mathbf{k+G})\cdot \mathbf{r} } u_{\mathbf{k+G}}(\mathbf{r})
$$
Therefore, physically, the states described by $\mathbf{k}$ and $\mathbf{k}+\mathbf{G}$ are indistinguishable. This allows us to restrict the range of $\mathbf{k}$ vectors to a fundamental region, the **First Brillouin Zone**, when describing the electronic band structure. All other $\mathbf{k}$ vectors outside this zone are equivalent to a $\mathbf{k}$ within it.

**in the same band index, the $\psi_{k}$ and $\psi_{k+G}$ has the same eigenvalue $e^{ i k \cdot R }$ for $T_{\mathbf{R}}$, while same eigenvalue $E(k)=E(k+G)$ for $H$, then the 2 state must be the same(with no other sym probability).**

another approach to these answer is explicit Fourier analysis. 

# Bloch's Theorem via Fourier Analysis

This approach demonstrates how the periodicity of the crystal potential naturally leads to the Bloch form of the wave function and the periodicity of energy bands in reciprocal space.

## I. Premise: The Schrödinger Equation in a Periodic Potential

The time-independent Schrödinger equation for an electron in a crystal:
$$-\frac{\hbar^2}{2m}\nabla^2\psi(\mathbf{r}) + V(\mathbf{r})\psi(\mathbf{r}) = E\psi(\mathbf{r})$$
The potential $V(\mathbf{r})$ is periodic, meaning:
$$V(\mathbf{r} + \mathbf{R}) = V(\mathbf{r}) \quad \text{for any lattice vector } \mathbf{R}$$

## II. Fourier Expansion of the Periodic Potential

Since $V(\mathbf{r})$ is periodic, its Fourier expansion contains only terms corresponding to **reciprocal lattice vectors $\mathbf{G}$**. The set of all reciprocal lattice vectors is denoted by $\{\mathbf{G}\}$.
$$V(\mathbf{r}) = \sum_{\mathbf{G}} V_{\mathbf{G}} e^{i\mathbf{G} \cdot \mathbf{r}}$$
where $V_{\mathbf{G}}$ are the Fourier coefficients of the potential.

## III. Fourier Expansion of the Wave Function

We assume the wave function $\psi(\mathbf{r})$ can also be expressed as a Fourier sum. Due to the coupling introduced by the periodic potential, we'll see that only specific wave vectors will have non-zero coefficients.
$$\psi(\mathbf{r}) = \sum_{\mathbf{q}} \psi_{\mathbf{q}} e^{i\mathbf{q} \cdot \mathbf{r}}$$
where $\psi_{\mathbf{q}}$ are the Fourier coefficients of the wave function. The sum over $\mathbf{q}$ generally runs over all possible wave vectors in Fourier space.

## IV. Substituting Expansions into the Schrödinger Equation

Substitute the Fourier expansions of $V(\mathbf{r})$ and $\psi(\mathbf{r})$ into the Schrödinger equation:

$$-\frac{\hbar^2}{2m}\nabla^2 \left( \sum_{\mathbf{q}} \psi_{\mathbf{q}} e^{i\mathbf{q} \cdot \mathbf{r}} \right) + \left( \sum_{\mathbf{G}} V_{\mathbf{G}} e^{i\mathbf{G} \cdot \mathbf{r}} \right) \left( \sum_{\mathbf{q}'} \psi_{\mathbf{q}'} e^{i\mathbf{q}' \cdot \mathbf{r}} \right) = E \sum_{\mathbf{q}} \psi_{\mathbf{q}} e^{i\mathbf{q} \cdot \mathbf{r}}$$

Let's evaluate each term:

1.  **Kinetic Energy Term:**
    The Laplacian operator acts on $e^{i\mathbf{q} \cdot \mathbf{r}}$ as $\nabla^2 e^{i\mathbf{q} \cdot \mathbf{r}} = -\mathbf{q}^2 e^{i\mathbf{q} \cdot \mathbf{r}}$.
    $$-\frac{\hbar^2}{2m}\nabla^2 \left( \sum_{\mathbf{q}} \psi_{\mathbf{q}} e^{i\mathbf{q} \cdot \mathbf{r}} \right) = \sum_{\mathbf{q}} \frac{\hbar^2 |\mathbf{q}|^2}{2m} \psi_{\mathbf{q}} e^{i\mathbf{q} \cdot \mathbf{r}}$$

2.  **Potential Energy Term:**
    This term involves a product of two Fourier series, which results in a convolution in Fourier space:
    $$\left( \sum_{\mathbf{G}} V_{\mathbf{G}} e^{i\mathbf{G} \cdot \mathbf{r}} \right) \left( \sum_{\mathbf{q}'} \psi_{\mathbf{q}'} e^{i\mathbf{q}' \cdot \mathbf{r}} \right) = \sum_{\mathbf{G}} \sum_{\mathbf{q}'} V_{\mathbf{G}} \psi_{\mathbf{q}'} e^{i(\mathbf{G}+\mathbf{q}') \cdot \mathbf{r}}$$
    To simplify the sums, let's redefine the summation variable. Let $\mathbf{q} = \mathbf{G} + \mathbf{q}'$. Then $\mathbf{q}' = \mathbf{q} - \mathbf{G}$.
    The sum now becomes:
    $$\sum_{\mathbf{q}} \sum_{\mathbf{G}} V_{\mathbf{G}} \psi_{\mathbf{q}-\mathbf{G}} e^{i\mathbf{q} \cdot \mathbf{r}}$$
    (Note: The sum over $\mathbf{G}$ now couples different $\psi_{\mathbf{q}}$ coefficients).

3.  **Putting it all together:**
    Substitute the expanded terms back into the Schrödinger equation:
    $$\sum_{\mathbf{q}} \frac{\hbar^2 |\mathbf{q}|^2}{2m} \psi_{\mathbf{q}} e^{i\mathbf{q} \cdot \mathbf{r}} + \sum_{\mathbf{q}} \sum_{\mathbf{G}} V_{\mathbf{G}} \psi_{\mathbf{q}-\mathbf{G}} e^{i\mathbf{q} \cdot \mathbf{r}} = E \sum_{\mathbf{q}} \psi_{\mathbf{q}} e^{i\mathbf{q} \cdot \mathbf{r}}$$

## V. Equating Coefficients and Deriving Coupled Equations

For the equality to hold for all $\mathbf{r}$, the coefficient of each $e^{i\mathbf{q} \cdot \mathbf{r}}$ term must be zero when rearranged:
$$\sum_{\mathbf{q}} \left( \frac{\hbar^2 |\mathbf{q}|^2}{2m} \psi_{\mathbf{q}} + \sum_{\mathbf{G}} V_{\mathbf{G}} \psi_{\mathbf{q}-\mathbf{G}} - E \psi_{\mathbf{q}} \right) e^{i\mathbf{q} \cdot \mathbf{r}} = 0$$
This implies that the expression in the parenthesis must be zero for every $\mathbf{q}$:
$$\left( \frac{\hbar^2 |\mathbf{q}|^2}{2m} - E \right) \psi_{\mathbf{q}} + \sum_{\mathbf{G}} V_{\mathbf{G}} \psi_{\mathbf{q}-\mathbf{G}} = 0$$
This is a set of **coupled linear equations** for the Fourier coefficients $\psi_{\mathbf{q}}$.

## VI. Deriving the Bloch Form

The coupled equations reveal a crucial property: if a particular coefficient $\psi_{\mathbf{q}_0}$ is non-zero, then this equation implies that $\psi_{\mathbf{q}_0}$ is coupled only to coefficients $\psi_{\mathbf{q}_0 - \mathbf{G}}$ for all reciprocal lattice vectors $\mathbf{G}$.
This means that for a non-trivial solution $\psi(\mathbf{r})$, its Fourier expansion can *only* contain wave vectors that differ from some initial wave vector (let's call it $\mathbf{k}$) by a reciprocal lattice vector.
Therefore, the Fourier expansion of $\psi(\mathbf{r})$ must be of the form:
$$\psi(\mathbf{r}) = \sum_{\mathbf{G}'} \psi_{\mathbf{k}+\mathbf{G}'} e^{i(\mathbf{k}+\mathbf{G}') \cdot \mathbf{r}}$$
Here, $\mathbf{G}'$ runs over all reciprocal lattice vectors, and $\psi_{\mathbf{k}+\mathbf{G}'}$ are the coefficients of these specific components.

We can factor out $e^{i\mathbf{k} \cdot \mathbf{r}}$ from the sum:
$$\psi(\mathbf{r}) = e^{i\mathbf{k} \cdot \mathbf{r}} \left( \sum_{\mathbf{G}'} \psi_{\mathbf{k}+\mathbf{G}'} e^{i\mathbf{G}' \cdot \mathbf{r}} \right)$$
Now, we define the periodic part $u_k(\mathbf{r})$ as the sum in the parenthesis:
$$u_k(\mathbf{r}) = \sum_{\mathbf{G}'} \psi_{\mathbf{k}+\mathbf{G}'} e^{i\mathbf{G}' \cdot \mathbf{r}}$$
To verify its periodicity, substitute $\mathbf{r}+\mathbf{R}$:
$$u_k(\mathbf{r}+\mathbf{R}) = \sum_{\mathbf{G}'} \psi_{\mathbf{k}+\mathbf{G}'} e^{i\mathbf{G}' \cdot (\mathbf{r}+\mathbf{R})} = \sum_{\mathbf{G}'} \psi_{\mathbf{k}+\mathbf{G}'} e^{i\mathbf{G}' \cdot \mathbf{r}} e^{i\mathbf{G}' \cdot \mathbf{R}}$$
Since $\mathbf{G}'$ is a reciprocal lattice vector and $\mathbf{R}$ is a real space lattice vector, $e^{i\mathbf{G}' \cdot \mathbf{R}} = 1$.
$$u_k(\mathbf{r}+\mathbf{R}) = \sum_{\mathbf{G}'} \psi_{\mathbf{k}+\mathbf{G}'} e^{i\mathbf{G}' \cdot \mathbf{r}} (1) = u_k(\mathbf{r})$$
This confirms that $u_k(\mathbf{r})$ is indeed periodic with the crystal lattice.

Thus, we arrive at the **Bloch wave function**:
$$\psi_k(\mathbf{r}) = e^{i\mathbf{k} \cdot \mathbf{r}} u_k(\mathbf{r})$$

## VII. Relationship between $\psi_k(\mathbf{r})$ and $\psi_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r})$

From the coupled equations, it is observed that the set of equations for coefficients $\psi_{\mathbf{k}+\mathbf{G}'}$ determines the energy $E(\mathbf{k})$. If we shift the chosen wave vector from $\mathbf{k}$ to $\mathbf{k}+\mathbf{G}_{\text{fixed}}$ (where $\mathbf{G}_{\text{fixed}}$ is a specific reciprocal lattice vector), the resulting set of coupled equations will be identical in form, just indexed differently. This implies that the energy eigenvalue is periodic in reciprocal space:
$$E(\mathbf{k}) = E(\mathbf{k}+\mathbf{G})$$
for any reciprocal lattice vector $\mathbf{G}$.

Since they have the same energy eigenvalue and come from the same physical system, the wave functions $\psi_k(\mathbf{r})$ and $\psi_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r})$ represent the same physical state. Therefore:
$$\psi_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r}) = \psi_k(\mathbf{r})$$

Now, let's explicitly derive the relationship between their periodic parts using their Fourier sums:

1.  **Fourier Sum for $u_k(\mathbf{r})$:**
    $$u_k(\mathbf{r}) = \sum_{\mathbf{G}'} \psi_{\mathbf{k}+\mathbf{G}'} e^{i\mathbf{G}' \cdot \mathbf{r}}$$

2.  **Fourier Sum for $u_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r})$:**
    Similarly, for $\psi_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r})$:
    $$\psi_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r}) = \sum_{\mathbf{G}''} \psi_{(\mathbf{k}+\mathbf{G}_{\text{fixed}})+\mathbf{G}''} e^{i((\mathbf{k}+\mathbf{G}_{\text{fixed}})+\mathbf{G}'') \cdot \mathbf{r}}$$
    From its Bloch form:
    $$\psi_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r}) = e^{i(\mathbf{k}+\mathbf{G}_{\text{fixed}}) \cdot \mathbf{r}} u_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r})$$
    Comparing the last two lines, we get:
    $$u_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r}) = \sum_{\mathbf{G}''} \psi_{(\mathbf{k}+\mathbf{G}_{\text{fixed}})+\mathbf{G}''} e^{i\mathbf{G}'' \cdot \mathbf{r}}$$

3.  **Relating the two periodic parts:**
    Since $\psi_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r}) = \psi_k(\mathbf{r})$, their Fourier coefficients must be equal:
    $$\psi_{(\mathbf{k}+\mathbf{G}_{\text{fixed}})+\mathbf{G}''} = \psi_{\mathbf{k}+(\mathbf{G}_{\text{fixed}}+\mathbf{G}'')}$$
    Let $\mathbf{G}' = \mathbf{G}_{\text{fixed}}+\mathbf{G}''$. Then $\mathbf{G}'' = \mathbf{G}' - \mathbf{G}_{\text{fixed}}$. Substituting this into the sum for $u_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r})$:
    $$u_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r}) = \sum_{\mathbf{G}'} \psi_{\mathbf{k}+\mathbf{G}'} e^{i(\mathbf{G}' - \mathbf{G}_{\text{fixed}}) \cdot \mathbf{r}}$$
    $$u_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r}) = \sum_{\mathbf{G}'} \psi_{\mathbf{k}+\mathbf{G}'} e^{i\mathbf{G}' \cdot \mathbf{r}} e^{-i\mathbf{G}_{\text{fixed}} \cdot \mathbf{r}}$$
    Factor out the term $e^{-i\mathbf{G}_{\text{fixed}} \cdot \mathbf{r}}$ (which is independent of $\mathbf{G}'$):
    $$u_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r}) = e^{-i\mathbf{G}_{\text{fixed}} \cdot \mathbf{r}} \left( \sum_{\mathbf{G}'} \psi_{\mathbf{k}+\mathbf{G}'} e^{i\mathbf{G}' \cdot \mathbf{r}} \right)$$
    The term in the parenthesis is precisely $u_k(\mathbf{r})$.
    Therefore:
    $$u_{\mathbf{k}+\mathbf{G}_{\text{fixed}}}(\mathbf{r}) = e^{-i\mathbf{G}_{\text{fixed}} \cdot \mathbf{r}} u_{\mathbf{k}}(\mathbf{r})$$

This confirms the relationship between the periodic parts derived from the fundamental identity of the total wave functions.