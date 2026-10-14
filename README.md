<!-- solve-problem:bc5d99b5-550a-4110-bbcc-b36c62c2cb72 -->
# Circuit lower bounds for NEXP

A [Tangle Solve problem](https://solve.tangle.tools/problems/bc5d99b5-550a-4110-bbcc-b36c62c2cb72).

## What is the problem?

Prove that NEXP (nondeterministic exponential time, ⋃_c NTIME[2^{n^c}]) is not contained in P/poly, the class of languages decidable by polynomial-size Boolean circuit families {C_n} with one circuit per input length, no uniformity requirement. Equivalently: exhibit a language L ∈ NEXP such that every circuit family computing L has size n^{ω(1)}.

**Formal setting.** Non-uniform Boolean circuits over the standard basis {AND, OR, NOT} (or any complete basis). "Size" = number of gates. P/poly ⊇ all of P and much more, since the circuit for length n can be arbitrary. The stronger target MA_EXP ⊄ P/poly (MA with exponential-time verifier and oracle) is also open in the fully non-uniform setting; note Buhrman–Fortnow–Thierauf showed MA_EXP ⊆ P/poly *relative to some oracle*, so relativizing techniques cannot work.

**Assumptions/constraints.** Any proof technique must evade the natural proofs barrier of Razborov–Rudich: no "natural" property of Boolean functions (constructible, useful against P/poly) can exist unless pseudorandom generators of subexponential hardness fail to exist. Standard diagonalization also fails because P/poly contains undecidable languages (non-uniformity defeats counting arguments).

## Why does it matter?

This is the front line of circuit lower bounds: it would be the first superpolynomial lower bound for any "natural" uniform class against unrestricted circuits, going far beyond Williams's NEXP ⊄ ACC0. It is a prerequisite step on essentially every proposed route toward P vs NP, and by Karp–Lipton-style results, such lower bounds yield derandomization consequences (e.g., would imply deterministic algorithms for certain randomized classes). Techniques developed to crack it would likely transfer to lower bounds for smaller classes like NP, where the same barriers apply.

## What's already known?

- **Williams (2010/2014):** NEXP ⊄ ACC0 via the "algorithmic method": a mildly faster-than-brute-force Circuit Analysis Algorithm (CACM) for ACC0-SAT (2^n/n^c) implies the lower bound for NEXP. This is the only known superpolynomial lower bound for a natural uniform class against a nontrivial circuit class.
- **Older:** Kannan: Σ_2^EXP ∩ Π_2^EXP ⊄ P/poly (and in fact for every k, Σ_k^p-level hierarchies yield some lower bounds at exponential levels). MA ⊄ P/poly is unknown to fail but is believed; EXP ⊄ P/poly is open! Actually: by counting, almost all languages need exponential circuits, but no explicit EXP (or even E) language is known to require superlinear size — even against honest-to-goodness unrestricted circuits, the best explicit lower bound is (3−ε)n for affine functions (Blum, 1984).
- **Barriers:** natural proofs (Razborov–Rudich 1997), relativization (Baker–Gill–Solovay; Buhrman–Fortnow–Thierauf for MA_EXP), algebrization (Aaronson–Wigderson).
- The ACC0 result does not extend to TC0, P/poly, etc., because no nontrivial SAT algorithm is known for those classes.

## What would count as solving it?

- **Primary:** A proof that NEXP ⊄ P/poly, i.e., a language in NTIME[2^{poly(n)}] requiring superpolynomial circuit size. A referee accepts any rigorous proof, by any technique.
- **Milestone variants:** (a) Williams-style: a deterministic algorithm deciding satisfiability of n-input P/poly circuits of size n^k in time 2^n / n^{ω(1)} (this suffices by Williams's theorem, extended from ACC0 to P/poly). (b) MA_EXP ⊄ P/poly. (c) Even EXP ⊄ P/poly or E ⊄ SIZE(2^{εn}) for explicit E-functions would be major partial progress. (d) A new barrier showing why it's impossible would also be a resolution of a different kind.

## How to start

1. **Read Williams's JACM paper (arXiv:0907.4753)**, especially the "easy witness lemma" framework: NEXP ⊆ P/poly ⇒ all NEXP witnesses have small circuits ⇒ a fast circuit-SAT algorithm contradicts this via diagonalization. The natural first attempt: find any nontrivial (#SAT or SAT) algorithm for a circuit class strictly larger than ACC0.
2. **Read Ryan Williams's survey arXiv:1502.07816** and his "New Techniques and Hardness for ACC0"-adjacent expositions for the roadmap of barriers.
3. **Study the natural proofs barrier** (Razborov–Rudich 1997) to understand exactly which proof shapes are ruled out — any solution must be "unnatural" (e.g., not computable in 2^{2^{O(n)}}, or not useful in the required sense).
4. **Main obstacle:** no one knows any nontrivial algorithm for general circuit-SAT beyond the 2^n(1−1/poly) barrier-era results ( Williams–Santhanam–Hirahara acc-with-threshold attempts), and diagonalization fails against non-uniform classes. Consider circuit-analysis algorithms for restricted gate sets, or interactive/PCP-flavored characterizations of NEXP to design a language with checkable hardness.

## Key references

- R. Williams, "Nonuniform ACC Circuit Lower Bounds", JACM 61(1), 2014 (arXiv:0907.4753). Proves NEXP ⊄ ACC0 via the algorithmic method: slightly-nontrivial ACC-SAT algorithms imply circuit lower bounds.
- R. Williams, "Some Estimated Likelihoods for Computational Complexity", 2015 (arXiv:1502.07816) (verify). A survey/essay on plausible outcomes and proof strategies for open lower-bound questions including NEXP vs P/poly.
- A. Razborov, S. Rudich, "Natural Proofs", JCSS 55(1), 1997. Defines and proves the barrier: any natural combinatorial property useful against P/poly would break standard pseudorandom generators.
- H. Buhrman, L. Fortnow, T. Thierauf, "Nonrelativizing separations", CCC 1998. Shows MA_EXP ⊆ P/poly relative to an oracle, ruling out relativizing proofs.
- S. Buss, R. Williams, "Limits on alternation trading proofs for time-space lower bounds", Comput. Complexity 2016 (verify). Maps what standard techniques can and cannot achieve for related lower bounds.
- R. Kannan, "Circuit-size lower bounds and non-reducibility to sparse sets", Inf. Control 1982. Proves Σ_2^EXP ∩ Π_2^EXP ⊄ P/poly.

## Warnings

- **The natural proofs barrier applies to this very target**: any proof must fail "naturality" — typically by being non-constructive at scale or by exploiting the specific structure of NEXP. Do not attempt a generic "property of hard functions" argument.
- **Diagonalization alone is dead**: P/poly contains uncountably many languages; only the Williams-style combination of an algorithm plus a collapse assumption works so far.
- **Don't over-claim ACC0 results**: NEXP ⊄ ACC0 does not generalize by tweaking parameters; the blocker is genuinely the absence of faster circuit-SAT for richer classes.
- **Check census citations yourself** — the arXiv:1502.07816 attribution and title are flagged "(verify)" in the source.

---
*`ALGO-000005` · flagged for review*

## Acceptance guidance

- **Primary:** A proof that NEXP ⊄ P/poly, i.e., a language in NTIME[2^{poly(n)}] requiring superpolynomial circuit size. A referee accepts any rigorous proof, by any technique.
- **Milestone variants:** (a) Williams-style: a deterministic algorithm deciding satisfiability of n-input P/poly circuits of size n^k in time 2^n / n^{ω(1)} (this suffices by Williams's theorem, extended from ACC0 to P/poly). (b) MA_EXP ⊄ P/poly. (c) Even EXP ⊄ P/poly or E ⊄ SIZE(2^{εn}) for explicit E-functions would be major partial progress. (d) A new barrier showing why it's impossible would also be a resolution of a different kind.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/bc5d99b5-550a-4110-bbcc-b36c62c2cb72?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000005.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000005)
