# HCP Lattice Geometry & Evolution Scheme Stability in Lean 4

Formal machine verification in **Lean 4** (Mathlib) covering 3D Hexagonal Close-Packed (HCP) lattice geometry, optimal sphere packing density, second-order finite-difference convergence, rational barrier regularizers, and energy dissipation bounds for numerical evolution schemes.

## Author & Reference

- **Author:** E. S. Markov (Independent Researcher, Astrakhan, RF) — ORCID: `0009-0005-2235-5464`
- **Monograph:** E. S. Markov, *Discrete Kinematics of the Spatial Matrix: Finite-Difference Foundations and Continuum Convergence Metrics* (2026), DOI: `10.5281/zenodo.20317598`

## Formalized Modules

All five modules compile cleanly in **Lean 4** over exact real arithmetic (`ℝ`) without `sorry` or custom axioms (and passed full `mathlib4` CI verification in PRs `#46197`, `#46199`, `#46205`, `#46207`, `#46209`):

1. **`HCPLattice.lean`** (`Mathlib4 PR #46197`):
   - Unit Euclidean norm of all 12 nearest-neighbor displacement vectors across even and odd stacking layers (`normSq_shiftVec`).
   - Exact vanishing of first-order drift (`sum_shiftVec_zero`) and reflection-odd cubic moments (`sum_symmetric_cubic_moments_zero`).
   - Second-order moment tensor isotropy (`4 I₃`) and exact quadratic consistency of the 12-neighbor discrete Laplacian (`discreteLaplacian_quadratic_exact`).
2. **`HCPPacking.lean`** (`Mathlib4 PR #46207`):
   - Exact primitive two-layer (`ABAB`) HCP unit-cell volume formula `√2 * a³` (`hcpUnitCellVolume_eq`).
   - Exact close-packing sphere fraction `π / (3 * √2)` (`hcp_packing_fraction`) and rigorous analytical enclosures `0.74 < η_HCP < 0.75` and `0.25 < 1 - η_HCP < 0.26` (`hcp_packing_fraction_bounds`, `hcp_void_fraction_bounds`).
3. **`EvolutionSchemeStability.lean`** (`Mathlib4 PR #46199`):
   - Invariance of the divergence-free subspace `ker div` under explicit evolution steps (`div_explicitStep_eq_zero`).
   - Energy dissipation under quadratic CFL bounds (`norm_sq_explicitStep_le`) and unconditional energy dissipation for semi-implicit Crank–Nicolson midpoint steps (`norm_sq_crankNicolson_le`).
   - Initial-state Lipschitz stability estimates (`norm_explicitStep_sub_le`).
4. **`SecondFiniteDifference.lean`** (`Mathlib4 PR #46205`):
   - Exact quadratic identities for backward and central second-order difference operators (`backwardSecondDiff_quadratic`, `centralSecondDiff_quadratic`).
   - Convergence of backward and central second-order finite differences to `f''` as `h → 0` (`tendsto_backwardSecondDiff`, `tendsto_centralSecondDiff`) via second-order Peano expansions.
5. **`RationalClearanceRegularizer.lean`** (`Mathlib4 PR #46209`):
   - Non-negativity, boundary vanishing at saturation, and strict antitone decay of rational internal-pressure potentials `κ * (Λ - ρ) / (ρ + 1)` on `[0, Λ]` (`rationalPressure_nonneg`, `rationalPressure_limit`, `rationalPressure_strictAnti`).
   - Uniform two-sided bounds `[0, L₀]`, balanced equilibrium, and critical overpressure collapse for clamped clearance regularizers (`clampedClearance_bounds`, `clampedClearance_balanced`, `clampedClearance_collapse`).

## Build & Verification

To build and verify all modules locally with Lake:

```bash
lake exe cache get
lake build
```

## Dual Licensing

Dual-licensed under **GNU Affero General Public License v3.0** (`LICENSE`) and **Apache License 2.0** (`LICENSE-APACHE`) for scientific reproducibility and Mathlib4 compatibility.
