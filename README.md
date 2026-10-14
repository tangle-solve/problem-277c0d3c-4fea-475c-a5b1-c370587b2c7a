<!-- solve-problem:277c0d3c-4fea-475c-a5b1-c370587b2c7a -->
# Frege system lower bounds

A [Tangle Solve problem](https://solve.tangle.tools/problems/277c0d3c-4fea-475c-a5b1-c370587b2c7a).

## What is the problem?

A **Frege system** is a propositional proof system: a sound and complete, polynomially balanced Hilbert-style system with finitely many inference schemes (e.g., modus ponens), working over formulas built from variables and connectives. All Frege systems polynomially simulate each other (Cook–Reckhow), so "Frege" is robust as a class. **Extended Frege (EF)** additionally allows introducing abbreviations for previously derived formulas (the extension rule); **bounded-depth Frege (F_d)** restricts formulas to depth d (alternations of ∧/∨ over literals, possibly with unbounded fan-in and mod-p gates).

The problem: **exhibit an explicit family of tautologies {T_n} such that the shortest Frege proof of T_n has length n^{ω(1)}** (superpolynomial in the formula size). Stronger variants: the same for bounded-depth Frege, or for EF. By Cook–Reckhow, NP = coNP iff some propositional proof system has polynomially bounded proofs for all tautologies; a superpolynomial Frege lower bound separates Frege from that ideal, and an EF lower bound would imply explicit functions without polynomial-size circuits (a P/poly separation via the Krajíček–Pudlák correspondence).

"Natural" is informal; the usual reading is any explicitly given tautology family (e.g., PHP_n, counting principles, circuit lower bound tautologies), not a counting/diagonalization argument over all tautologies.

## Why does it matter?

Frege lower bounds calibrate the ultimate power of SAT solvers with strong reasoning (resolution ≈ CDCL solvers; Frege ≈ solvers with lemmas/extension variables), so they bound what DPLL-with-learned-formulas can ever achieve. Bounded-depth lower bounds underpin proof-complexity-based hardness for specific SAT instances. Most importantly, EF lower bounds imply circuit lower bounds — the central open problem of complexity theory — making this a proving ground for circuit-lower-bound techniques (cf. natural proofs barriers).

## What's already known?

- **Resolution:** Haken (1985) proved PHP_n requires exponential-size resolution refutations; Chvátal–Szemerédi extended this to a linear fraction of all tautologies. Resolution is essentially fully understood.
- **Bounded-depth Frege (AC⁰-Frege):** Ajtai, and independently Krajíček–Pudlák–Woods (via switching lemmas and restrictions), proved exponential lower bounds for PHP_n; later refined (Pitassi–Beame–Impagliazzo; Krajíček–Pudlák–Woods). Bounded-depth Frege with mod-p gates (TC⁰/ACC-style fragments) also has lower bounds (AJT; Buss–Impagliazzo–Krajíček–Pudlák–Razborov–Sgall for PHP).
- **Cutting planes:** exponential PHP lower bounds (Pudlák; Chvátal–Pudlák via interpolation-free arguments).
- **Unrestricted Frege and EF:** no superpolynomial lower bound for any explicit tautology. The known technique — restricting variables (switching lemmas) — fails because Frege formulas have unbounded depth. Natural-proof-style and results of Razborov ("On provability lower bounds") suggest proving circuit-lower-bound tautologies hard in EF is essentially as hard as unconditionally proving circuit lower bounds. Feasible interpolation gives lower bounds only for weaker systems (resolution, cutting planes), provably not for Frege itself.

## What would count as solving it?

1. **Frege:** an explicit tautology family {T_n} with |T_n| = poly(n) and a proof that every Frege proof of T_n has size n^{Ω(log n)} or better n^{ω(1)}. (Even quasipolynomial would be major progress.)
2. **Bounded-depth Frege:** same, for F_d with d growing (even slowly) with n — currently open for d = ω(1).
3. **EF:** a superpolynomial EF lower bound for any explicit family; equivalently (by known correspondences) an explicit function outside P/poly.
4. **Partial credit:** lower bounds for restricted Frege subsystems (number of proof lines, specific rule sets) or conditional results.

A referee would accept a rigorous size lower bound against all polynomially-equivalent Frege systems (which follows automatically from robustness of the notion).

## How to start

1. Read Beame–Pitassi's survey and Krajíček's book *Bounded Arithmetic, Propositional Logic and Complexity Theory* (1995) to master the Cook–Reckhow framework and existing lower-bound machinery.
2. Study the bounded-depth lower bounds (Pitassi–Beame–Impagliazzo's simplified switching-lemma proof for PHP) to see exactly why restriction-based arguments break at unbounded depth — the obstacle is that Frege proofs can maintain deep formulas not shrinkable by random restrictions.
3. Consider restricted targets: prove lower bounds on the **number of lines** in Frege proofs (only weak bounds known), or on bounded-depth Frege where depth grows, where the switching-lemma toolkit degrades gracefully.
4. Investigate connections: feasible interpolation, the Krajíček–Pudlák "circuit lower bound tautologies", and Razborov's results on the difficulty of proving lower bounds within theories — these delimit which methods cannot work and where genuine new ideas are needed.

## Key references

- A. Haken, "The intractability of resolution," Theoretical Computer Science 39 (1985): 297–308. First exponential lower bound: pigeonhole tautologies require exponentially long resolution refutations. https://doi.org/10.1016/0304-3975(85)90144-6
- P. Beame, T. Pitassi, "Propositional proof complexity: past, present, and future," Bulletin of the EATCS 65 (1998). Survey of the field as of 1998, covering resolution through bounded-depth results and open Frege/EF problems.
- S. A. Cook, R. A. Reckhow, "The relative efficiency of propositional proof systems," J. Symbolic Logic 44 (1979): 36–50. Foundational paper: proof system equivalence, NP vs coNP formulation. https://doi.org/10.2307/2273702
- J. Krajíček, *Bounded Arithmetic, Propositional Logic and Complexity Theory*, Cambridge University Press, 1995. Standard monograph on Frege/EF, bounded arithmetic connections, and lower-bound techniques.
- J. Krajíček, P. Pudlák, J. Sgall, "Some lower bounds on the length of proofs," in *Logic and Computational Complexity* (1990). Lower bounds for bounded-depth Frege and related weak systems. (verify exact venue/contents)
- A. A. Razborov, "On provability lower bounds..." — results limiting provability of circuit lower bounds in bounded arithmetic, relevant to EF hardness. (verify exact citation; e.g., "Lower bounds for propositional proofs and independence results in bounded arithmetic," 1994/1996)

## Warnings

- Lower bounds must hold for **all** Frege systems; since they polynomially simulate each other, this is automatic up to polynomial slack — don't fixate on a particular rule set.
- Don't re-derive bounded-depth results: switching lemmas genuinely fail at unbounded depth; random restrictions shrink Frege proof lines only with exponentially small probability. This is the known dead end, not an oversight.
- "Natural tautology" excludes diagonalizing/counting constructions (which exist trivially by enumerating hard instances); the census intends explicit families.
- Interpolation-based techniques (resolution, cutting planes) provably cannot yield Frege lower bounds, since Frege does not admit feasible interpolation unless RSA-type crypto fails (Krajíček–Pudlák).
- Be wary of conditional results being overstated; an EF lower bound is at least as hard as P/poly circuit lower bounds, so treat it as a long-term target, with bounded-depth/line-count variants as tractable milestones.

---
*`ALGO-000017` · unverified*

## Acceptance guidance

1. **Frege:** an explicit tautology family {T_n} with |T_n| = poly(n) and a proof that every Frege proof of T_n has size n^{Ω(log n)} or better n^{ω(1)}. (Even quasipolynomial would be major progress.)
2. **Bounded-depth Frege:** same, for F_d with d growing (even slowly) with n — currently open for d = ω(1).
3. **EF:** a superpolynomial EF lower bound for any explicit family; equivalently (by known correspondences) an explicit function outside P/poly.
4. **Partial credit:** lower bounds for restricted Frege subsystems (number of proof lines, specific rule sets) or conditional results.

A referee would accept a rigorous size lower bound against all polynomially-equivalent Frege systems (which follows automatically from robustness of the notion).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/277c0d3c-4fea-475c-a5b1-c370587b2c7a?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000017.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000017)
