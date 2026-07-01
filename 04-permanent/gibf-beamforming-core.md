---
title: "GIBF inverts each cross-spectral-matrix eigenmode independently under a sparse prior; on a real (phase-less) transfer kernel this only helps when source pairs carry nonzero relative phase"
type: permanent
domain: space-physics
status: active
created: 2026-07-01
updated: 2026-07-01
tags:
  - space-physics/source-localization
  - space-physics/inverse-problems
---

# GIBF: per-mode eigen-decomposition beamforming, and when it beats joint sparse inversion

## Formulation

GIBF (Generalized Inverse Beamforming) images sparse sources from a sensor array via: (1) build the cross-spectral matrix (CSM) **S = (1/N)·X·Xᴴ** from N complex frequency-bin phasor snapshots X — not raw time samples (see invariant below); (2) eigendecompose S = Σ_i λ_i·u_i·u_iᴴ, keep the top K "signal" eigenmodes (K chosen via mode selection, e.g. Wax–Kailath AIC/MDL); (3) form each mode's **eigenmode vector v_i = √λ_i·u_i** (Suzuki Eq. 3 — carries the eigenvalue magnitude, not just the unit eigenvector); (4) invert each v_i **independently** against the real transfer matrix A (B = A·s) using a sparse per-mode prior (L1, solved by IRLS with iterative grid-reduction pruning, factor β=0.9 per iteration, switching the solve from underdetermined to overdetermined); (5) accumulate intensity across modes, I(j) = Σ_k |Ā[j,k]|², to form the final source image. The competitor, **MMV-L1** (multiple measurement vector), instead solves all K modes **jointly** under a shared-support (row-sparse, L2,1) prior — same inputs V and A, differing only in independent-per-mode vs shared-support.

## Constraints & Invariants

- **A must be real** everywhere except a deliberate phantom-phase ablation test — no `exp(ikr)` propagation phase, since a magnetostatic/quasi-static transfer kernel carries no propagation delay across the array aperture (domain of validity: aperture L and period T satisfy L/c ≪ T, i.e. ground arrays ~10²–10³ km at Pc3–5/Pi2/substorm timescales, 10⁻³–1 Hz). This is the fundamental disanalogy with acoustic GIBF, whose steering vectors carry `exp(ikr)` phase ramps that make the eigendecomposition informative by construction.
- **Load-bearing result (derived numerically, mag-GIBF project, 2026-06-30–07-01):** with a real A, the CSM is real-up-to-a-global-phase — and therefore its eigenvectors carry almost no exploitable complex structure — whenever the underlying sources are either incoherent, or coherent with zero relative phase (φ=0). Measured **residual eigenvector complexity κ** (global-phase-removed imaginary content of the top eigenmodes, κ = min_θ‖Im(e^{iθ}u)‖/‖u‖): incoherent ≈0.14 (N=64 snapshots, falling as 1/√N — e.g. ≈0.0013 at N=10⁵); φ=0 ≈0.01; φ=90° ≈0.62 (peak); returns to ≈0 at φ=180°. **Consequence: per-mode GIBF can only outperform joint MMV-L1 on a real kernel in the narrow regime of coherent sources with relative phase substantially away from 0°/180°, peaking near 90°.** Everywhere else (incoherent, or in-phase-coherent), the signal eigenmodes are mixtures projecting onto multiple steering vectors simultaneously, which favors MMV's shared-support prior — GIBF is expected to perform at best equal to, plausibly worse than, MMV in those regimes.
- **κ must be evaluated at the ground (κ_ground), not just at the source (κ_source)** — ionospheric spatial integration through A can wash out source-level phase structure before it reaches the array. The gap between κ_source and κ_ground is itself diagnostic of how much a real deployment can exploit this effect.
- A fair GIBF-vs-MMV comparison requires more than identical inputs (V, A): GIBF (per-mode L1-IRLS + grid reduction) and MMV-L1 (joint L2,1) cannot share a literal parameter set, so comparison is only fair under an explicit **matched-regularization / matched-effective-sparsity protocol**, with grid reduction applied symmetrically to both methods or neither — otherwise a loss is confoundable with "MMV was under-tuned."
- Because the discriminating variable (inter-source relative phase φ) is **latent** — it must be imaged, not directly observed — the algorithm cannot be gated on φ directly. The nearest observable proxy is the raw CSM imaginary content ‖Im S‖/‖S‖ (high exactly when φ is in the exploitable range), which any deployed gating rule must use instead of φ itself.

## Connections

[[secs-elementary-current-system]] — SECS supplies the source basis and real transfer matrix A that GIBF/MMV both invert
[[fukushima-theorem]] — the ground-null result that separately constrains which *part* (CF vs DF) of the source basis is even recoverable, independent of the eigenmode question here
[[secs-gibf-viability]] — active viability test operationalizing this note's φ-dependence as Experiment B (Card B, decision node D2) and forward-modeling realistic φ via Card C (field-line-resonance source coherence)

## Open Questions

Whether realistic ionospheric source pairs (e.g. field-line-resonance poles) actually present with φ in the exploitable 60–120° band on the ground, after washout through A — this is exactly what Card C (Tier 1 running now, Tier 2 pending `transfer.py`) is measuring, unresolved as of 2026-07-01.

## Sources

Suzuki 2011 (J. Sound Vib. 330) — GIBF derivation, carries √λ per Eq. 3; Wax & Kailath 1985 (IEEE TASSP) — AIC/MDL mode selection. No literature notes written yet. PDF: `Desktop\School\IBF_Project\Suzuki GIBF.pdf` (see [[local-library]]). Empirical φ/κ figures derived directly in the mag-GIBF project's roadmap desk-checks (`Python\mag-GIBF\ROADMAP (1).md`, Experiment Log entries 2026-06-30/07-01), not yet published anywhere external.
