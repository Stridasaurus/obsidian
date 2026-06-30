---
title: "Active Projects"
type: meta
updated: 2026-06-29
---

# Active Projects

### Dynamica

- **Goal:** Interactive mathematical modeling web app proving that finance, neuroscience, and physics share the same math. Three studios (QuantViz, NeuroLearn, PhySim), dual navigation derived from a single Registry, 12-model launch slice.
- **Status:** in-progress
- **Next action:** Write SPEC: compute-core (function signatures, purity rules, known-value test fixtures)
- **Notes:** `[[dynamica-manifesto]]` — SignalViz → PhySim rename pending in codebase

---

### SECS-GIBF Viability Test

- **Goal:** Two go/no-go experiments (CF/DF identifiability + GIBF vs MMV-L1) outputting `DECISION_MEMO.md` with figures and a go/no-go recommendation. Doubles as methods paper backbone.
- **Status:** planning
- **Next action:** Build `geometry` and `transfer` modules + tests to get a trusted real transfer matrix A; then run Experiment A end-to-end
- **Notes:** `[[secs-gibf-viability]]` — repo: `GIBF/viability-test/`

---

### Neural-GIBF

- **Goal:** Port GIBF beamforming from magnetospheric to cortical source localization (MEG/EEG). 5-week part-time build. Primary deliverable: quantitative benchmark vs MNE-Python reference methods + coherent-source extension.
- **Status:** planning
- **Next action:** Resolve four open decisions (repo name, methods note scope, Week 4 cut-line, Dynamica integration) before Week 1 starts
- **Notes:** `[[neural-gibf-proposal]]` — target: before September execution window

---

### Realized Volatility Prediction

- **Goal:** Can a small LSTM beat HAR at forecasting realized volatility, and does any edge survive honest OOS validation? DL course Project 2.
- **Status:** in-progress
- **Next action:** Complete Phase 1 — data pipeline + baseline (HAR, GARCH) in notebook 00
- **Notes:** `[[rv-prediction]]` — repo: `realized-volatility-prediction/`

---

## Template (copy when adding a project)

### Project Name

- **Goal:** What the deliverable is
- **Status:** planning | in-progress | blocked | wrapping-up
- **Next action:** Specific next step
- **Notes:** `[[project-note-link]]`
