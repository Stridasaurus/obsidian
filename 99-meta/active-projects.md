---
title: "Active Projects"
type: meta
updated: 2026-06-30
---

# Active Projects

Priority order set 2026-06-30 (course deadlines drive #1–2; career/momentum drive #3–5).

### 1. Realized Volatility Prediction

- **Priority:** 1 — due in a week (~2026-07-07), course deliverable
- **Goal:** Can a small LSTM beat HAR at forecasting realized volatility, and does any edge survive honest OOS validation? DL course Project 2.
- **Status:** in-progress
- **Next action:** Complete Phase 1 — data pipeline + baseline (HAR, GARCH) in notebook 00
- **Notes:** `[[rv-prediction]]` — repo: `realized-volatility-prediction/`

---

### 2. Category Theory in Differential Geometry — Course Essay

- **Priority:** 2 — due in a week (~2026-07-07), course deliverable
- **Goal:** Class essay applying category-theoretic framing to differential geometry.
- **Status:** in-progress
- **Next action:** Define essay scope/thesis and outline
- **Notes:** `[[category-theory-diffgeo-essay]]` — precursor to `[[math-blog]]`; math-blog work won't start until this is done and is expected to roll directly into it

---

### 3. SECS-GIBF Viability Test (mag-GIBF)

- **Priority:** 3 — career move, no hard deadline
- **Goal:** Two go/no-go experiments (CF/DF identifiability + GIBF vs MMV-L1) outputting `DECISION_MEMO.md` with figures and a go/no-go recommendation. Doubles as methods paper backbone.
- **Status:** planning
- **Next action:** Build `geometry` and `transfer` modules + tests to get a trusted real transfer matrix A; then run Experiment A end-to-end
- **Notes:** `[[secs-gibf-viability]]` — repo: `GIBF/viability-test/`

---

### 4. Dynamica

- **Priority:** 4 — already started, unfinished work is visible/reputational
- **Goal:** Interactive mathematical modeling web app proving that finance, neuroscience, and physics share the same math. Three studios (QuantViz, NeuroLearn, PhySim), dual navigation derived from a single Registry, 12-model launch slice.
- **Status:** in-progress
- **Next action:** Write SPEC: compute-core (function signatures, purity rules, known-value test fixtures)
- **Notes:** `[[dynamica-manifesto]]` — SignalViz → PhySim rename pending in codebase

---

### 5. Neural-GIBF (MEG)

- **Priority:** 5 — not yet started
- **Goal:** Port GIBF beamforming from magnetospheric to cortical source localization (MEG/EEG). 5-week part-time build. Primary deliverable: quantitative benchmark vs MNE-Python reference methods + coherent-source extension.
- **Status:** planning
- **Next action:** Resolve four open decisions (repo name, methods note scope, Week 4 cut-line, Dynamica integration) before Week 1 starts
- **Notes:** `[[neural-gibf-proposal]]` — target: before September execution window

---

### Math Blog (not independently prioritized — gated on #2 above)

- **Goal:** 10-post blog series unifying category theory, tensors, duality, and measurement as a thread through signal processing, beamforming, stochastic processes, and learning. Post 7 (GIBF) is the signature applied piece.
- **Status:** draft
- **Next action:** Will start once the category-theory/diff-geo essay (#2) is complete; expected to reuse that material directly
- **Notes:** `[[math-blog]]` — brainstorm at `01-projects/math-blog/math-blog.md`

---

## Template (copy when adding a project)

### Project Name

- **Goal:** What the deliverable is
- **Status:** planning | in-progress | blocked | wrapping-up
- **Next action:** Specific next step
- **Notes:** `[[project-note-link]]`
