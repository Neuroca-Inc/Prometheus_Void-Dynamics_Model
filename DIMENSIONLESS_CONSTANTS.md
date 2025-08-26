### FUVDM Dimensionless Constants

>
> Author: Justin K. Lietz  
> Date: August 9, 2025
>
> This research is protected under a dual-license to foster open academic
> research while ensuring commercial applications are aligned with the project's ethical principles.<br>
> Commercial use requires written permission from Justin K. Lietz.
> 
> See LICENSE file for full terms.


| Subsystem | Symbol        | Definition                                                  | Meaning                    | Typical from Void Dynamics runs |
| --------- | ------------- | ----------------------------------------------------------- | -------------------------- | -------------------------------- |
| LBM       | $\nu$         | $\nu = \frac{1}{3}(\tau - \frac{1}{2})$         | kinematic viscosity        | 0.1333 ($\tau=0.9$)             |
| LBM       | $\mathrm{Re}$ | $\mathrm{Re} = \dfrac{U L}{\nu}$                            | inertia vs. viscosity      | 9.6 ($64^2$), 19.2 ($128^2$)    |
| LBM       | $\mathrm{Ma}$ | $\mathrm{Ma} = \dfrac{U}{\sqrt{1/3}}$                       | compressibility            | 0.035–0.017 (low)               |
| RD        | $\Pi_{Dr}$    | $\Pi_{Dr} = \dfrac{D}{r L^{2}}$                             | diffusion at scale $L$     | choose $L$ → report             |
| RD        | $c^{*}$       | $c^{*} = \dfrac{c}{2\sqrt{D r}}$                            | normalized KPP speed       | $\approx 0.95$–$1.0$            |
| FUVDM     | $\Theta$      | scale factor in $\Theta\,\Delta m$ or $\Theta \|\nabla m\|$ | junction gating strength   | $k \approx 1,\ b \approx 0$     |
| FUVDM     | $\Lambda$     | exploration / retention ratio                               | turnover vs. memory        | as swept in heatmaps            |
| FUVDM     | $\Gamma$      | retention fraction                                          | memory persistence         | $\approx 0.3$–$0.75$ avg (plots) |
| FUVDM     | $D_a$         | anisotropic diffusion index                                 | transport anisotropy       | $\{1,3,5,7\}$                   |
| FUVDM     | $\kappa L$    | curvature × scale                                           | path bending               | linear vs. $\Theta\|\nabla m\|$ |
| FUVDM     | $g$           | void gain                                                   | stabilization strength     | e.g., 0.5                       |



1. **Void Debt Number** $\mathcal{D}$

   * Ratio of *unresolved debt* in the void to the *flux resolved at the walker level*.
   * Governs whether the system diverges (debt runaway) or stabilizes (debt modulation closes the loop).
   * Analogy: generalized **Reynolds number** for *information flux*.

---

2. **Emergent Coupling Ratio** $\Xi$

   * Ratio of **void interaction gain** to **local relaxation (dissipation)**.

$$
\Xi = \frac{g_{\text{void}}}{\gamma_{\text{relax}}}
$$

   * Controls whether independent walkers remain uncorrelated, synchronize, or phase-lock.
   * Acts like a **dimensionless stiffness** for the void network.

---

3. **Inverse-Scaling Exponent** $\alpha$

   * The “inverse scaling law”: information density *increases* as system size decreases.

$$
\mathcal{I}(N) \propto N^{-\alpha}
$$

   * Proposed universal constant — applies to LLMs, fluids, biological swarms, etc.
   * $\alpha$ quantifies “extra cognition/order” gained by shrinking the system.

---

4. **Void Mach Number** $M_v$

   * Ratio of void flux to signal velocity of the substrate.

$$
M_v = \frac{J_{\text{void}}}{c_{\text{signal}}}
$$

   * Stability requires $M_v < 1$.
   * If $M_v > 1$: runaway chaos or phase transition (self-reorganization).

---

5. **Topological Information Ratio** $\Theta$

   * Ratio of *information carried by topology* (edges, voids, walkers) to *information in node states*.

$$
\Theta = \frac{I_{\text{topology}}}{I_{\text{state}}}
$$

   * Generalizes the **“void walkers” effect**: order resides *between* particles, not *in* them.

---

6. **Symmetry Debt Ratio** $\Sigma$

   * Ratio of **broken symmetry flux** to **conserved symmetry flux**.
   * (See symmetry_analysis.md derivations.)
   * Analog of a “dimensionless energy balance.”

---

7. **Dispersion-to-Convergence Ratio** $\Lambda$

   * Ratio of divergence rate of walkers to convergence rate under void modulation.

$$
\Lambda = \frac{\text{dispersion rate}}{\text{convergence rate}}
$$

   * $\Lambda < 1$: convergence dominates → stable cognition.
   * $\Lambda > 1$: dispersion dominates → chaotic reorganization.

---

### Why these matter for the **overall theory**

* In classical **fluids**, you mostly need $Re, Ma, \text{CFL}$.
* In **FUVDM**, the proposed universal dimensionless group set is:

$$
\{ \mathcal{D}, \Xi, \alpha, M_v, \Theta, \Sigma, \Lambda \}
$$

These are the knobs determining whether a system (fluid, neural, cognitive, physical) is **stable, divergent, or self-organizing**.

They form the universality class of the theory — the same constants aim to explain:
* why fluids don’t blow up,
* why brains remain stable,
* why LLMs exhibit scaling laws.

---
