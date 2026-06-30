---
title: Realized Volatility Prediction — Deep Learning Project 2
type: capture
domain: machine-learning
status: draft
created: 2026-06-30
updated: 2026-06-30
tags:
  - machine-learning/time-series
  - finance/volatility
---

# Realized Volatility Prediction — Deep Learning Project 2

**Repo:** https://github.com/Stridasaurus/realized-volatility-prediction  
**Class:** MTH / DL course project 2  
**Compute:** Google Colab · **HP search:** Optuna · **Tracking:** lightweight JSON artifacts

## Research Question

Can a deep sequence model beat the HAR benchmark at forecasting realized volatility — and does any improvement survive honest out-of-sample validation and translate into economic value?

## Core Design Constraint

**Shared library, thin notebooks.** All shared logic (RV construction, walk-forward splitter, metrics, baselines, model def, artifact I/O) lives in `src/` as importable Python. Notebooks configure one experiment, call the library, save artifacts. Guarantees consistent metrics across experiments by construction.

## Key Decisions (frozen)

| Decision | Choice |
|----------|--------|
| RV estimator | Garman–Klass (daily OHLC); intraday 5-min = stretch |
| Architecture | Small LSTM (1–2 layers, frozen family); Optuna tunes sizes |
| Target | log-RV (near-lognormal); exponentiate back for scoring |
| Training loss | QLIKE (primary); fallback MSE-of-log-RV |
| Evaluation metric | QLIKE (primary), RMSE (secondary) |
| Temporal split | Train 2005–2017 · Val 2018–2019 · Test 2020–present · few-day embargo |
| Walk-forward | Monthly retrain inside test region |
| Seeds | ~5 dev, 10 for headline; report mean ± std |
| Checkpoint storage | Results → git; best weights → Google Drive |
| Experiment tracking | Lightweight JSON + parquet artifacts |

## Experiments (5 notebooks)

1. **00** — Data + baselines (HAR, GARCH). HAR is the real benchmark; GARCH is context only.
2. **01** — HP search (Optuna, leak-safe, validation region only)
3. **02** — RV-only net vs HAR (same info as HAR, different model)
4. **03** — RV + aux features (Tier 1: lagged returns, day/night split, volume surprise, range estimators, calendar flags; Tier 2: VIX, VIX term structure, VVIX)
5. **04** — Decay: expanding vs rolling window, one curve, not a grid
6. **99** — Evaluation only (loads artifacts, never recomputes)

## Pre-committed Analysis ("where the edge lives")

Three cuts computed before peeking at test results:
1. By volatility regime (calm vs. post-shock)
2. By horizon (h=1 vs h=5)
3. Source: architecture vs. aux features (falls out from 02 vs 03)

## Open Items

- [ ] Exact split boundaries in trading days
- [ ] Rolling-window length for decay study (default ~2 yrs)
- [ ] LSTM input sequence length (candidate for Optuna search)

## Phase Order (deadline-safe)

Phase 1 → Phase 2 (tuned net + RV-only vs HAR) → Phase 3 (RV+aux + decay) → stretch (intraday RV, multi-asset)

**Rule:** do not start stretch until Phase 3 is locked and saved.

## Future Work (specced but deferred)

Economic significance via volatility-targeting: size positions inversely to predicted risk, equalize exposure, charge transaction costs, cap leverage. The QLIKE edge may or may not survive into real Sharpe — a legitimate result either way.
