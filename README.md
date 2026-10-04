<div align="center">

<img src="aien-butterfly.webp" alt="AIEN butterfly mark" width="180" />

# AIEN

**A sovereign computing stack, built in the open: its own operating system, its own compiler and reaction runtime, its own machine realization layer.**

[aienos.com](https://www.aienos.com) · [drakestapleton.com](https://www.drakestapleton.com) · [aien@aienos.com](mailto:aien@aienos.com)

[![License: AGPL-3.0-or-later](https://img.shields.io/badge/License-AGPL--3.0--or--later-blue.svg)](LICENSE)

</div>

---

## What this is

AIEN is an attempt to build a persistent, local computing system from the first instruction upward, on an NVIDIA DGX Spark (Grace Blackwell GB10), with no outside organization required to boot, build, trust or recover it. The founding principle: closest to the metal, fastest wins. Mojo is a default, not dogma. Beat it if you can. Build what is missing.

Built by [Drake Stapleton](https://www.drakestapleton.com) with AI collaborators. Contributions and hard questions are welcome.

## Status at a glance (2026-10-04)

This is research-grade, pre-alpha software. Nothing here is qualified on real hardware as a finished system. Every line below links to the record it comes from; if the record and this page disagree, the record wins.

**Works today, with receipts**

- Omega reaction runtime: the R1 to R16 qualification ladder passed on the GB10 ([execution plan, 2026-09-29 addendum](https://github.com/aien-dev/aien-architecture/blob/main/CURRENT_EXECUTION_PLAN.md)); M19 resident foundation requalified ([omega evidence](https://github.com/aien-dev/omega/tree/main/evidence)).
- AIENOS C kernel: passes 9 of 14 emulator gates in QEMU; the rest report NOT_RUN, never PASS ([aienos README](https://github.com/aien-dev/aienos#current-state), [gate list](https://github.com/aien-dev/aienos/blob/main/native/kernel/GATES.md)).
- Legacy Rust runtime (aien-sovereign-core): builds, lints and tests green in CI on Linux using the documented CPU fallback ([CI](https://github.com/aien-dev/aien-sovereign-core/actions)); policy decides before any tool runs, with tests showing denied, contained, pending and stale requests never reach the tool ([authority tests](https://github.com/aien-dev/aien-sovereign-core/blob/main/crates/aien-mcp/tests/authority.rs)).

**Experimental (host only, not in a qualified build)**

- Capability Graph, Skill Router, J-Space branch store, machine identity and a loopback Fabric slice exist in omega and run on the host ([implementation status](https://github.com/aien-dev/aien-architecture/blob/main/docs/02-implementation-status.md)).
- Omega Systems Core compiler: OSC-1 and OSC-2 implemented with host receipts, OSC-3 in progress; there is no general Omega compiler and it is not self-hosting ([omega README](https://github.com/aien-dev/omega#current-state)).
- FORGE machine realization: the substrate-neutral descriptor contract (AR1) passed its gates ([physics](https://github.com/aien-dev/physics)).

**Blocked or not done**

- The C kernel has never booted on the real machine; real boot needs the operator present and a recovery stick.
- Trust chain and encrypted storage (TRUST-1, M5) are NOT_QUALIFIED ([gate matrix](https://github.com/aien-dev/aienos/blob/main/docs/TRUST-1-M5-GATE-MATRIX.md)).
- GPU qualification of the legacy Rust runtime is not established; its CI proves software health only.
- All performance figures published before 23 September 2026 are withdrawn until regenerated with a reproducible command and an evidence bundle ([benchmarks](https://github.com/aien-dev/benchmarks)).

Status words used everywhere: PASS, FAIL, NOT_RUN, BLOCKED_HARDWARE, BLOCKED_OPERATOR, MISSING_IMPLEMENTATION. A passing emulator run is never described as hardware qualification. Authority for what is done and what is not:

- [Plan authority](https://github.com/aien-dev/aien-architecture/blob/main/PLAN_AUTHORITY.md): which document wins
- [Current execution plan](https://github.com/aien-dev/aien-architecture/blob/main/CURRENT_EXECUTION_PLAN.md): what is being done now, with receipts
- [Milestone registry](https://github.com/aien-dev/aien-architecture/blob/main/doctrine/ROADMAP.md): milestone status

## The repositories

| Repository | What it is |
| :--- | :--- |
| [aien-architecture](https://github.com/aien-dev/aien-architecture) | The authority for whole-system design, milestone status and sequencing. Start here. |
| [aienos](https://github.com/aien-dev/aienos) | AIENOS: our own kernel and operating system, replacing Linux on the DGX Spark. Contributors wanted. |
| [omega](https://github.com/aien-dev/omega) | The reaction runtime and compiler (Omega Systems Core). The current implementation is C. |
| [physics](https://github.com/aien-dev/physics) | Machine realization (FORGE) and the historical Atlas/PHYSICS boot artifacts. |
| [aien-protocols](https://github.com/aien-dev/aien-protocols) | Versioned specifications and reference crates for agent state, inference and evaluation. |
| [aien-sovereign-core](https://github.com/aien-dev/aien-sovereign-core) | The earlier Linux-hosted Rust runtime. Legacy, kept as scaffolding while the repositories above replace it ([ADR 0024](https://github.com/aien-dev/aien-architecture/blob/main/docs/adr/0024-rust-scaffolding-omega-destination.md)). |
| [interplane](https://github.com/aien-dev/interplane) | INTERPLANE: an open protocol between AI models and agent runtimes. Models express intent, runtimes keep authority. |
| [benchmarks](https://github.com/aien-dev/benchmarks) | Measurement harnesses and evidence bundles. |
| [aienos.com](https://github.com/aien-dev/aienos.com) · [drakestapleton.com](https://github.com/aien-dev/drakestapleton.com) | Project site and personal project record. |

Other repositories (aegis-runtime, open-humanity, spark-rsi, atlas, aien-edge and similar) are experimental or research and carry no status claims. Earlier standalone repositories are archived.

## Standing rules

- Language rule: Rust is scaffolding, Omega is the destination, and C or assembly only where hardware, boot, or a measurement justifies it. Nothing already merged is reverted ([ADR 0024](https://github.com/aien-dev/aien-architecture/blob/main/docs/adr/0024-rust-scaffolding-omega-destination.md)).
- No Python anywhere, including helper scripts.
- No CUDA toolkit and no dependence on vendor CUDA libraries. The GB10 is driven by our own native path.
- No systemd in AIENOS boot, init, services or tooling.
- Builds are offline and in-house for the trusted base. No outside dependency may be required to build, boot or recover it.
- Outside inference stacks (Modular MAX, llama.cpp, vLLM) are yardsticks only, kept in [aien-yardsticks](https://github.com/aien-dev/aien-yardsticks); nothing from them ships in AIEN.
- Every performance figure must resolve to a reproducible command and a content-addressed evidence bundle. Old figures without one are withdrawn.
- Changes land through pull requests with the commands run and their output. Main branches on the core repositories are protected; no automatic merging.

## How to help

Start with [AIENOS issues labelled `good first issue` or `emulator-ok`](https://github.com/aien-dev/aienos/issues). Those need no special hardware. Read each repository's CONTRIBUTING or AGENTS file first.

## License and values

Code across the AIEN repositories is licensed under the GNU Affero General Public License v3.0 or later (AGPL-3.0-or-later); see each repository's LICENSE. aien-protocols also uses the Community Specification License 1.0 for its specifications. Project values live in the nonbinding [COVENANT.md](COVENANT.md): keep foundational advances open. The covenant grants and restricts no legal rights; LICENSE governs. Governance text for agents working in these repositories: [CONSTITUTION.md](CONSTITUTION.md) and [AGENT_CODE_OF_CONDUCT.md](AGENT_CODE_OF_CONDUCT.md).

## Copyright

Copyright (c) 2026 Drake Stapleton <aien@aienos.com> and AIEN Contributors. Authored by Drake Stapleton in collaboration with AIEN.
