---
title: "Suzuki 2011 — L1 generalized inverse beamforming for coherent/incoherent, distributed and multipole sources"
type: literature
domain: space-physics
status: active
created: 2026-07-01
updated: 2026-07-01
tags:
  - space-physics/source-localization
source: "Takao Suzuki, 2011, 'L1 generalized inverse beam-forming algorithm resolving coherent/incoherent, distributed and multipole sources,' Journal of Sound and Vibration 330: 5835-5851"
source_url: "https://doi.org/10.1016/j.jsv.2011.05.021"
---

# Suzuki 2011 — GIBF source paper

## Key Quotes

- p.5835 (abstract): "To resolve coherent/incoherent, distributed/compact, and multipole aerodynamic-sound sources with phased-array pressure data, a new source-detection algorithm is developed based on L1 generalized inverse techniques. To extract each coherent signal, a cross spectral matrix is decomposed into eigenmodes. Subsequently, the complex source-amplitude distribution that recovers each eigenmode is solved using generalized inverse techniques..."
- p.5836, Eq. (2): the cross-spectral matrix decomposes as `(pp†) = UΛU†`, U unitary (orthonormal eigenvectors), Λ diagonal (eigenvalues).
- p.5836, Eq. (3): "the ith eigenmode is defined as `v_i = √λ_i · u_i`" — the exact eigenvalue-magnitude-carrying step [[gibf-beamforming-core]] flags as a common implementation bug if dropped (i.e. inverting the unit eigenvector `u_i` instead).
- p.5836, Eq. (4): `v_i = A·a_i` — the per-mode forward model; `A` is Suzuki's acoustic transfer/steering matrix (carries propagation phase across the array), `a_i` the unknown per-mode source-amplitude vector to recover by L1-IRLS.
- p.5835: the entire method is developed and demonstrated in an **aeroacoustics** context — phased-microphone-array localization of aerodynamic noise sources (jet/airframe noise), compared against DAMAS, DAMAS2, and CLEAN(-SC).

## My Summary

This is the actual GIBF source paper, and it is an aeroacoustics paper, not a space-physics one — a fact not previously captured anywhere in the vault. Suzuki's algorithm: build the array's cross-spectral matrix (CSM) from microphone pressure data, eigendecompose it, form each "eigenmode" as `v_i = √λ_i·u_i` (carrying the eigenvalue's square root, not just the unit eigenvector), then invert each eigenmode **independently** against a transfer matrix `A` using an L1-penalized IRLS solve with progressive grid reduction (underdetermined → overdetermined). Benchmarked against DAMAS/DAMAS2/CLEAN-SC, it resolves distributed and multipole sources better, at a few times DAMAS2's computational cost, and is validated against real wind-tunnel jet-flap interaction data.

The load-bearing detail for the mag-GIBF project: Suzuki's `A` is an **acoustic** kernel — it carries a complex propagation phase (`exp(ikr)`-style steering) across the array aperture, and that phase diversity is exactly what makes independent per-mode inversion informative in his domain. [[secs-gibf-viability]] replaces this with a **real-valued, phase-less** magnetostatic SECS kernel, which is the entire physical question the viability test (Card B, decision node D2) exists to resolve — see [[gibf-beamforming-core]] for the derived consequence.

## Connections

[[gibf-beamforming-core]] — the permanent note built directly from this paper's algorithm (Eqs. 1-4), extended and stress-tested on a real (non-acoustic) transfer kernel
[[secs-gibf-viability]] — active project applying/stress-testing this algorithm outside its native acoustic domain
