---
title: "Li, Tong & Jiang 2014 — Sound Source Localization via Elastic Net Regularization"
type: literature
domain: space-physics
status: active
created: 2026-07-01
updated: 2026-07-01
tags:
  - space-physics/source-localization
source: "Xiaodong Li, Weiming Tong, Min Jiang, 2014, 'Sound Source Localization via Elastic Net Regularization,' BeBeC-2014-02 (5th Berlin Beamforming Conference)"
source_url: ""
---

# Li, Tong & Jiang 2014 — elastic net for beamforming (BeBeC-2014-02)

## Key Quotes

- p.1 (abstract): "Since only a small portion of the source scanning region is expected to possess strong sources, the solutions of these equations would be sparse. In this paper, the elastic net regularization technique is proposed to solve the linear equations for sound source localization... could improve both the resolution and accuracy compared with DAS... and DAMAS..., particularly for cases under low signal-to-noise ratios."
- p.2 (§2), Eqs. (2)-(3): L2 (Tikhonov) regularization `min_x {‖Ax−b‖²₂ + λ‖x‖²₂}` vs. L1 regularization `min_x {‖Ax−b‖²₂ + λ‖x‖₁}` — elastic net combines both terms.

## My Summary

A sparse-regularization comparison paper from the acoustic beamforming literature, not directly about GIBF's eigen-decomposition step. It addresses the same underlying linear inverse problem (`Ax=b`, sparse `x` expected) that GIBF's per-mode L1-IRLS solve also addresses, but via elastic net (combined L1+L2) rather than pure L1, and validates against DAS/DAMAS on NACA0012 airfoil self-noise simulation data. `local-library.md`'s prior guess ("likely a regularization baseline for GIBF") holds up on reading — it is a plausible alternative regularizer, not currently adopted by [[secs-gibf-viability]].

## Connections

[[gibf-beamforming-core]] — alternative sparse-inversion regularization scheme, not currently adopted by the active project
