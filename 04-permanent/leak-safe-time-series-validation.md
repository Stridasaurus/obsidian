---
title: "Leak-safe time-series model validation requires chronological splits, train-only-fit scalers, an embargo gap, and a test region touched exactly once"
type: permanent
domain: machine-learning
status: active
created: 2026-07-01
updated: 2026-07-01
tags:
  - machine-learning/time-series
---

# Leak-safe time-series validation checklist

## Formulation

A time-series forecasting evaluation is leak-safe only if every one of the following holds jointly (each alone is necessary but not sufficient): (1) splits are strictly **chronological** — never shuffle, since shuffling lets future information contaminate past predictions via any statistic computed across the shuffled set; (2) any preprocessing statistic (scaler mean/std, feature normalization) is **fit on the training partition only**, then applied forward to validation/test — never fit across the full dataset; (3) each feature at time t uses **only information known at or before the close of day t**, and that information is never later revised (no restatement leakage); (4) an **embargo gap** separates train from validation/test so a feature with a lookback window can't straddle the boundary; (5) the **test region is touched exactly once**, at the very end — it must never influence any hyperparameter, feature, or window-length choice upstream, including indirectly via a validation loop that peeked at it; (6) **walk-forward evaluation** (e.g. monthly retrain windows) inside the test region, rather than a single train/test cut, to average out regime-specific luck; (7) **one canonical splitter and one canonical metrics implementation**, imported everywhere and never copy-pasted into a notebook — divergent reimplementations are a silent way for two experiments to become incomparable.

## Constraints & Invariants

- Violating any one of these **silently invalidates** a project's headline result rather than crashing it — there is no error message for a leaked backtest, only an over-optimistic number. Treat this list as a checklist to assert in code (e.g. "scaler fit-indices ⊆ train indices" as an executable test), not merely a design principle.
- **Frozen controls matter as much as the split**: when comparing two feature sets (e.g. baseline vs baseline+aux) or two models, everything except the one variable under test (architecture family, tuned hyperparameters, window length, retrain cadence) must be held identical between the two arms, or the comparison conflates the intended variable with an accidental confound.
- **Report significance, not just point estimates**: use a paired test appropriate to the loss differential (e.g. Diebold–Mariano on the loss differential against a benchmark) and report edges as mean ± std over multiple seeds (≥10 for a headline claim) — a single-seed win is not evidence of an edge, since seed noise alone can produce it.

## Connections

[[garman-klass-range-variance-proxy]] — the target-construction side of the same project this checklist was hardened on
[[agentic-document-cascade]] — this checklist is exactly the kind of "hard invariant" content the manifesto layer is meant to carry verbatim into the build phase

## Open Questions

None currently open — this is a settled methodological checklist, not an active research question, in [[rv-prediction]].

## Sources

Derived directly from the RV-prediction manifesto (`Downloads\MANIFESTO.md`, v2 as of 2026-07-01, superseding `Desktop\Prompts\Class\RV-pred\MANIFESTO.md`) — no external literature note yet; general time-series-validation literature (e.g. Diebold & Mariano 1995 for the significance test) not yet cited in a lit note.
