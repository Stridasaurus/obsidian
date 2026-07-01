---
title: "Fukushima theorem: radial field-aligned currents and their curl-free ionospheric closure produce no magnetic field at the ground, independent of conductance distribution"
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

At high magnetic latitude, the curl-free (CF) part of the ionospheric horizontal current, together with its associated field-aligned current (FAC), produces **no magnetic field below the ionosphere**. Fukushima (1976) proved this assuming uniform ionospheric conductance; Amm (1997) generalized it to show the result holds **independent of the conductance distribution**. The one crucial, load-bearing assumption is that the **FAC flows radially**. For strictly radial FAC, the ground magnetic disturbance from the ionospheric current system is produced solely by the divergence-free (DF) part.

## Constraints & Invariants

- **The breakdown mechanism is tilted field lines, not lateral conductivity variation.** The radial-FAC assumption is only approximately true even in the auroral zone and breaks down completely at lower/mid latitude, where the geomagnetic field has larger inclination — this is the actual mechanism by which CF leaks a ground signature, not spatial conductance structure. (Corrected 2026-07-01 after reading the source directly — an earlier draft of this note incorrectly attributed the breakdown to lateral conductivity variation.)
- When field lines are tilted, the FACs and their CF closure make some ground contribution — Tamao (1986) showed this can be "reasonably large" even at ~60° magnetic latitude, though the resulting field is typically spatially smoother than the DF contribution, so opposite-sign FAC contributions partially cancel.
- **Observability ≠ identifiability.** A CF signal can be technically nonzero (via tilted-FAC leakage) yet still not identifiable if it lies in the span of the DF ground response. Checking only "is there any CF signal" (ρ_obs) is necessary but not sufficient; a subspace-separation check (principal angles between the CF-driven and DF-driven ground-field subspaces) is required to actually decide identifiability. This distinction was a load-bearing gap found and fixed in the mag-GIBF roadmap on 2026-06-30.
- **Failure mode to guard against:** a SECS library (e.g. `secsy`) may implement only the horizontal CF current without its companion radial FAC. In that case the ground field will *not* vanish, and any transfer matrix computed from it will not reflect this theorem at all — verify the library returns the full Fukushima pair (horizontal CF current + radial FAC) before treating a computed near-null as a physical result rather than a library artifact.

## Connections

[[secs-elementary-current-system]] — defines CF vs DF; this theorem is the ground-observability consequence of the CF definition
[[gibf-beamforming-core]] — the observability ratio ρ_obs operationalizes this theorem as a per-grid-point statistic
[[secs-gibf-viability]] — Experiment A (Card A) / decision node D1 sweeps latitude (high/mid/low), directly probing where the radial-FAC assumption (and hence this theorem) breaks down
[[vanhamaki-juusola-2020-notes]] — source of this corrected understanding (§2.7)

## Open Questions

The latitude/inclination regime at which the CF near-null breaks down enough to become marginally identifiable — being measured empirically in Experiment A, not yet run as of 2026-07-01. Tamao (1986) puts "reasonably large" tilted-FAC contribution at ~60° magnetic latitude as a rough external reference point.

## Sources

Fukushima, N. 1976. *Generalized theorem for no ground magnetic effect of vertical currents connected with Pedersen currents in the uniform-conductivity ionosphere.* Report of Ionosphere and Space Research in Japan 30: 35–40 — cited secondhand via [[vanhamaki-juusola-2020-notes]] (§2.7); the 1976 original itself has not been read (no local PDF found). Amm, O. 1997 (generalization to arbitrary conductance) — also cited secondhand, not read directly. Tamao, T. 1986. *Direct contribution of oblique field-aligned currents to ground magnetic fields.* JGR 91(A1): 183–189 — cited secondhand.
