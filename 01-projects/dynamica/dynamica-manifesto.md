---
title: Dynamica Manifesto — Project Spine and Design Decisions
type: project
domain: general
status: active
created: 2026-06-30
updated: 2026-06-30
tags:
  - meta/repos
  - meta/dynamica
  - project/dynamica
---
# Dynamica Manifesto — Project Spine and Design Decisions

> Source: `C:\Users\strid\Downloads\manifesto.md` — the single source of truth for Dynamica. Every SPEC, design, and CLAUDE.md inherits from this file.

---

## The thesis

Finance, neuroscience, and physics are running the same mathematics. The site sells the **connection** between widgets, not the widgets. Correlation is correlation whether it measures portfolio diversification, neuron co-firing, or sensor array wavefronts. The toys are evidence; the thesis is the product.

Dynamica is simultaneously a **portfolio piece** (must never render broken in front of a recruiter) and a **learning project** (must be honest and rigorous enough to teach). Those two goals are co-equal and pull cuts in opposite directions — the invariants below serve both.

---

## Studios (three substrates)

**This is different from the current codebase.** The manifesto replaces **SignalViz** with **PhySim**. The current `studios.ts` still says SignalViz — the migration to PhySim is pending.

| Studio | Domain | Notes |
|--------|--------|-------|
| **QuantViz** | Finance | Seed studio. CorrelationLab is the reference implementation. |
| **NeuroLearn** | Neuroscience | LIF neuron is the seed model (ported from LIF-project stub). |
| **PhySim** | Physical & engineered systems | Replaces SignalViz. Contains mechanics (n-body, pendulums), stat-mech/thermodynamics, waves, and a **Signals & Systems neighborhood** (LTI, sampling, filtering, beamforming). DSP toys live here, not in a standalone SignalViz studio. |

---

## Math taxonomy

**Two families:** Dynamics (how systems *evolve*) and Analysis (how we *measure and decompose*).

### Core tools (M1–M8) — each gets a full three-substrate triple and a tool page

| # | Tool | Family |
|---|------|--------|
| M1 | Correlation & Covariance | Analysis |
| M2 | Fourier & Spectral Analysis | Analysis |
| M3 | Convolution & Filtering | Analysis |
| M4 | Stochastic Processes | Dynamics |
| M5 | Differential Equations & Dynamical Systems | Dynamics |
| M6 | Linear Algebra & Dimensionality Reduction (PCA/SVD) | Analysis |
| M7 | Detection & Estimation (matched filter, Kalman, SDT) | Analysis |
| M8 | Information Theory & Entropy | Analysis |

### Secondary (M9–M14) — tags only at launch, no dedicated tool pages
M9 Probability & Tails · M10 Markov/HMM · M11 Optimization · M12 Networks/Graphs · M13 Time-Frequency/Wavelets (child of M2) · M14 Nonlinear Dynamics/Chaos (child of M5)

### Strongest triples (prioritize these tool pages first)
- **M3 Convolution:** moving average (finance) = receptive field (neuro) = heat equation as Gaussian convolution (physics)
- **M4 Stochastic:** GBM (finance) = Poisson spikes (neuro) = Brownian motion (physics — the original)
- **M8 Information:** entropy as diversification = neural coding = Shannon meets thermodynamic entropy

**Cleanest launch tool pages: M1, M3, M4, M5.** M2 and M7 are fast-follows.

---

## Module map (dependency DAG)

```
        settgast-ui ─┐
                     ▼
  Compute Core ──► Model Shell ──► Models ──► Registry ──► Navigation
        ▲                            ▲
   Data Layer ───────────────────────┘
```

### Compute Core — `src/lib/`
Pure, deterministic, framework-free TypeScript functions. The literal connective tissue. Owns the single canonical implementation of every M1–M8 tool and its tests (`pearson`, `fft`, `convolve`, `pca`, `matchedFilter`, `integrateODE`…). **No React, no DOM, no I/O.** Leaf node — most stable code in the repo. Unit tests with known-value fixtures are the merge gate.

### Data Layer — `src/data/`
Static-bake pipeline (Python + yfinance via CI cron) + live client fetch (Stooq → Yahoo via CORS-proxy chain) + synthetic fallback. Exposes typed series to models. Mostly a QuantViz concern — NeuroLearn and PhySim models are predominantly simulated, not fetched.

### Model Shell — `src/shell/`
The one skeleton every toy wears, built on `@settgast/ui`. Owns: anatomy layout (metadata → controls → viz → narrative → cross-link footer), shared control primitives including the **mathjs expression input**, URL-hash state encode/decode.

### Models — `src/models/<id>/`
One interactive toy each = metadata + control config + viz + narrative. Composed from Shell, computing via Compute Core. Each model belongs to exactly one studio and carries ≥1 math tag.

### Registry — `src/models/registry.ts`
Single source of truth: `{ id, title, studio, mathTags[], blurb, difficulty }` per model. Drives both browse modes and the cross-link matrix. Is data only — nothing renders from it but Navigation.

### Navigation — `src/pages/`
Landing page, studio indexes, tool indexes, cross-link matrix. **Derives everything from Registry, asserts nothing.** Top of the DAG; nothing depends on it.

---

## Success criteria (measurable)

| | Criterion | Check |
|--|-----------|-------|
| S1 | Every shipped math tool is correct | Vitest unit tests with known-value fixtures; `npm test` green is merge gate |
| S2 | No cross-link is a lie | Registry check: every model tagged `M1` imports the same canonical correlation fn |
| S3 | Thesis fully covered | Every M1–M8 has ≥1 model in each of the three studios (no empty cells in cross-link matrix) |
| S4 | Dual nav is derived, not duplicated | Grep proves no second hand-maintained list |
| S5 | Nothing renders broken offline | Every model produces valid (possibly synthetic, labeled) view with network disabled |
| S6 | Every view is shareable | Full state encodes in URL hash; `decode(encode(state)) === state` unit test |
| S7 | "Wow" lands | Editorial — flagship model delivers one non-obvious sentence; tool page delivers clean three-field triple |

---

## Non-negotiable invariants

1. **One tool, one implementation.** Compute Core only. Never reimplement a tool inside a studio. If two studios' "correlation" aren't the same function, the cross-link is a lie. (S2)
2. **Dual nav is derived, never asserted.** Studio pages, tool pages, and matrix all build from one Registry. Never hand-maintain a second list.
3. **Compute Core is pure and tested. Always.** No I/O, no React, no DOM in `lib/`. A tool without passing known-value tests is not done.
4. **Every model obeys the anatomy.** metadata → controls → viz → narrative → cross-link footer. A toy that won't fit the shell is a shell bug to escalate, not a snowflake.
5. **Graceful degradation, always.** Live data → bundled snapshot → clearly-labeled synthetic. Never renders broken or empty.
6. **Every view is shareable.** Full state in URL hash.
7. **Static-only at runtime.** No backend, no auth, no database.

---

## Open questions (as of 2026-06-30)

- **CORS-proxy fragility** — public proxies are flaky and rate-limited. Synthetic fallback is the safety net. Possible future: self-hosted/serverless proxy or scheduled job → KV store.
- **Launch slice / cuts** — which marginal models get dropped; exact first build set.
- **Third-studio name** — `PhySim` vs `PhysViz`. Cosmetic; lock before registry hard-codes it.
- **Data dependence of NeuroLearn / PhySim** — most models are simulated, not fetched; confirm before specs assume it.

---

## Recommended launch slice

12 models across 4 tool pages — the minimum that proves dual-nav thesis end to end.

**Tools to launch:** M1, M3, M4, M5 (complete triples). M2 and M7 as fast-follows.

| Studio | Models |
|--------|--------|
| QuantViz | CorrelationLab (M1, done), Random-Walk vs Markets (M4), Mean-Reversion/OU (M5), Moving-Averages-as-Filters (M3) |
| NeuroLearn | LIF neuron (M5, port stub), Cross-Correlogram (M1), Spike-Train/Poisson (M4), Receptive Fields (M3) |
| PhySim | Convolution/Heat-equation visualizer (M3, canonical), Beamforming + inverse beamforming (M1), Brownian motion (M4), n-body or pendulum phase plane (M5) |

---

## Downstream SPECs implied

1. `SPEC: compute-core` — function signatures, purity rules, known-value test fixtures (S1), registry check (S2)
2. `SPEC: model-anatomy` — metadata schema, control primitives (incl. mathjs expression input), viz-surface slots, narrative block, cross-link footer, URL-state codec (S6)
3. `SPEC: data-layer` — static-bake pipeline, live-fetch proxy chain, TTL/caching, synthetic-fallback contract (S5)
4. `SPEC: registry-and-nav` — registry schema, derivation of studio indexes, tool indexes, cross-link matrix (S3, S4)
5. Per-model SPECs — one per launch model, inheriting from root

---

## Tech stack (root-level only)

React 19 + TypeScript, Vite, `@settgast/ui` on TailwindCSS, Recharts (default charts), mathjs (expression input), Vitest, Python + yfinance (data pipeline in GitHub Actions weekday cron), GitHub Pages (static deploy).
