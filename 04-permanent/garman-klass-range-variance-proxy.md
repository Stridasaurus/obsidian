---
title: "Garman-Klass is a range-variance proxy, not canonical realized variance — it is biased low for total daily variance because it omits the overnight return, and this breaks QLIKE's unbiasedness assumption"
type: permanent
domain: machine-learning
status: active
created: 2026-07-01
updated: 2026-07-01
tags:
  - machine-learning/time-series
  - finance/volatility
---

# Garman-Klass range-variance proxy: honest framing and its biases

## Formulation

Garman–Klass (GK) estimates daily variance from OHLC (open/high/low/close) data via a weighted combination of the log high-low range and the log open-close range, e.g. GK = 0.5·(ln(H/L))² − (2ln2−1)·(ln(C/O))². It is a **range-variance proxy** computed entirely within the trading session — it is not the canonical high-frequency **realized variance (RV)** (the sum of squared intraday returns from tick/minute data), which GK approximates only under stated Brownian-motion assumptions and only for the open-to-close portion of the day. GK, Parkinson (PK, high-low range only), and Rogers–Satchell (RS, drift-robust range estimator) are all open-to-close estimators sharing this same omission.

## Constraints & Invariants

- **GK omits the overnight (close-to-next-open) return entirely**, so it is biased low for *total* daily variance whenever overnight variance is nonzero (true for essentially any asset with an overnight session) — do not present a GK-trained model's numbers as "realized volatility forecasting" without this caveat; name the target honestly as a range-variance proxy.
- **QLIKE-unbiasedness breaks under this omission**: QLIKE's proxy-robustness property (Patton 2011) — that ranking models by QLIKE against a *noisy but conditionally unbiased* proxy still recovers the true ranking — assumes the proxy is conditionally unbiased for the true target. Since GK is systematically biased low (missing overnight variance), this assumption does not fully hold; report RMSE alongside QLIKE rather than relying on QLIKE alone.
- **Adjustment-invariance nuance:** GK/PK/RS (open-to-close estimators) are invariant to proportional price adjustment (e.g. retroactive dividend/split adjustment scales all four OHLC prices by the same factor, canceling out of any log-ratio). An overnight-inclusive target (e.g. RS + overnight², or a windowed Yang–Zhang estimator) is **not** adjustment-invariant, because it spans the corporate-action boundary — computing it requires committing to the adjusted price basis, unlike the base open-to-close estimators.
- **Floor vs. ceiling framing:** a model beating/tying an HAR benchmark on the GK proxy establishes only a *floor* on extractable signal (signal-beyond-HAR is *at least* that much) — it says nothing about the proxy's own irreducible noise ceiling relative to true RV. Treating a floor result as if it measured the ceiling overstates the finding.

## Connections

[[leak-safe-time-series-validation]] — the validation discipline this target is evaluated under
[[rv-prediction]] — active project; GK is Stage 0/1's target, with an overnight-inclusive upgrade specced (not yet built) for Stage 3

## Open Questions

Whether the Stage-3 overnight-inclusive target (RS+overnight² or windowed Yang–Zhang) will be built in [[rv-prediction]] this cycle — currently specced only, deferred behind Stage 0–2.

## Sources

RV-prediction manifesto v2 (`Downloads\MANIFESTO.md`, 2026-07-01) — Patton 2011 (QLIKE robustness) and the original Garman–Klass 1980 paper not yet captured as literature notes.
