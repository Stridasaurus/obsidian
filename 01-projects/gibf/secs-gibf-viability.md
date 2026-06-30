---
title: SECS-GIBF Viability Test — Two Go/No-Go Experiments
type: project
domain: space-physics
status: active
created: 2026-06-30
updated: 2026-06-30
tags:
  - space-physics/magnetometry
  - space-physics/inverse-problems
---

# SECS-GIBF Viability Test — Two Go/No-Go Experiments

**Repo:** https://github.com/Stridasaurus/GIBF  
**Location in repo:** `viability-test/`  
**Status:** Full build brief written; not yet implemented  
**Output:** `DECISION_MEMO.md` with two figures and a go/no-go recommendation (doubles as experimental backbone of a methods paper)

## Two Non-Negotiable Invariants

1. **Transfer matrix `A` is real-valued.** No `exp(ikr)` anywhere except Experiment B4. Assert `np.isrealobj(A)` in solvers.
2. **Snapshots are complex frequency-bin phasors, not raw time samples.** Real X → real CSM → real eigenvectors → method collapses. A test guards this.

## The Two Questions

### Question 1 — CF/DF Identifiability (Experiment A)

For radial FAC at high latitude, the Fukushima theorem says CF current produces *no ground magnetic field*. If true for our geometry, the CF columns of A are near-null and CF/DF separation is unrecoverable from ground data.

**Statistic:** median observability ratio `ρ_obs(j) = ‖A·e_CF(j)‖ / ‖A·e_DF(j)‖`

**Decision rule:**
- `< 1e-2` at high lat → CF unrecoverable; pipeline must be DF-only
- `1e-2 to 1e-1` → marginal; low-confidence diagnostic only
- `≥ 1e-1` → CF observable; keep it

### Question 2 — Does GIBF Eigen Layer Earn Its Keep? (Experiment B)

Acoustic GIBF works because steering vectors carry `exp(ikr)` phase ramps across the array. Our magnetostatic kernel has **no propagation phase**. Does mode-by-mode inversion still beat joint sparse inversion (MMV-L1) on identical inputs?

**Fair comparison:** GIBF and MMV-L1 receive identical `V = [√λ₁u₁, ..., √λₖuₖ]` and identical real `A`. Only difference: independent-per-mode (GIBF) vs shared-support joint (MMV).

**Decision rule:** GIBF "worth it" only if Δr̄ ≥ 20% lower OR resolves at ≥1 grid cell smaller separation, with non-overlapping 95% CIs at two+ SNR levels.

## Three Solvers

- **L2 min-norm** — Tikhonov, context baseline
- **GIBF (Suzuki, per-mode L1 IRLS)** — grid reduction (β=0.9), carry `√λᵢ` (NOT unit eigenvector — prior report dropped this, it's a bug)
- **MMV-L1 (joint row-sparse IRLS)** — shared support across modes; accumulation `I(j) = Σₖ|Ā[j,k]|²` same as GIBF

## Experiments

- **A** — deterministic SVD/observability at high/mid/low latitude; no Monte Carlo
- **B1** — incoherent separation sweep (headline), grid-reduction on/off
- **B2** — coherent stress test (ρ = 0.95)
- **B3** — mode-selection validity (Wax-Kailath AIC/MDL vs true K)
- **B4** — phantom-phase ablation (GIBF with fake acoustic phase vs real A); gold explanatory figure
- **B5** — CF/DF attribution (only if Exp A says CF observable)

## Build Order

1. `geometry`, `transfer` (+ tests) → get real A you trust
2. **Experiment A end-to-end** (land CF/DF decision FIRST; may simplify all downstream)
3. `simulate`, `csm`, `modeselect` (+ tests)
4. Three solvers (+ tests)
5. `metrics`, `plotting`
6. Experiment B1 → B3 → B2 → B4 → (B5 if applicable)

## secsy API Warning

The existing project report uses `get_SECS_B_G_matrices(..., current_type='curlfree')` but this keyword changes across secsy versions. Must run verification probe before writing `transfer.py`. Pin the version.

## References

- Suzuki 2011 (J. Sound Vib. 330) — GIBF algorithm; carry √λ per Eq. 3
- Vanhamäki & Juusola 2020 (ISSI SR-17) — SECS; §2.7 = Fukushima/DF result
- Wax & Kailath 1985 (IEEE TASSP) — AIC/MDL mode selection
- Fukushima 1976 — no-ground-effect theorem
