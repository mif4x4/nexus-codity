# nexus-codity
Experimental protocol for verifying answers of RAG knowledge bases.

## Overview
`nexus-codity` describes a protocol that verifies answers produced by a RAG system: several material projections (text, vector, graph) are derived from a single source corpus, and an answer is scored by the number of projections that agree on it. Cross-checking projections detects discrepancies between transformations, but not errors of the source corpus itself; detecting those requires an external oracle not derived from the corpus. The protocol is experimental.

**Status:** Experimental proposal. Not a standard, not peer-reviewed; not intended for production use.

## Usage
Documentation, a small experimental core (`nexus_codity_core.py`), and demo results ([DEMO_REPORT.md](DEMO_REPORT.md)).

## Whitepaper
The conceptual foundation — **[WHITEPAPER.md](WHITEPAPER.md)** — defines *Codity*
(Кодичество), the material/declarative projection criterion (|P_M| ≥ 2) and the
**Shannon-Mirror Lemma**: cross-verification between derived projections cannot
detect common-mode errors of the source corpus; an external oracle is required.
Full philosophical framework: [`Codity.pdf`](Codity.pdf).

## Citation
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23681952.svg)](https://doi.org/10.5281/zenodo.23681952)

Cite as: **mif4x4** (2026). *nexus-codity: Codity & Shannon-Mirror Lemma*.
GitHub repository. See [CITATION.cff](CITATION.cff).

- Concept DOI (always latest): <https://doi.org/10.5281/zenodo.23681952>
- v1.0.0 (2026-10-27): <https://doi.org/10.5281/zenodo.23681953>

## License and scope

This repository (protocol description, whitepaper, experimental
snippets) is released under the [MIT License](LICENSE).

The production verification pipeline, projection builder, and
customer knowledge bases are proprietary and are not included
in this repository. The public artifacts demonstrate the
verification protocol and its stated limits (Shannon-Mirror);
they do not constitute the commercial implementation.

See also: [DEMO_REPORT.md](DEMO_REPORT.md) — aggregate demo results of the protocol.

## Author
[mif4x4](https://github.com/mif4x4)
