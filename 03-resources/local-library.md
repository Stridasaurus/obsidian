---
title: "Local PDF Library — Textbooks and Reference Papers"
type: reference
domain: general
status: active
created: 2026-06-30
updated: 2026-07-01
tags:
  - meta/resources
source: ""
source_url: ""
---

Local PDF collection. All files are on the desktop and accessible to Claude during sessions.

## IBF / SECS / GIBF Papers

`C:\Users\strid\Desktop\School\IBF_Project\`

| File | Description |
|---|---|
| `SECS.pdf` | **Correction (2026-07-01): not a standalone SECS paper.** Byte-identical to `Ionospheric SECS.pdf` (same MD5) — both are the full 296-page ISSI Scientific Report Series 17 book, *Ionospheric Multi-Spacecraft Analysis Tools* (Dunlop & Lühr, eds., 2020, open access). Chapter 2 (Vanhamäki & Juusola, "Introduction to Spherical Elementary Current Systems," pp. 5-33) is the SECS review — see [[vanhamaki-juusola-2020-notes]]. Other chapters cover FAC estimation, Curlometer, AMPERE, and Swarm-specific applications, not yet read. |
| `Ionospheric SECS.pdf` | Duplicate of `SECS.pdf` — same file, different filename. See above. |
| `GIB.pdf` | **Correction (2026-07-01): was mislabeled.** Not "Geomagnetic induction in bodies" (a guess from the filename, never verified). Actually Zavala et al. 2010, "Generalized Inverse Beamforming Investigation and Hybrid Estimation" (BeBeC-2010-10) — an **acoustic** beamforming paper validating Suzuki-style GIB. Read in full once; no literature note kept (nothing in the active project depends on it beyond what [[suzuki-2011-gibf]] already covers) — re-read directly if needed again. |
| `Suzuki GIBF.pdf` | Suzuki 2011, *J. Sound Vib.* 330: 5835-5851 — the actual GIBF method paper. Confirmed by reading: an **aeroacoustics** paper (phased-microphone-array noise-source localization), not a space-physics paper — the mag-GIBF project transplants this algorithm onto a real-valued SECS transfer kernel. See [[suzuki-2011-gibf]]. |
| `Elastic Net.pdf` | Li, Tong & Jiang 2014, "Sound Source Localization via Elastic Net Regularization" (BeBeC-2014-02) — acoustic beamforming, alternative sparse regularizer to GIBF's L1-IRLS. Read in full once; no literature note kept (not currently used by the active project) — re-read directly if it becomes relevant. |

## Textbooks

`C:\Users\strid\Desktop\School\Textbooks\`

### Physics & Electromagnetism
| File | Description |
|---|---|
| `griffiths_4ed.pdf` | Griffiths — *Introduction to Electrodynamics* (4th ed) |
| `E&M_solutions_manual.pdf` | E&M solutions manual (likely Griffiths companion) |
| `Fundamentals of Physics [10th Edition] - Halliday & Resnick.pdf` | Halliday & Resnick — *Fundamentals of Physics* (10th ed) |
| `Modern_Physics_Formulas.pdf` | Modern physics formula reference |
| `ONeill.pdf` | O'Neill — likely *Semi-Riemannian Geometry* |
| `Quantum Gravity.pdf` | Quantum gravity reference |

### Quantum Mechanics
| File | Description |
|---|---|
| `Griffiths - Introduction to Quantum Mechanics 3rd ed 2018.pdf` | Griffiths QM (3rd ed) |
| `Quantum - Sakurai.pdf` | Sakurai — *Modern Quantum Mechanics* |
| `pdfcoffee.com_mahesh-c-jain-qmpdf-pdf-free.pdf` | Mahesh C. Jain QM problems/supplement |

### Mathematics
| File | Description |
|---|---|
| `Fundamentals of Differential Equations and Boundary Value Problems (7th Edition).pdf` | Nagle, Saff et al. — ODEs & BVPs |
| `William L. Briggs ... Calculus Early Transcendentals (3rd Ed) (2018).pdf` | Briggs et al. — Calculus |
| `Students Guide to Vectors and Tensors.pdf` | Fleisch — *A Student's Guide to Vectors and Tensors* |
| `Basic_Category_Theory.pdf` | Tom Leinster — *Basic Category Theory* |
| `Type_theory.pdf` | Type theory reference |
| `Brown-Churchill.pdf` | Brown & Churchill — *Complex Variables and Applications* |
| `Math--Bertsekas_Tsitsiklis_Introduction_to_probability.pdf` | Bertsekas & Tsitsiklis — *Introduction to Probability* |

### Finance & Stochastic Calculus
| File | Description |
|---|---|
| `Steve_Shreve_Stochastic_Calculus_for_Finance_I.pdf` | Shreve — *Stochastic Calculus for Finance I* |
| `stochCal2-shreve.pdf` | Shreve — *Stochastic Calculus for Finance II* |
| `analysis-of-financial-time-series-copy-2ffgm3v.pdf` | Tsay — *Analysis of Financial Time Series* |
| `Richard_A_Brealey_Stewart_C_Myers_Alan.pdf` | Brealey, Myers, Allen — *Principles of Corporate Finance* |

### Neuroscience
| File | Description |
|---|---|
| `Theoretical_neuroscience.pdf` | Dayan & Abbott — *Theoretical Neuroscience* |
| `Neuroscience Book[].pdf` | General neuroscience textbook |
| `Neurophilosophy.pdf` | Patricia Churchland — *Neurophilosophy* |
| `Effective_Information.pdf` | Tononi et al. — Effective Information / IIT reference |

### Electronics
| File | Description |
|---|---|
| `BasicElectronicsforScientistsandEngineers-2.pdf` | Eggleston — *Basic Electronics for Scientists and Engineers* |
| `Basic_Electronic++.pdf` | Electronics supplement |
| `basic electronics-an introduction to electronics for science.pdf` | Intro electronics reference |

## Notes

- `cv-strider-settgast.pdf` is in the Textbooks folder (CV, not a textbook)
- IBF_Project papers are directly relevant to [[secs-gibf-viability]] and [[neural-gibf-proposal]]
- Shreve I & II are the standard graduate stochastic calculus sequence
- **2026-07-01:** all 4 distinct IBF_Project PDFs have been read at least once. Literature notes kept only for [[suzuki-2011-gibf]] and [[vanhamaki-juusola-2020-notes]] — both corrected a real error or anchor a load-bearing permanent-note claim. Notes for the Zavala 2010 and Li 2014 papers were written and then deliberately dropped (2026-07-01): nothing in the active project depends on them, so they were scope creep rather than signal — re-read the PDFs directly if that changes. Fukushima 1976 and Wax & Kailath 1985 are cited within these but their own papers are not present as local PDFs — still unread.
