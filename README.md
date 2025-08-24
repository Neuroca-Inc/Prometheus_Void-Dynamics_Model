# Void Dynamics (FUVDM) — Derivation Papers (Public Overview)

This folder contains the public, paper-only view of the Void Dynamics program. It provides theoretical derivations and validation write-ups intended for cold review by physicists, applied mathematicians, and scientifically minded engineers. No source code is included here yet, but will be after I've informed all priority insiders; the focus is on equations, assumptions, mappings, and acceptance criteria.

High-level summary
- Canonical baseline [PROVEN]: a reaction–diffusion (RD) layer used to anchor claims with reproducible dispersion and front-speed checks.
- Quarantined future work [PLAUSIBLE]: a second-order effective field theory (EFT/Klein–Gordon-like) branch kept separate until a full discrete action is completed and stress-tested.
- Scope discipline: each derivation file labels claims as [PROVEN]/[PLAUSIBLE]/[SPECULATIVE] and states numerical acceptance gates when applicable.

Why this relates to AI (at a high level)
- The project studies how simple, local physical laws can yield stable, interpretable global behavior under resource constraints. That lens is relevant to AI because:
  - Locality and event-driven updates parallel scalable AI systems that avoid heavy global passes.
  - Memory steering (separately documented) frames “routing bias” and retention/decay as slow fields over faster dynamics—an analogy to how AI systems can guide computation without opaque black-box shortcuts.
  - The emphasis on acceptance tests and dispersion/front-speed baselines mirrors how safety and evaluation can be grounded in measurable invariants rather than purely empirical heuristics.
- No AI training algorithms are presented here; the connection is conceptual and architectural, not a disclosure of implementation details.

What’s included (papers)
- Program overview and banner:
  - [FUVDM_Overview.md](Prometheus_FUVDM/derivation/FUVDM_Overview.md:1)
- Foundations:
  - [discrete_to_continuum.md](Prometheus_FUVDM/derivation/foundations/discrete_to_continuum.md:1)
  - [continuum_stack.md](Prometheus_FUVDM/derivation/foundations/continuum_stack.md:1)
- Reaction–Diffusion (canonical baseline):
  - [rd_front_speed_validation.md](Prometheus_FUVDM/derivation/reaction_diffusion/rd_front_speed_validation.md:1)
  - [rd_dispersion_validation.md](Prometheus_FUVDM/derivation/reaction_diffusion/rd_dispersion_validation.md:1)
  - [rd_validation_plan.md](Prometheus_FUVDM/derivation/reaction_diffusion/rd_validation_plan.md:1)
- Memory Steering (slow routing bias; separate layer):
  - [memory_steering.md](Prometheus_FUVDM/derivation/memory_steering/memory_steering.md:1)
- Finite-domain EFT modes (quarantined future work):
  - [finite_tube_mode_analysis.md](Prometheus_FUVDM/derivation/tachyon_condensation/finite_tube_mode_analysis.md:1)
- Change log / scoping notes:
  - [CORRECTIONS.md](Prometheus_FUVDM/derivation/CORRECTIONS.md:1)

What’s explicitly not included here
- Source code, executables, and private runtime harnesses.
- Generated logs/figures and any artifacts sufficient to reconstruct proprietary implementations.
- Any unreviewed drafts outside the derivation index above.

How to read these papers
- Each file follows a consistent structure: Purpose · Assumptions/Parameters · Discrete law · Continuum limit · PDE/Action/Potential · Fixed points & stability · Dispersion · Conservation/Lyapunov · Numerical plan + acceptance · Results · Open questions.
- Claims labeled [PROVEN] are those with sign checks, units, limit checks, and a minimal numerical test that passes documented tolerance gates.
- The EFT/KG branch is labeled [PLAUSIBLE] and remains quarantined until the discrete-action derivation and stability scans are complete.

Minimal math banner (for orientation only)
- RD canonical baseline:
  $$
  \partial_t \phi = D \nabla^2 \phi + r \phi - u \phi^2
  $$
  with front-speed reference $c_{\text{front}} = 2\sqrt{Dr}$ and linear dispersion $\sigma(k) = r - Dk^2$.
- EFT (quarantined future work):
  $$
  \square \phi + V'(\phi)=0, \quad \square=\partial_t^2 - c^2 \nabla^2,\quad c^2=2Ja^2
  $$
  kept separate from canonical RD claims pending full discrete-action derivation.

Licensing and use
- These materials are shared for academic review and discussion. Commercial use requires prior written permission. See the project’s LICENSE notice in the parent materials or distribution notes.

Rendering note
- Equations are written for MathJax/KaTeX. If your markdown viewer does not render display math, open the papers in a viewer that supports LaTeX math.

Contact and citations
- Cite the overview and the specific validation document you are referencing, e.g.:
  - “FUVDM Overview,”
  - “Reaction–Diffusion: Front-Speed Validation,”
  - “Reaction–Diffusion: Dispersion Validation.”
- For clarifications about scope, labels, or acceptance criteria, reference the file headers in [FUVDM_Overview.md](Prometheus_FUVDM/derivation/FUVDM_Overview.md:1) and the corresponding topic files listed above.

Scope boundaries and safety
- The derivations remain within theoretical physics and simulation. Cosmological or expansive claims are withheld or labeled until supported by derivation plus numeric checks. No ML training or proprietary AI algorithms are disclosed in this paper-only set.
