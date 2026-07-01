---
title: "SECS decomposes ionospheric sheet currents into curl-free (CF) and divergence-free (DF) elementary systems, each with a closed-form magnetic field kernel"
type: permanent
domain: space-physics
status: active
created: 2026-07-01
updated: 2026-07-01
tags:
  - space-physics/ionosphere
  - space-physics/source-localization
---

# SECS: curl-free / divergence-free elementary current decomposition

## Formulation

SECS (Spherical Elementary Current Systems) represents an ionospheric sheet current density as a superposition of elementary current systems placed on a grid over a spherical shell. Two elementary types: **curl-free (CF)** — radial current spreading uniformly outward/inward from a pole, closing via a field-aligned current (FAC) that connects to the magnetosphere; **divergence-free (DF)** — purely rotational/solenoidal current confined to the sheet, with no FAC connection. Any horizontal sheet current J_h(r) decomposes uniquely as J_h = J_CF + J_DF (a Helmholtz decomposition restricted to a spherical shell). Each elementary system i carries a scalar amplitude s_i; the ground field is B(r) = Σ_i s_i·G(r, r_i), where G is the elementary system's known closed-form kernel (different for CF vs DF). Stacking amplitudes as vector **s** and kernels as matrix **A** gives the linear forward model **B = A·s** used throughout SECS-GIBF (see [[gibf-beamforming-core]]).

## Constraints & Invariants

- CF and DF are defined by the divergence/curl properties of the *sheet current itself*, not by any property of the resulting ground field — the ground-field consequence (see [[fukushima-theorem]]) is a derived theorem, not part of the definition.
- The library `secsy` provides the field kernels (Ge, Gn, Gu components); its API for selecting CF vs DF (`current_type='curlfree'` etc.) has changed across versions — pin the version and verify with a probe before trusting any transfer matrix built from it. This bit the mag-GIBF project directly: a library that returns only the horizontal CF current without its companion radial FAC will not reproduce the Fukushima null, silently corrupting any transfer matrix built from it (see [[secs-gibf-viability]]).
- SECS is a source basis, not a physical model of currents — the sheet-current assumption (all current confined to a thin shell at ionospheric altitude) is itself an approximation, valid only in the quasi-static regime (ground arrays ~10²–10³ km, signal periods where aperture/c ≪ period).

## Connections

[[fukushima-theorem]] — the ground-null result for CF/radial-FAC systems, a direct consequence of the CF elementary system's field structure
[[gibf-beamforming-core]] — SECS supplies the source basis and the real transfer matrix A that GIBF and MMV-L1 both invert
[[secs-gibf-viability]] — active project running a CF/DF identifiability test (Experiment A) on this basis

## Open Questions

Whether CF is *identifiable* (not just observable) from ground data at high latitude — this is Experiment A / decision node D1 in the active roadmap, unresolved as of 2026-07-01.

## Sources

Suzuki 2011 (J. Sound Vib. 330); Vanhamäki & Juusola 2020 (ISSI SR-17, §2.7) — no literature note written yet. PDFs: `Desktop\School\IBF_Project\SECS.pdf`, `Desktop\School\IBF_Project\Ionospheric SECS.pdf` (see [[local-library]]).
