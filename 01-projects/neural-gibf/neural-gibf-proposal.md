---
title: Neural-GIBF — Cross-Domain Inverse Beamforming for MEG/EEG Cortical
  Source Localization
type: capture
domain: computational-neuroscience
status: draft
created: 2026-06-30
updated: 2026-06-30
tags:
  - computational-neuroscience/source-localization
  - space-physics/inverse-problems
---

# Neural-GIBF — Cross-Domain Inverse Beamforming for MEG/EEG

**Repo name (proposed):** `neural-gibf`  
**Timeline:** 5-week part-time build (target: before September execution window)  
**Purpose:** Portfolio/PhD application artifact; demonstrate cross-domain transfer of inverse beamforming from magnetospheric to cortical source localization

## The One-Sentence Version

Take the GIBF machinery built for magnetometer arrays, point it at a brain instead of a magnetosphere, and prove — against MEG's reference methods on ground-truth data — that it reconstructs cortical sources competitively.

## Why the Math is the Same

| Dimension | MHD work | MEG/EEG |
|-----------|----------|---------|
| Measurement | Ground magnetometer array b (nT) | SQUID/OPM array b (fT–pT) |
| Unknown | MHD wave current sources | Cortical primary-current dipoles |
| Forward op | SECS kernel → real A | Quasi-static Maxwell + head conductivity → leadfield L |
| Model | b = Lx + n | b = Lx + n |
| Method | Generalized inverse beamforming | LCMV / DICS beamforming (already standard in MEG) |
| Coherence | Coherogram across magnetometers | DICS = coherent-source imaging |

Key: LCMV/DICS is *already* the establishment method in MEG. This is not an exotic import — it's arriving in a field that already speaks the same mathematical language.

## Differentiated Contribution: Coherent Sources

Standard beamformers (LCMV/DICS) assume uncorrelated source time courses. When sources are coherent, the spatial filter partially cancels them. This is documented but underexplored.

The coherent-source regime is exactly the object of study from the magnetometer coherogram work (detecting coherent global periodic anomalies across spatially separated sensors). This makes the coherent-source extension the project's intellectual core, not a generic exercise.

## Methods Under Comparison

- **LCMV/GIBF (from scratch)** — `W = (LᵀC⁻¹L)⁻¹LᵀC⁻¹`; validated against MNE-Python reference
- **DICS** (frequency-domain beamformer) — bridge to coherogram work
- **dSPM** — noise-normalized minimum-norm
- **sLORETA** — zero localization bias for single source; principled reference for bias analysis
- **(Stretch) RAP-MUSIC**

## Three Data Tiers

1. **Simulation** — full ground-truth control; SNR and separation sweeps; ports from `magnetometer-time-series-simulator`
2. **Phantom data** — physical dipoles at known positions inside real scanner; gold standard for honest DLE numbers
3. **Real evoked data** — MNE `sample` (auditory/visual), somatosensory; approximate known generators

## Key Analysis: Resolution Matrix

For each linear inverse, form `R = (inverse operator)·L`. Columns = point-spread functions; rows = cross-talk functions. Standard rigorous method (Hauk/Stenroos/Molins) to characterize inverses as operators, not black boxes. Most PhD-legible piece of the analysis.

## Five-Week Plan

| Week | Deliverable | Done When |
|------|-------------|-----------|
| 1 | Forward model + "Rosetta Stone" notation mapping | Clean notebook reproducing known source estimate |
| 2 | LCMV/GIBF from scratch, validated vs MNE | Matches MNE's LCMV to numerical tolerance |
| 3 | Ground-truth benchmark (core deliverable) | Quantitative table + figures on ground-truth data |
| 4 | Coherent-source extension (differentiator) | Coherence vs. localization result with figures |
| 5 | Feature freeze, methods note (4–6 pp), clean repo | Stranger can clone + understand in 90 seconds |

**Cut line:** if Week 4 fights back, ship the Section-5 benchmark and stop. Week 4 is explicitly cuttable.

## Risk Register

| Risk | Mitigation |
|------|-----------|
| FreeSurfer/BEM rabbit hole | Use `fsaverage` precomputed forward; sphere models for sim/phantom. Banned from building head models. |
| Coordinate frame/unit footguns | Lean on MNE's coordinate handling; Week 2 anchor catches most |
| Scope creep | Weeks 1–3 = minimum shippable; feature freeze week 5 |
| Overclaiming | Framing: validated reimplementation + comparison + focused result; never "beat the library" |

## Open Decisions (need answers before Week 1)

1. Repo name: `neural-gibf` vs cleaner alternative
2. Methods note: pure portfolio note vs arXiv-structured (~10% more effort)
3. Pre-commit cut-line for Week 4
4. `dynamica` integration: stretch or real Week-5 deliverable?

## PhD Application Positioning

Targets: Caltech CNS, Princeton PNI, Gatsby (physics-to-neuro track). Framing: "the operator is domain-agnostic; I demonstrated it by carrying my own method across from magnetospheric to cortical sources and validating it against the field's standards." Signals: method depth, cross-domain transfer, ability to self-direct a small research project to a written result.

## Connections

- Directly downstream of [[20260630-secs-gibf-viability]] (same GIBF machinery)
- EM-Globe ([[20260630-em-globe-proposal]]) is the long-run upstream project that would supply the complex transfer matrix both domains need
