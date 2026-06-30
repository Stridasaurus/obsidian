---
title: "Recent Context Cache"
type: meta
updated: 2026-06-29
---

# Recent Context Cache

**Last updated:** 2026-06-30

## What was done

First real organization pass of the vault. All 7 inbox captures from 2026-06-30 were triaged and filed:

- `04-permanent/agentic-document-cascade.md` — Evergreen methodology note on the four-layer document cascade (Manifesto → SPEC → design → CLAUDE.md) for agent-driven coding projects. Frontmatter updated: type `permanent`, status `evergreen`.
- `03-resources/code-repositories-map.md` — Full map of all repos under `Code-Repositories/`: Python repos (magsim, magnetic-source-identification, mhd-ibf-reconstruction, GIBF, lab-notebooks, Summer-2026-DL), Sites repos (settgast-ui, dynamica, correlationlab, LIF-project, StriderSettgast.com, application-tracker, resume-tracker, magnetometer-coherogram, pca-engine). Cross-cutting notes on shared sensor file (L058.txt), magsim as shared dep, research pipeline direction, job search context.
- `01-projects/dynamica/dynamica-manifesto.md` — Full Dynamica manifesto: three studios (QuantViz/NeuroLearn/PhySim replacing SignalViz), M1–M8 math taxonomy, module DAG (Compute Core → Model Shell → Models → Registry → Navigation), 7 success criteria, 7 non-negotiable invariants, 12-model launch slice, 5 downstream SPECs implied.
- `01-projects/gibf/secs-gibf-viability.md` — SECS-GIBF viability test build brief: two experiments (CF/DF identifiability via observability ratio; GIBF vs MMV-L1 with decision rule Δr̄ ≥ 20%), three solvers (L2 min-norm, GIBF per-mode L1 IRLS, MMV-L1 joint), build order, secsy API warning.
- `01-projects/neural-gibf/neural-gibf-proposal.md` — Neural-GIBF proposal: port GIBF machinery from magnetospheric to cortical source localization. Five-week plan, three data tiers (simulation/phantom/real evoked), resolution matrix analysis, four open decisions blocking Week 1.
- `01-projects/rv-prediction/rv-prediction.md` — RV Prediction DL project: LSTM vs HAR, 5 notebooks, Garman–Klass estimator, QLIKE loss, walk-forward OOS, pre-committed three-way analysis (by regime / horizon / architecture-vs-features).
- `01-projects/em-globe/em-globe-proposal.md` — EM-Globe long-range proposal: full-wave Maxwell FEM solver for ionosphere-Earth system, 9 modules, 6 known research gaps requiring human intervention (especially reciprocity in gyrotropic media). Upstream of SECS-GIBF.

Structural fix: `02-areas/` had been accidentally moved by Obsidian into `01-projects/02-areas/`. Restored to vault root with `.gitkeep`.

`99-meta/active-projects.md` and `99-meta/vault-index.md` both updated to reflect current state.

## Active project landscape (as of 2026-06-30)

- **Dynamica** (in-progress) — next: write SPEC: compute-core
- **SECS-GIBF** (planning) — next: build `geometry` + `transfer` modules, land Experiment A
- **Neural-GIBF** (planning) — next: resolve 4 open decisions before Week 1
- **RV Prediction** (in-progress) — next: Phase 1, notebook 00 (data + HAR/GARCH baselines)
- **EM-Globe** (proposal/draft) — no active work; upstream of SECS-GIBF

## Connections to map

The three research projects form a loose dependency chain: SECS-GIBF (immediate viability gate) → Neural-GIBF (cross-domain port, shares GIBF machinery) → EM-Globe (long-run upstream providing complex transfer matrix). Dynamica and RV Prediction are independent.

## Unresolved

- No permanent notes yet on core domain concepts (space physics / SECS / MHD wave physics). Worth creating those as research sessions happen.
- No MOCs created yet. First MOC candidates: `space-physics-moc.md`, `machine-learning-moc.md`.
- Neural-GIBF Week 1 is blocked on 4 open decisions — resolve before scheduling build time.
