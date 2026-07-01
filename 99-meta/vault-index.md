---
title: Vault Index
type: meta
updated: 2026-07-01
---

# Vault Index

Master catalog of permanent notes and MOCs. Update when adding a new permanent note or MOC.

## Permanent Notes (`04-permanent/`)

| File | Title | Domain | Summary |
|---|---|---|---|
| `agentic-document-cascade.md` | Document cascade from manifesto to CLAUDE.md keeps stable invariants at root and volatile details at leaves | general | Four-layer doc hierarchy (Manifesto → SPEC → design → CLAUDE.md) for agent-driven coding projects |
| `secs-elementary-current-system.md` | SECS: curl-free/divergence-free decomposition of ionospheric currents | space-physics | Defines the CF/DF source basis and real transfer matrix A used throughout SECS-GIBF |
| `fukushima-theorem.md` | Fukushima theorem: CF/radial-FAC ground null, independent of conductance distribution | space-physics | Corrected 2026-07-01: breakdown mechanism is tilted field lines at lower latitude, not lateral conductivity |
| `gibf-beamforming-core.md` | GIBF: per-mode eigen-decomposition beamforming vs joint MMV-L1 on a real kernel | space-physics | GIBF only beats MMV-L1 when sources carry nonzero relative phase (φ≈90° peak); carries the residual-eigenvector-complexity (κ) result |
| `leak-safe-time-series-validation.md` | Leak-safe time-series validation checklist | machine-learning | Chronological splits, train-only scalers, embargo gap, test touched once, frozen controls, significance testing |
| `garman-klass-range-variance-proxy.md` | Garman-Klass is a range-variance proxy, not canonical RV | machine-learning | Biased low from omitted overnight return; breaks QLIKE unbiasedness; adjustment-invariance nuance |

## Maps of Content (`05-mocs/`)

| File | Domain | Summary |
|---|---|---|
| `space-physics-moc.md` | space-physics | Index for ionospheric currents, SECS/GIBF source localization, and related literature |
| `machine-learning-moc.md` | machine-learning | Index for ML architectures, time series, and source localization (Neural-GIBF, RV prediction) |
| `claude-workflow-moc.md` | claude-workflow | Index for Claude Code skills, CLAUDE.md hierarchy, and MCP/config decisions |

## Areas (`02-areas/`)

| Folder | Status | Goal |
|---|---|---|
| `claude-workflow/` | active | Ongoing practice domain for how Strider uses Claude Code — skills, CLAUDE.md hierarchy, MCP servers, hooks |
| `personal/` | active | Career trajectory, graduate program research, virtues/priorities |

## Projects (`01-projects/`)

| Folder | Status | Goal |
|---|---|---|
| `dynamica/` | in-progress | Interactive math modeling app proving cross-domain math unity |
| `gibf/` | planning | SECS-GIBF viability gate — two go/no-go experiments |
| `neural-gibf/` | planning | Cross-domain beamforming for MEG/EEG cortical source localization |
| `rv-prediction/` | in-progress | LSTM vs HAR for realized volatility forecasting (DL course project) |
| `em-globe/` | draft | Full-wave EM solver for ionosphere-Earth system (3-year proposal) |
| `math-blog/` | draft | 10-post blog series on categorical duality spanning pure math foundations to applied interdisciplinary science |
| `category-theory-diffgeo-essay/` | in-progress | Course essay applying category theory to differential geometry; precursor/feeder to math-blog |


## Resources (`03-resources/`)

| File | Type | Summary |
|---|---|---|
| `local-library.md` | reference | Local PDF collection: textbooks + IBF/SECS/GIBF papers, with paths — corrected 2026-07-01 after reading all 4 IBF_Project PDFs |
| `code-repositories-map.md` | reference | All Git repos under Code-Repositories with stack and purpose |
| `skill-vault-file.md` | reference | vault-file skill — inbox triage workflow, tested working |
| `skill-repo-state.md` | reference | repo-state skill — fetch-before-clean git workflow, tested working 2026-07-01 |
| `skills-kepano-obsidian.md` | reference | kepano/obsidian-skills pack — 5 installed skills |
| `claude-md-hierarchy.md` | reference | Four-tier CLAUDE.md hierarchy, current contents, rationale |
| `mcp-servers-in-use.md` | reference | Obsidian + GitHub MCP servers, config and status |
| `suzuki-2011-gibf.md` | literature | GIBF source paper — aeroacoustics (J. Sound Vib. 330, 2011), not space physics |
| `vanhamaki-juusola-2020-notes.md` | literature | SECS review, ISSI SR-17 Ch. 2 — source of the corrected Fukushima-theorem mechanism |
| `zavala-2010-generalized-inverse-beamforming.md` | literature | GIB investigation/validation study (acoustics); corrects a local-library mislabel |
| `li-2014-elastic-net-beamforming.md` | literature | Elastic net regularization for beamforming (acoustics), alternative to L1-IRLS |
