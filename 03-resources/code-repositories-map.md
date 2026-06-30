---
title: Code Repositories Map — Strider Settgast
type: reference
domain: general
status: active
created: 2026-06-30
updated: 2026-06-30
tags:
  - meta/repos
  - meta/codebase-map
---
# Code Repositories Map — Strider Settgast

All repos live under `C:\Users\strid\OneDrive\Code-Repositories\`. Three subdirectories: `Python/`, `Sites/`, and `obsidian/` (this vault).

Root `CLAUDE.md`: follow each ecosystem's standard best practices; inspect lockfiles/package managers before acting.

---

## Python Repos (`Python/`)

### `magnetometer-time-series-simulator`
**Purpose:** Installable Python package (`magsim`, v1.0.0) that generates synthetic magnetometer data from magnetic dipole sources. Built specifically to produce training data for neural networks doing magnetic source localization.

**Key classes:** `TimeSeriesSimulator`, `SimulatorConfig`, `SourceType` enum, `NoiseModel` enum (Gaussian/Uniform/Mixed).

**Core methods:** `generate_sample()`, `generate_batch()`, `generate_time_series()`, `dipole_field()`. Supports static batches and moving-source time series.

**Stack:** Python 3.12, NumPy. Installable via `pyproject.toml`. Tests in `tests/`. Shared as a dependency by other repos (copied into GIBF as a submodule).

**CLAUDE.md:** Has one; check before working.

---

### `magnetic-source-identification`
**Purpose:** MTH 5320 Project 1 — identifying 3D position and pole type (monopole vs dipole) of simulated ionospheric sources from a 29-station global magnetometer array (L058.txt). Multi-task feedforward neural network with Optuna hyperparameter search.

**Key finding:** Monopole sources localize well (~720 km error, improves with data). Dipole sources hit an irreducible floor (~8,300 km — geocentric radius scale) due to moment ambiguity that cannot be resolved by architecture or data size changes.

**Structure:** 5 experiment notebooks (self-contained, run independently) + `05_Analysis.ipynb` cross-experiment evaluation. Saved model checkpoints in `winners/`. Full report in `Settgast_Project1_Report.md`.

**Stack:** Python 3.12, PyTorch, Optuna, NumPy. Targets Google Colab GPU; also runs locally.

**CLAUDE.md:** Has one.

---

### `mhd-ibf-reconstruction`
**Purpose:** Computational framework to reconstruct 3D MHD wave fields in the magnetosphere using ground-based magnetometer arrays. Implements Generalized Inverse Beamforming (GIBF). Flask web app (`app.py`).

**Two phases:** Phase 1 — synthetic test (generate wave, simulate sensors, FFT, IBF reconstruct, compare). Phase 2 — apply to real magnetometer data.

**Key invariant for GIBF work:** The transfer matrix `A` is **real-valued** (no propagation phase). This is the core physics constraint separating SECS-GIBF from acoustic beamforming.

**Stack:** Python, Flask, NumPy/SciPy. Has `CPCA.Base` dependency.

**CLAUDE.md:** Has one.

---

### `GIBF`
**Purpose:** SECS-GIBF viability gate — a self-contained research codebase to answer two go/no-go questions about the SECS-GIBF method before building the full pipeline. Also serves as the backbone of a methods paper.

**Two invariants (never violate):**
1. Transfer matrix `A` is real-valued — no `exp(i k r)` propagation phase outside ablation experiment B4.
2. Snapshots are complex frequency-bin phasors, not raw time samples (must produce complex Hermitian CSM, not real covariance).

**Structure:** Contains `magnetometer-time-series-simulator` and `mhd-ibf-reconstruction` as submodules/subdirectories. Also has `secsy/` (SECS kernel library requiring network access to install) and `mhd_notebook (1).ipynb`.

**Output target:** `DECISION_MEMO.md` with two figures and a go/no-go recommendation.

**CLAUDE.md:** Build brief is `GIBF_viability_BUILD_BRIEF.md`. Very detailed spec — read in full before any work.

---

### `lab-notebooks`
**Purpose:** Sandbox / experimental notebooks. Main research notebooks for magnetometer data analysis and MHD wave work.

**Key notebooks:**
- `magnetometer/mag-data-analysis.ipynb` — real IAGA-format magnetometer data analysis
- `magnetometer/mhd-notebook.ipynb` — MHD wave analysis
- `magnetometer/Mag Data/` — IAGA `.txt` files, one per station (e.g., ADL.txt, TIX.txt)
- `scratch/` — misc experiments (Biot-Savart, probability, finance)

**Stack:** conda env `sandbox-env`. Launch: `conda activate base && jupyter notebook`, select `sandbox-env` kernel. Pre-commit hook auto-regenerates `environment.yml`.

**CLAUDE.md:** Has one — read before working, especially for env setup.

---

### `Summer-2026-Deep-Learning`
**Purpose:** Course materials from a summer 2026 deep learning course. Weeks 1–5 covering regression, gradient descent, classification, neural nets, backpropagation, SGD, hyperparameters, CNNs, transfer learning. Has `Homework/`, `Workshops/`, `Project-1/`, and weekly folders.

**Stack:** Python, likely PyTorch/Keras. No README.

---

## Sites Repos (`Sites/`)

### `settgast-ui`
**Purpose:** `@settgast/ui` — a published npm component library (v0.2.0) used across Strider's web projects. Turborepo monorepo.

**Critical build detail:** `tsup.config.ts` has a custom `onSuccess` hook that scopes CSS Modules class names and prepends design token CSS. Do not remove or simplify this hook — components depend on it.

**Stack:** TypeScript, React 19, CSS Modules, tsup, Storybook. Published to npm with public access.

**Publishing workflow:** `pnpm changeset` → `pnpm changeset version` → `pnpm release` (from `packages/ui/`).

**CLAUDE.md:** Has one — read it before touching the build system.

---

### `dynamica`
**Purpose:** Interactive mathematical modeling web app organized around three "studios":
- **QuantViz** (Finance) — markets as stochastic dynamical systems, portfolio correlation/returns
- **NeuroLearn** (Neuroscience) — neural dynamics from first principles (LIF neurons, spike stats)
- **SignalViz** (Signal Processing) — shared mathematical toolkit (Fourier, correlation, convolution, etc.)

**Tools modeled:** correlation, Fourier, convolution, stochastic calculus, dynamical systems, linear algebra, detection, information theory.

**Stack:** React 19, TypeScript, Vite, Recharts, Zustand, Tailwind, React Router. Turborepo monorepo. Depends on `@settgast/ui`. Package manager: `pnpm`.

**Structure:** `apps/dynamica/` — main app. `apps/correlationlab/` and `apps/lif-project/` likely share the monorepo.

---

### `correlationlab`
**Purpose:** Browser-only financial portfolio correlation analysis tool. Build a portfolio, explore rolling Pearson correlation matrices, cumulative returns, Sharpe ratios across time windows 3M–20Y.

**Live:** https://stridasaurus.github.io/correlationlab/

**Data:** Pre-built static JSON for ≤2Y ranges (refreshed daily by GitHub Actions via yfinance). Live-fetch from Stooq/Yahoo Finance for custom tickers and 5Y+ ranges. Three CORS proxies in fallback chain; synthetic series if all fail.

**Stack:** React 19, TypeScript 6, Vite 8, Recharts 3, Tailwind 3, Vitest 4. No backend.

**CLAUDE.md:** Has one.

---

### `LIF-project`
**Purpose:** Leaky Integrate-and-Fire neuron simulator. Originally a CSE1505 (Intro to Python, Fall 2025) final project. Evolved into a web app.

**Live:** https://stridasaurus.github.io/LIF-project/

**Structure:** `lif_core/` — reusable Python simulation engine. `web-app/frontend/` — browser app running simulation client-side (Plotly). `web-app/backend/` — optional FastAPI REST API. Original notebook preserved in `web-app/notebook/`.

**Physics:** RC circuit model. τ_m × (dV/dt) = −(V − V_rest) + R(t) × I(t). Parameters I(t), V_thr(t), R(t) are configurable as arbitrary time functions.

**CLAUDE.md:** Has one with conda setup instructions.

---

### `StriderSettgast.com`
**Purpose:** Personal portfolio/blog site.

**Live:** Deployed to GitHub Pages via GitHub Actions on push to `main`.

**Stack:** Astro. Blog posts: drop `.md` file in `src/content/blog/` with filename `YYYY-MM-DD-short-slug.md`. Math support via KaTeX (`$...$` inline, `$$...$$` display). Code highlighting via Shiki.

**CLAUDE.md:** Has one.

---

### `application-tracker`
**Purpose:** Static client-side Kanban for a multi-track job + PhD search. Tracks: Quant Finance, Neurotech/BCI, Defense/Aerospace, Fusion, PhD Programs, Other. Data persists in `localStorage`. Daily GitHub Actions job discovery via Greenhouse/Lever/Ashby APIs, USAJOBS, and Adzuna.

**Features:** Track-aware pipelines (jobs vs PhD differ), deadline-first prioritization, analytics dashboard, one-click PDF, JSON backup/import, dark/light theme.

**Stack:** React 18, Vite, Tailwind, Recharts, jsPDF, Vitest. Logic in `src/domain/` is unit-tested.

**Note:** A similar repo `resume-tracker` exists — appears to be a parallel build or earlier iteration with the same README description. Check both if working on this feature area.

**CLAUDE.md:** Has one.

---

### `resume-tracker`
**Purpose:** Appears nearly identical to `application-tracker` — same README, same stack, same feature set. Likely an earlier version or experimental branch. Deployed to a different Pages URL (`stridasaurus.github.io/resume-tracker/`).

**CLAUDE.md:** Has one.

---

### `magnetometer-coherogram`
**Purpose:** Single-page vanilla JS browser tool for visualizing coherence across the global magnetometer network. No build step. Dark-themed UI with Chart.js. Has a Python `proxy.py` for local data fetching.

**Stack:** HTML + JS + Chart.js. `dsp.js` and `dsp.worker.js` handle signal processing in a Web Worker.

---

### `pca-engine`
**Purpose:** Empty repository — no files yet.

---

## Cross-Cutting Notes

- **Shared sensor file:** `L058.txt` (29-station global magnetometer array positions) appears in multiple Python repos. It's the standard sensor configuration for ionospheric work.
- **`magsim` as shared dependency:** The `magnetometer-time-series-simulator` package is used by `magnetic-source-identification` and appears as a submodule inside `GIBF`.
- **Research pipeline direction:** `lab-notebooks` (exploration) → `magnetometer-time-series-simulator` (simulator) → `magnetic-source-identification` (ML experiment) → `mhd-ibf-reconstruction` / `GIBF` (physics-based reconstruction).
- **Web stack pattern:** Most Sites repos use React + Vite + Tailwind + GitHub Pages. `@settgast/ui` is the shared component library used in `dynamica` and available for new projects.
- **Job search context (as of 2026-06-30):** `application-tracker` and `resume-tracker` both exist and are active — Strider is in a multi-track job + PhD search.
