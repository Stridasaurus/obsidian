---
title: EM-Globe — Full-Wave EM Solver for the Ionosphere-Earth System (Proposal)
type: project
domain: space-physics
status: draft
created: 2026-06-30
updated: 2026-06-30
tags:
  - space-physics/computational-em
  - space-physics/magnetometry
---

# EM-Globe — Full-Wave EM Solver for the Ionosphere-Earth System

**Status:** Planning document / funding proposal  
**Timeline:** 3-year project, three phases  
**Development model:** Agent-driven modular construction (9 independent modules)

## The Gap

All operational ground magnetometer inversions (SECS, Lompe, spherical harmonic cap) use a **real, frequency-independent** transfer matrix — the quasi-static approximation. This breaks down when:
- Array aperture × signal frequency means propagation phase is non-negligible
- Frequencies enter VLF where reflection and displacement currents matter
- Ionospheric conductivity must be a full 3×3 tensor (Hall, Pedersen, field-aligned)
- Earth has strong 3D heterogeneous conductivity
- One wants complex phase diversity for GIBF-style beamforming

The Fukushima theorem (CF current → zero ground field) is exact only at DC for radial geometry. At finite frequencies, CF leaks — but quantifying this requires a full-wave solver.

## What EM-Globe Computes

Complex magnetic field phasor `B(r,ω)` at ground stations due to arbitrary 3D ionospheric/magnetospheric currents, accounting for:
- Anisotropic ionosphere (Pedersen σ_P, Hall σ_H, field-aligned σ_∥)
- 3D heterogeneous Earth conductivity
- Full Maxwell equations in frequency domain
- Open boundaries (PML or BEM)

## Key Technical Approach

**Reciprocity for transfer matrix efficiency:** Instead of one solve per source (thousands of grid points), solve only 3×N_stations reciprocal problems per frequency (one per receiver/orientation). The magnetic field at a receiver from a source equals the electric field at the source from a magnetic dipole at the receiver. Massive speedup.

**Core solver:** Curl-conforming FEM (Nédélec edge elements) on unstructured tetrahedral meshes; FGMRES/BiCGSTAB with multigrid preconditioners via PETSc.

## 9 Modules (agent-driven development)

| Module | Purpose |
|--------|---------|
| M1 | Ionosphere-Earth conductivity builder (IRI + MSIS + IGRF) |
| M2 | Source discretization and current injection |
| M3 | Frequency-domain Maxwell FEM solver |
| M4 | Green's function extraction via reciprocity → complex transfer matrix |
| M5 | High-level pipeline: mesh generation + end-to-end `build_complex_A()` |
| M6 | Validation suite (analytic benchmarks, convergence, cross-code) |
| M7 | HPC and parallelization wrappers (PETSc/DMPlex, SLURM) |
| M8 | Python user API (`emglobe` package) |
| M9 | Documentation and community tutorials |

## Known Research Gaps (human-intervention required)

1. **Reciprocity for gyrotropic media** (M4) — Hall terms break standard Lorentz reciprocity; adjoint operator must be derived (reverse sign of σ_H or use reversed-B₀ reciprocity). Critical — would silently invalidate all results.
2. **Solver robustness for extreme anisotropy** (M3) — σ_∥ can be 10³–10⁵× larger than σ_P/σ_H; creates near-null space for curl-curl; standard preconditioners likely fail. Mitigation: start with thin-sheet ionosphere approximation.
3. **Stable absorbing boundaries** (M3) — PML may go unstable for anisotropic inhomogeneous media; BEM hybrid may be safer.
4. **Source singularity regularization** (M2) — delta-function sources in FEM are non-convergent; use mollification or subtraction method.
5. **Multi-scale mesh generation** (M5) — domain spans Earth core to several thousand km altitude; ionospheric shell needs ~km resolution.
6. **Analytic validation benchmarks** (M6) — very few known solutions for anisotropic ionosphere + conductive Earth; must be derived.

## Science Demonstrations (Phase 3)

1. CF observability atlas: map where/when CF signals reach ground as function of frequency, latitude, array geometry
2. Phase-diverse source separation: re-run SECS-GIBF experiments with complex transfer matrix
3. Joint ionosphere–Earth inversion: simultaneous recovery of external sources + subsurface conductivity

## Connection to Other Projects

EM-Globe is the **long-term upstream project** that would give SECS-GIBF the complex transfer matrix it currently lacks. The SECS-GIBF viability test (see [[20260630-secs-gibf-viability]]) is the immediate precursor — it quantifies exactly how much the real/quasi-static kernel limits performance, motivating EM-Globe.

## Likely Journals

JGR Space Physics, Earth Planets Space, Geophysical Journal International, Radio Science
