# OPG-57403 in Lean 4

Lean 4 formalization of **OPG-57403**: *"Every metamonovalued reloid is monovalued"*  
(https://www.unsolvedmath.com/problems/OPG-57403).

## Overview

This repository provides a self-contained Lean 4 (`v4.36.0`) formalization using only Lean's `Init` library (zero Mathlib dependencies).

- [`UnsolvedMath/OPG57403.lean`](UnsolvedMath/OPG57403.lean) — Defines reloids (`Reloid A B` as filters on `A × B`), the filter order (`≤`), `⊥`, `⊤`, `principal`, binary meets (`⊓`), arbitrary meets (`sInf`), relational composition (`comp`) and converse (`inv`), monovaluedness (`Monovalued`), metamonovaluedness (`Metamonovalued`), weak metamonovaluedness (`WeaklyMetamonovalued`), and proper weak metamonovaluedness (`ProperWeaklyMetamonovalued`).
- [`UnsolvedMath.lean`](UnsolvedMath.lean) — Root module importing `UnsolvedMath.OPG57403` and checking `#print axioms` for the main theorems.

## Main Theorems

In namespace `UnsolvedMath.OPG57403`:

- `metamonovalued_is_monovalued` — Every metamonovalued reloid is monovalued (OPG-57403).
- `weakly_metamonovalued_is_monovalued` — Every weakly metamonovalued reloid (preserving binary meets under right composition) is monovalued.
- `proper_weakly_metamonovalued_is_monovalued` — Even restricting binary meet preservation to proper (`≠ ⊥`) reloids implies monovaluedness.
- `monovalued_iff_metamonovalued` — Full characterization: `Monovalued f ↔ Metamonovalued f` (combining Porton's converse `monovalued_is_metamonovalued` with `metamonovalued_is_monovalued`).
- `monovalued_iff_comp_inv_le_diag` — Equivalence of `Monovalued f` with `comp f (inv f) ≤ principal (diag B)`.

## Build & Verification

Requires Lean `v4.36.0` (configured via [`lean-toolchain`](lean-toolchain)).

```sh
lake build
```

Running `lake build` compiles `UnsolvedMath.OPG57403` and `UnsolvedMath`, verifying all proofs with zero `sorry` and printing the axiom dependencies of the main theorems (`[propext, Classical.choice, Quot.sound]`).
