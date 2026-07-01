---
title: "Vanhamäki & Juusola 2020 — Introduction to Spherical Elementary Current Systems"
type: literature
domain: space-physics
status: active
created: 2026-07-01
updated: 2026-07-01
tags:
  - space-physics/ionosphere
source: "Heikki Vanhamäki and Liisa Juusola, 2020, 'Introduction to Spherical Elementary Current Systems,' Chapter 2 in M.W. Dunlop and H. Lühr (eds.), Ionospheric Multi-Spacecraft Analysis Tools, ISSI Scientific Report Series 17, pp. 5-33 (open access)"
source_url: "https://doi.org/10.1007/978-3-030-26732-2_2"
---

# Vanhamäki & Juusola 2020 — SECS review (ISSI SR-17, Ch. 2)

## Key Quotes

- p.7 (§2.1): "the ionospheric current system basically consist of horizontal currents flowing around 100–150 km altitude, and almost vertical field-aligned currents (FAC) flowing along the geomagnetic field, thus connecting the ionospheric currents to the magnetosphere."
- p.9 (§2.3): "Elementary current systems... are based on Helmholtz's theorem, which states that any well-behaved... vector field is uniquely composed of a sum of curl-free (CF) and divergence-free (DF) parts... the CF system has a Dirac δ-function divergence and the DF system a δ-function curl at its pole, with uniform and oppositely directed sources elsewhere."
- p.9, Eqs. (2.7)-(2.8): the closed-form elementary field kernels, `V_CF(r') = (S_CF/4πR)·cot(θ'/2)·ê_θ'` and `V_DF(r') = (S_DF/4πR)·cot(θ'/2)·ê_φ'` — the exact kernel forms underlying [[secs-elementary-current-system]].
- **p.14-15 (§2.7, the load-bearing passage):** "At high magnetic latitudes the curl-free part of the ionospheric horizontal current, together with associated FAC, does not produce any magnetic field below the ionosphere. Fukushima (1976) showed this by assuming uniform ionospheric conductances, but the result is valid independent of the conductance distribution (Amm 1997). The crucial assumption needed in deriving this result is that the FAC should flow radially. For strictly radial FAC, the ground magnetic disturbance from ionospheric current is produced solely by the divergence-free part... This is only approximately true even at the auroral zone, and breaks down completely at lower latitudes, where the magnetic field has larger inclination."
- p.15: "When the magnetic field lines are tilted, the FACs and associated horizontal curl-free currents make some contribution to the ground magnetic disturbance. As... Tamao (1986) showed, this contribution can be reasonably large even at ∼60° magnetic latitude."
- p.15, Eq. (2.30): the ground-field transfer relation `B_G,⊥ = T · S_DF` — the direct ancestor of the `B = A·s` forward model in [[secs-elementary-current-system]] / [[gibf-beamforming-core]], here restricted to DF SECS only (since CF contributes ~nothing at high latitude).
- p.31 (References): full citation recovered — "Fukushima, N. 1976. Generalized theorem for no ground magnetic effect of vertical currents connected with Pedersen currents in the uniform-conductivity ionosphere. Report of Ionosphere and Space Research in Japan 30: 35–40."

## My Summary

This is the actual SECS source/review — Chapter 2 of the open-access ISSI SR-17 book (*Ionospheric Multi-Spacecraft Analysis Tools*, ed. Dunlop & Lühr, Springer 2020). Both `SECS.pdf` and `Ionospheric SECS.pdf` in the local library turned out to be byte-identical copies of this same 296-page book, not two different papers — `local-library.md` has been corrected. Chapter 2 derives the CF/DF elementary-system basis from Helmholtz's theorem, gives the closed-form field kernels, and — most importantly for [[secs-gibf-viability]] — pins down the exact mechanism and validity conditions of the Fukushima ground-null result.

**This directly corrected an error in the vault's [[fukushima-theorem]] note**: the null result's exactness hinges on the FAC flowing strictly radially, not on uniform ionospheric conductance. Fukushima's 1976 proof assumed uniform conductance, but Amm (1997) showed the result holds for *any* conductance distribution provided FAC is radial. The actual breakdown mechanism at lower latitude is tilted field lines (FAC stops being radial), not lateral conductivity structure as the note previously stated — fixed 2026-07-01.

## Connections

[[secs-elementary-current-system]] — drawn directly from this chapter's §2.2-2.3
[[fukushima-theorem]] — corrected using this chapter's §2.7
[[secs-gibf-viability]] — Experiment A's latitude sweep (high/mid/low) directly tests where the radial-FAC assumption (and hence the ground-null result) breaks down
