---
title: "Fukushima theorem: radial field-aligned currents and their curl-free ionospheric closure produce no magnetic field at the ground beneath a uniform ionosphere"
type: permanent
domain: space-physics
status: active
created: 2026-07-01
updated: 2026-07-01
tags:
  - space-physics/ionosphere
  - space-physics/magnetometry
---

# Fukushima theorem: CF/radial-FAC ground null

## Formulation

For a spherically symmetric, laterally uniform ionosphere, a system of radial field-aligned currents (FACs) connecting to the magnetosphere, closed by curl-free (CF) horizontal sheet current in the ionosphere, produces **exactly zero magnetic field below the ionosphere** (at the ground) under a 1-D (radially layered) conductivity model. Equivalently: only the divergence-free (DF) part of the ionospheric sheet current, plus any genuinely 3-D conductivity structure, contributes a ground signature. This is the physical reason CF/FAC current systems are difficult or impossible to recover from ground-based magnetometer arrays alone.

## Constraints & Invariants

- The null result is **exact only under the 1-D/uniform-conductivity idealization**; real, laterally-varying ionospheric conductance leaks some CF signature to the ground — a "near-null," not a hard zero, in practice. This is the physical content behind the observability-ratio statistic ρ_obs used operationally in [[gibf-beamforming-core]] / [[secs-gibf-viability]].
- **Observability ≠ identifiability.** A CF signal can be technically nonzero (leaked via lateral conductivity) yet still not identifiable if it lies in the span of the DF response at the ground. Checking only "is there any CF signal" (ρ_obs) is necessary but not sufficient; a subspace-separation check (principal angles between the CF-driven and DF-driven ground-field subspaces) is required to actually decide identifiability. This distinction was a load-bearing gap found and fixed in the mag-GIBF roadmap on 2026-06-30.
- **Failure mode to guard against:** a SECS library (e.g. `secsy`) may implement only the horizontal CF current without its companion radial FAC. In that case the ground field will *not* vanish, and any transfer matrix computed from it will not reflect this theorem at all — verify the library returns the full Fukushima pair (horizontal CF current + radial FAC) before treating a computed near-null as a physical result, not a library artifact.

## Connections

[[secs-elementary-current-system]] — defines CF vs DF; this theorem is the ground-observability consequence of the CF definition
[[gibf-beamforming-core]] — the observability ratio ρ_obs operationalizes this theorem as a per-grid-point statistic
[[secs-gibf-viability]] — Experiment A (Card A) / decision node D1 tests this theorem's practical consequence for a real array geometry

## Open Questions

The latitude/conductivity regime at which the CF near-null breaks down enough to become marginally identifiable — being measured empirically in Experiment A, not yet run as of 2026-07-01.

## Sources

Fukushima 1976 (original theorem); Amm 1997 (restatement); Vanhamäki & Juusola 2020 (ISSI SR-17, §2.7) — no literature notes written yet. No local PDF specifically cataloged for Fukushima 1976 — check `Desktop\School\IBF_Project\` before citing further (see [[local-library]]).
