# OPG-57403 in Lean 4

Lean 4 formalization of **OPG-57403**: *"Every metamonovalued reloid is monovalued"*  
(https://www.unsolvedmath.com/problems/OPG-57403).

## Overview

This repository provides a self-contained Lean 4 (`v4.36.0`) formalization using only Lean's `Init` library (zero Mathlib dependencies), alongside a compressed LaTeX proof:

- [`UnsolvedMath/OPG57403.lean`](UnsolvedMath/OPG57403.lean) — Defines reloids (`Reloid A B` as filters on `A × B`), the filter order (`≤`), `⊥`, `⊤`, `principal`, binary meets (`⊓`), arbitrary meets (`sInf`), scoped notation (`Reloid.Notation`), relational composition (`comp`) and converse (`inv`), monovaluedness (`Monovalued`, constructive `MonovaluedDN`), and metamonovaluedness variants (`Metamonovalued`, `UnrestrictedMetamonovalued`, `WeaklyMetamonovalued`, `ProperWeaklyMetamonovalued`, `ProperMeetWeaklyMetamonovalued`, `PrincipalEndoWeaklyMetamonovalued`).
- [`UnsolvedMath.lean`](UnsolvedMath.lean) — Root module importing `UnsolvedMath.OPG57403` and checking `#print axioms` on the main theorems.
- [`OPG57403.tex`](OPG57403.tex) / [`OPG57403.pdf`](OPG57403.pdf) — Compressed LaTeX proof of OPG-57403 and compiled PDF matching the formalization.

## Main Theorems

In namespace `UnsolvedMath.OPG57403` (universe-polymorphic over codomain universe `max v w`, including `v` at `w = 0`):

- `metamonovalued_is_monovalued` — Every metamonovalued reloid is monovalued (OPG-57403).
- `weakly_metamonovalued_is_monovalued` — Every weakly metamonovalued reloid (preserving binary meets under right composition) is monovalued.
- `proper_weakly_metamonovalued_is_monovalued` — Restricting binary meet preservation to proper (`≠ ⊥`) operands still implies monovaluedness.
- `proper_meet_weakly_metamonovalued_is_monovalued` — Restricting binary meet preservation to pairs with proper meet (`g ⊓ h ≠ ⊥`) still implies monovaluedness.
- `principal_endo_weakly_metamonovalued_is_monovalued` — Sharpest binary-meet hypothesis: preserving binary meets of principal endoreloids on `B × B` already implies monovaluedness.
- `unrestricted_metamonovalued_is_monovalued` — OPG-57403 under the unrestricted (possibly empty `G`) reading of metamonovaluedness.
- `exists_proper_monovalued_not_unrestricted_metamonovalued` — Necessity of nonemptiness of `G` in Porton's converse: a proper, non-entire monovalued reloid fails `UnrestrictedMetamonovalued` at `G = ∅`.
- `monovalued_iff_metamonovalued` (and corresponding `iff` characterizations for `WeaklyMetamonovalued`, `ProperWeaklyMetamonovalued`, `ProperMeetWeaklyMetamonovalued`, and `PrincipalEndoWeaklyMetamonovalued`) — Full characterizations combining Porton's converse `monovalued_is_metamonovalued` with the theorems above.
- `monovalued_iff_comp_inv_le_diag` — Constructive equivalence of `Monovalued f` with `comp f (inv f) ≤ principal (diag B)`.

## Build & Verification

Requires Lean `v4.36.0` (configured via [`lean-toolchain`](lean-toolchain)).

```sh
lake build
```

Running `lake build` compiles `UnsolvedMath.OPG57403` and `UnsolvedMath`, verifying all proofs with zero `sorry` and printing the axiom dependencies of the main theorems (`[propext, Classical.choice, Quot.sound]`, and `[propext, Quot.sound]` for `exists_proper_monovalued_not_unrestricted_metamonovalued`).
