---
title: Realized Volatility Prediction — Deep Learning Project 2
type: project
domain: machine-learning
status: active
created: 2026-06-30
updated: 2026-07-01
tags:
  - machine-learning/time-series
  - finance/volatility
---

# Realized Volatility Prediction — Deep Learning Project 2

**Repo:** https://github.com/Stridasaurus/realized-volatility-prediction
**Class:** MTH / DL course project 2 · due ~2026-07-07
**Compute:** Google Colab (free tier) · **HP search:** Optuna · **Tracking:** lightweight JSON/parquet artifacts

**Manifesto locked:** `C:\Users\strid\Downloads\MANIFESTO.md` (regenerated 2026-06-30/07-01, supersedes the earlier `Desktop\Prompts\Class\RV-pred\MANIFESTO.md` copy — not yet reconciled/moved into the repo) is the single source of truth, produced via the [[agentic-document-cascade]] Decide phase (Roadmap → Manifesto, in a separate Claude.ai Project). Next artifacts are the per-module `SPEC.md`s, written in Claude Code against the repo.

**Manifesto v2 delta (not yet folded into the tables below — full review/refine pass still pending):**
- Target named honestly as a **range-variance proxy** (Garman–Klass), explicitly distinguished from canonical high-frequency RV — the project *tests* whether HAR's dominance transfers rather than assuming it.
- **Stage 3 upgrade re-specified:** an overnight-inclusive daily target (per-day Rogers–Satchell + overnight², or windowed Yang–Zhang) computable from the *same* OHLC snapshot — no new data — repairs the QLIKE-unbiasedness caveat below. A PK+GK+RS blend is demoted to an optional robustness footnote only.
- **QLIKE bias caveat (new):** QLIKE's proxy-robustness (Patton 2011) assumes a conditionally unbiased proxy; GK omits the overnight return and is biased low for total daily variance — report RMSE alongside, don't lean on QLIKE alone.
- **Adjustment-invariance nuance (new):** open-to-close estimators (GK/PK/RS) are invariant to proportional price adjustment; the Stage-3 overnight-inclusive target is **not** (crosses the dividend-adjustment boundary) and requires the adjusted basis.
- **Forecastability floor vs. ceiling framing (new):** the base project claims a floor only (beat/tie HAR = signal-beyond-HAR is *at least* that much); the target's own noise ceiling is a deliberate Stage-3 analysis, not a base-pipeline deliverable.

## Research Question

Can a deep sequence model beat the HAR benchmark at forecasting realized volatility, does any improvement survive honest out-of-sample validation, and *where does the edge live*? Economic significance (does the edge convert to money) is an explicit separate follow-on project, specced but not built here.

## Core Design Constraint

**Shared library, thin notebooks.** All shared logic lives in `src/` as importable Python; notebooks configure one experiment, call the library, save artifacts. Guarantees consistent metrics across experiments by construction — if two experiments could disagree on RV construction, splitter, metrics, baselines, model harness, or artifact format, the comparison is void.

## Module Map (`src/`)

| Module | File(s) | Owns | Depends on |
|---|---|---|---|
| data | `src/data.py` | Snapshot loading, Garman–Klass RV construction, trading-day calendar | snapshot only (no network at experiment time) |
| features | `src/features.py` | Leak-safe feature matrix, Tier 1/2/3 aux menu, scalers (fit train-only) | `data` |
| splits | `src/splits.py` | The one canonical walk-forward splitter, embargo gap, monthly retrain folds | nothing |
| metrics | `src/metrics.py` | `qlike()`, `rmse()`, Diebold–Mariano test, variance-space discipline | nothing |
| baselines | `src/baselines.py` | HAR (the real bar), GARCH(1,1) (context only) | `data`, `splits`, `metrics` |
| model + harness | `src/models.py`, `src/train.py` | Frozen small-LSTM family, seeded leak-safe train/eval loop, log-RV modeling, QLIKE loss | `features`, `splits`, `metrics` |
| io / artifacts | `src/io.py` + `results/` schema | `config.json`/`preds.parquet`/`metrics.json` save/load contract | nothing (used by all) |

Open carve question: whether `models`+`train` stay one module or split, and whether `baselines` splits HAR/GARCH — default is one each.

## Key Decisions (frozen)

| Decision | Choice |
|----------|--------|
| Data sources | Stooq (SPY OHLCV) + CBOE (VIX OHLC), frozen checksummed snapshot; FRED reserved for portfolio-stage cross-asset features |
| RV estimator | Garman–Klass (daily OHLC); intraday 5-min = stretch |
| Architecture | Small LSTM (1–2 layers, frozen family); Optuna tunes sizes only, never the family |
| Targets | h=1 (next-day) spine + h=5 (next-week, avg daily RV), forecast directly (not iterated) |
| Modeled quantity | log-RV (near-lognormal); exponentiate back to level space for scoring |
| Training loss | QLIKE-with-floor (primary); fallback MSE-of-log-RV |
| Evaluation metrics | QLIKE (primary, variance space), RMSE (secondary) |
| Significance | Diebold–Mariano test vs. HAR on the QLIKE loss differential, p-value per model |
| Temporal split | Train 2005–2017 (incl. 2008) · Val 2018–2019 · Test 2020–present (COVID, 2022 bear, calm) · embargo gap |
| Walk-forward | Monthly retrain inside test region |
| Seeds | ~5 dev, ≥10 for headline; report mean ± std, edge must exceed seed spread |
| Checkpoint storage | `config`/`preds`/`metrics` → git (they are the deliverable); best weights → Google Drive |

## Project-Level Success Criteria (S1–S7, executable)

| # | Criterion | Check |
|---|---|---|
| S1 | The bar exists | HAR + GARCH(1,1) scored on frozen splits, `metrics.json` has finite HAR QLIKE |
| S2 | Reproducible from nothing | Clean clone + frozen snapshot + pinned `requirements.txt` runs end-to-end; snapshot SHA-256 matches |
| S3 | No lookahead, provably | Future-perturbation leakage test passes; scaler fit-indices ⊆ train indices |
| S4 | Results are pure replay | `99_evaluation` rebuilds the headline table from saved artifacts, retrains nothing |
| S5 | Significance reported, not asserted | DM test vs HAR emits a p-value per model |
| S6 | Edges survive seed noise | Headline numbers mean ± std over ≥10 seeds; edge exceeds seed spread |
| S7 | Edge decomposition pre-committed | The three "where the edge lives" cuts computed and reported regardless of win/tie/loss |

## Stages (grade-ready, then portfolio — never start the next until the previous is locked)

- **Stage 0 — Harness.** Data snapshot + RV construction + frozen splits + metrics + HAR + GARCH scored. Everything after is upside.
- **Stage 1 — Tuned net + controlled comparison.** Leak-safe Optuna search → one frozen HP set; RV-only net vs HAR on identical inputs.
- **Stage 2 — Real results (grade-ready cut).** RV+aux experiment, decay curve, final evaluation notebook. Lock and save before any stretch.
- **Stage 3 — Portfolio extensions.** Intraday 5-min RV → realized semivariance; multi-asset robustness; data refresh/cross-check; then the economic-significance follow-on as its own project.

## Experiments (notebooks — thin, call the library)

1. **00** — Data + baselines (HAR, GARCH)
2. **01** — HP search (Optuna, leak-safe, validation region only)
3. **02** — RV-only net vs HAR
4. **03** — RV + aux features (Tier 1: lagged returns, day/night split, volume surprise, range estimators, calendar flags; Tier 2: VIX, VIX term structure, VVIX)
5. **04** — Decay: expanding vs rolling window, one curve, not a grid
6. **99** — Evaluation only (loads artifacts, never recomputes)

## Pre-committed Analysis ("where the edge lives")

Three cuts computed before peeking at test results: (1) by volatility regime (calm vs. post-shock), (2) by horizon (h=1 vs h=5), (3) source — architecture vs. aux features (falls out from 02 vs 03).

## Hard Invariants (violation silently invalidates the project)

- Never shuffle the time series; all splits chronological.
- Fit scalers on training data only, apply forward.
- Every feature at day *t* uses only information known at close of day *t*, never revised.
- Test region touched exactly once — never influences any hyperparameter/feature/window choice.
- One splitter, one metrics definition, imported everywhere — never copy-pasted into a notebook.
- Frozen controls (architecture family, tuned HPs, window length, retrain cadence) identical between RV-only and RV+aux — the only variable is the input feature set.
- Score QLIKE in variance space; never mix volatility and variance.
- Never report a single-seed result as an edge.

## Open Items

- [ ] Exact split boundaries in trading days
- [ ] Rolling-window length for decay study (default ~2 yrs)
- [ ] LSTM input sequence length (candidate for Optuna search)

## Next Action

Write the dependency-ordered SPEC.md set in Claude Code, starting with `splits/SPEC.md` and `metrics/SPEC.md` (everything downstream trusts these), then `data/SPEC.md`, `features/SPEC.md`, `baselines/SPEC.md`, `model+harness/SPEC.md`, `io/SPEC.md`. Then build Stage 0 (data pipeline + HAR/GARCH baselines, notebook 00).

## Future Work (specced but deferred)

Economic significance via volatility-targeting: size positions inversely to predicted risk, equalize exposure, charge transaction costs, cap leverage. The QLIKE edge may or may not survive into real Sharpe — a legitimate result either way.
