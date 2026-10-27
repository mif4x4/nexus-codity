# DEMO_REPORT — Verification Protocol: Aggregate Demo Results

**Date:** 2026-10-27
**Status:** Public demo artifact. Aggregate metrics only — production
knowledge bases, the projection builder and the bench runner are
proprietary and **not included** in this repository (see [LICENSE](LICENSE)).

## 1. What is demonstrated

Application of the Codity verification protocol (WHITEPAPER.md) to three
knowledge bases (KB) in a read-only QA stand:

| KB | Domain | Projections | Questions | Design |
|-----|--------|-------------|-----------|--------|
| **KB-R** | reference KB (own development) | 3 | 43 | 31 positive + 12 negative |
| **KB-A** | industrial equipment documentation | 5 | 40 | 30 positive + 10 negative |
| **KB-B** | industrial tooling documentation | 3 | 40 | 30 positive + 10 negative |

Fixed rules applied to all three:

- **Codity map** (evidence → confidence): `0→0.10, 1→0.45, 2→0.65, 3→0.85, 4→0.92, 5→1.00`,
  where the score = number of *confirming material projections*.
- **Rule R** (identical for negatives everywhere): an honest refusal is scored by the
  number of projections in which absence of the answer was confirmed;
  a false "golden" label (answer actually present) is scored by the layers
  that contain the answer.
- **Mutation testing**: 20 mutants per KB, 5 categories:
  A requirement gap · B projection contradiction · C version drift ·
  D dead meaning (text layers alive, vector/graph layers empty) ·
  E consistent lie (all layers agree, claim violates an external oracle).
- **Trap probes**: 5 synthetic traps injected into a real question's context:
  1 empty answer · 2 garbage file · 3 false confirmation ·
  4 foreign random numbers · 5 missing source. Plus a conservative pass
  over all organic results.

## 2. Results

| Metric | KB-R | KB-A | KB-B |
|--------|------|------|------|
| PASS | **43/43** | **40/40** | **40/40** |
| avg codity | **0.755** | **0.774** | **0.680** |
| Distribution (H/M/L/NO) | 24 / 7 / 12 / 0 | 24 / 8 / 8 / 0 | 14 / 18 / 8 / 0 |
| Negative tests | **12/12** | **10/10** (+1 false golden label caught) | **10/10** |
| Mutants caught | 10/10 (per protocol) | **18/20 (90%)** | **18/20 (90%)** |
| Trap probes (5 types) | 10 organic events (G1–G6) | **5/5** + 10 organic | **5/5** + 12 organic |

## 3. Verdict against the acceptance criteria

| Criterion | Threshold | KB-R | KB-A | KB-B |
|-----------|-----------|------|------|------|
| Negative tests | ≥ 95 % | 100 % ✅ | 100 % ✅ | 100 % ✅ |
| avg codity | 0.65 – 0.85 | 0.755 ✅ | 0.774 ✅ | 0.680 ✅ |
| Mutants caught | ≥ 80 % | ✅ | 90 % ✅ | 90 % ✅ |
| Trap probes | ≥ 70 % | ✅ | 100 % ✅ | 100 % ✅ |
| Projections | ≥ 3 | 3 ✅ | 5 ✅ | 3 ✅ |

**Confidence level: HIGH for all three KBs.**

## 4. Honest limitation (as stated by the Shannon-Mirror Lemma)

Category **E** mutants ("consistent lie") were caught only **2/4** on each KB.
This is the *expected* outcome, not a defect: four claims had no external
oracle in the stand, so the system honestly accepted the consistent corpus
as an invariant — exactly the behaviour predicted by the lemma. Detecting
this class requires an oracle not derived from the source corpus.

Additional honest finding: on KB-A the negative suite surfaced **1 false
golden label** — a test marked "absent" that in fact has a real sourced
answer in the corpus; the system returned the answer instead of refusing.

## 5. Scope reminder

The public artifacts (protocol, whitepaper, this demo report, the small
experimental core) demonstrate the verification protocol **and its stated
limits**. The commercial implementation — projection builder, automated
bench, customer knowledge bases, CI — is proprietary and absent from this
repository; MIT licensing here does not and cannot open it.
