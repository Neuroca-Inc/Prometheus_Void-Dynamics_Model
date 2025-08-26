# Derivation of the FUM Kinetic Term

**Author:** Justin K. Lietz  
**Date:** August 8, 2025

---

### 1. Objective

As outlined in our Effective Field Theory (EFT) roadmap, we must rigorously derive the coefficients of the general Lagrangian from the underlying discrete FUM simulation. Earlier work separated temporal and spatial (interaction) contributions.

The objective of this document is to derive the kinetic prefactor (wave‑function normalization) $Z(\phi)$ and show it is a constant, $Z(\phi)=\tfrac{1}{2}$, consistent with a canonical Klein–Gordon–type scalar field. We start from the discrete temporal “kinetic energy” and nearest‑neighbor interaction, take the continuum limit, and match to the continuum Lagrangian density.

---

### 2. Temporal Kinetic Term

The temporal part of the kinetic term arises from the discrete “kinetic energy” (see `derivation/discrete_conservation.md`):

$$
\mathcal{K}_i = \frac{1}{2}\left(\frac{dW_i}{dt}\right)^2
$$

with the discrete time derivative

$$
\frac{dW_i}{dt} = \frac{W_i(t+\Delta t) - W_i(t)}{\Delta t}.
$$

Continuum limit $W_i \to \phi(\mathbf{x},t)$, $\frac{dW_i}{dt} \to \partial_t \phi$:

$$
\mathcal{L}_{\text{kinetic, temporal}} = \frac{1}{2}(\partial_t \phi)^2.
$$

So the coefficient of $(\partial_t \phi)^2$ is already $1/2$.

---

### 3. Spatial Kinetic (Gradient) Term

The spatial contribution comes from the discrete interaction energy:

$$
\mathcal{I}i = \tfrac{1}{2} \sum{j \in N(i)} J \big(W_j - W_i\big)^2
$$

This penalizes sharp spatial variations.

#### 3.1 Continuum Limit via Taylor Expansion

Approximate the local k‑NN structure by a regular cubic lattice (spacing $a$, dimension $d=3$). Let site $i$ be at $\mathbf{x}$; neighbors lie at $\mathbf{x} \pm a \hat{e}_k$, $k\in\{x,y,z\}$.

Taylor expand:

$$
W(\mathbf{x}+a\hat{e}_k) = W(\mathbf{x}) + a\,\partial_k W(\mathbf{x}) + \frac{a^2}{2}\partial_k^2 W(\mathbf{x}) + O(a^3).
$$

Difference:

$$
W(\mathbf{x}+a\hat{e}_k) - W(\mathbf{x}) = a\,\partial_k W + \frac{a^2}{2}\partial_k^2 W + O(a^3).
$$

Lowest non‑vanishing order when squared:

$$
\big(W(\mathbf{x}+a\hat{e}_k) - W(\mathbf{x})\big)^2 = a^2 (\partial_k W)^2 + O(a^3).
$$

Similarly for the negative direction. Summing the 6 neighbors:

$$
\sum_{j \in N(i)} (W_j - W_i)^2 = 2 a^2 \sum_{k}( \partial_k W )^2 + O(a^3) = 2 a^2 (\nabla W)^2 + O(a^3).
$$

Insert into interaction energy and pass to the field $\phi$:

$$
\mathcal{I}_i \approx \frac{1}{2} J \left(2 a^2 (\nabla \phi)^2\right) = J a^2 (\nabla \phi)^2.
$$

Thus the spatial gradient term appears with coefficient $J a^2$.

#### 3.2 Variational Derivation from a Discrete Action

Define:
- Lattice spacing $a$, dimension $d$.
- Time step $\Delta t$, times $t_n = n \Delta t$.
- Field $W_i^n = W(\mathbf{x}_i, t_n)$.
- Unit vectors $\hat{e}_\mu$, $\mu=1,\dots,d$.

Discrete Lagrangian per time step:

$$
L^n = a^d \sum_i \Bigg[ \frac{1}{2}\Big(\frac{W_i^{n+1}-W_i^{n}}{\Delta t}\Big)^2 - \frac{\kappa}{2} \sum_{\mu=1}^d \big(W_{i+\mu}^{n} - W_i^{n}\big)^2 - V(W_i^{n}) \Bigg]
$$

Discrete Euler–Lagrange:

$$
\frac{W_i^{n+1} - 2 W_i^{n} + W_i^{n-1}}{(\Delta t)^2} - \kappa \sum_{\mu=1}^d \big(W_{i+\mu}^{n} + W_{i-\mu}^{n} - 2 W_i^{n}\big) + V'(W_i^{n}) = 0
$$

Continuum expansion:

$$
W_{i+\mu} + W_{i-\mu} - 2 W_i = a^2 \partial_\mu^2 \phi + O(a^4),
$$

yields

$$
\partial_t^2 \phi - \kappa a^2 \nabla^2 \phi + V'(\phi) = 0,
$$

from

$$
\mathcal{L} = \frac{1}{2}(\partial_t \phi)^2 - \frac{\kappa a^2}{2} (\nabla \phi)^2 - V(\phi).
$$

Edge‑counting conventions:
- Per undirected edge counted once: coefficient $\kappa$, wave speed $c^2 = \kappa a^2$.
- Per site with both $\pm\mu$ neighbors in a sum $\tfrac{1}{2}\sum_{j\in N(i)} J (W_j-W_i)^2$: $\kappa = 2J$, so $c^2 = 2 J a^2$.

---

### 4. Full Kinetic Term

Combining temporal and spatial pieces (signature $+ - - -$):

$$
\mathcal{L}_{K} = \frac{1}{2}(\partial_t \phi)^2 - J a^2 (\nabla \phi)^2.
$$

Define

$$
c^2 \equiv 2 J a^2 \quad (\text{equivalently } c^2 = \kappa a^2).
$$

Then

$$
\mathcal{L}_{K} = \frac{1}{2}(\partial_t \phi)^2 - \frac{c^2}{2}(\nabla \phi)^2,
$$

and the Euler–Lagrange equation (with potential) is

$$
\partial_t^2 \phi - c^2 \nabla^2 \phi + V'(\phi) = 0.
$$

One may set $c=1$ by a units rescaling; this does not alter $Z(\phi)$.

---

### 5. Conclusion

We have

$$
\mathcal{L}_{K} = \frac{1}{2}(\partial_t \phi)^2 - J a^2 (\nabla \phi)^2
= \frac{1}{2}(\partial_t \phi)^2 - \frac{c^2}{2}(\nabla \phi)^2,
\qquad c^2 = 2 J a^2.
$$

Thus the kinetic normalization is constant: $Z(\phi)=\tfrac{1}{2}$. No field‑dependent prefactor emerges from the discrete nearest‑neighbor quadratic form.

---

### 6. Conventions Summary

- Per‑site coupling form (both directions): $c^2 = 2 J a^2$.
- Per‑edge single count: $c^2 = \kappa a^2$ with $\kappa = 2J$.
- Canonical relativistic form follows by choosing $c=1$.

---

### 7. Possible Extensions

- Anisotropy: $c_k^2 = 2 J_k a_k^2$.
- Higher‑order lattice corrections: keep $O(a^4)$ to estimate discretization error.
- Longer‑range couplings: induce higher derivative operators (e.g. $(\nabla^2 \phi)^2$) in an EFT expansion.
- Field‑dependent couplings $J(\phi)$: would generate non‑constant $Z(\phi)$.

---

End of document.
