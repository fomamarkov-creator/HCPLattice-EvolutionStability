# HCP Lattice Geometry & Evolution Scheme Stability in Lean 4

Formal machine verification in **Lean 4** (Mathlib) covering 12-neighbor HCP lattice geometry and stability bounds for numerical evolution schemes.

## Author & Reference

- **Author:** E. S. Markov (Independent Researcher, Astrakhan, RF) — ORCID: `0009-0005-2235-5464`
- **Monograph:** E. S. Markov, *Discrete Kinematics of the Spatial Matrix* (2026), DOI: `10.5281/zenodo.20317598`

## Formalized Modules (Mathlib4 PRs)

1. **`HCPLattice.lean`** (`Mathlib4/PR #46197`):
   - Unit Euclidean lengths for 12 nearest neighbors (`normSq_shiftVec`), vanishing first-order drift (`sum_shiftVec_zero`) and cubic moments (`sum_symmetric_cubic_moments_zero`).
   - Moment tensor isotropy (`4 I₃`) and discrete HCP Laplacian quadratic consistency (`discreteLaplacian_quadratic_exact`).
2. **`EvolutionSchemeStability.lean`** (`Mathlib4/PR #46199`):
   - Subspace invariance (`ker div`) under explicit steps (`div_explicitStep_eq_zero`).
   - Energy dissipation under CFL bounds (`norm_sq_explicitStep_le`) and unconditional Crank–Nicolson dissipation (`norm_sq_crankNicolson_le`).
   - Initial-state Lipschitz stability (`norm_explicitStep_sub_le`).

## Build & Verification

Verified in **Lean 4** without `sorry` or custom axioms:
```bash
lake exe cache get
lake build
```

## Dual Licensing

Dual-licensed under **AGPL-3.0** (`LICENSE`) and **Apache 2.0** (`LICENSE-APACHE`) for scientific reproducibility and Mathlib4 compatibility.
