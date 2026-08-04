# Procedural Guides

These guides are the step-by-step operating layer for the first AI Development
On-Ramp track. This page is the canonical detailed index for the developer
track. Use the matching page under [`../visuals/`](../visuals/) as the
mental-model companion.

## Choose by current need

Use this map to find the relevant topic when you arrive with a particular
concern. It is a discovery aid, not an alternative sequence: before acting,
identify the first unmet gate in the ordered phase table and resume there. No
row authorizes skipping prerequisite phases.

| Current concern | Read first | Required ordered path | Completion evidence |
|---|---|---|---|
| Local environment | [Phase 2: Windows 11 baseline](02-windows-11-baseline.md) | Complete the first unmet phase before Phase 4; continue through Phases 4-7 as the declared stack requires. | The relevant local tool or workspace gate passes. |
| GitHub identity and ownership | [Phase 3: GitHub foundation](03-github-foundation.md) | Phase 3, then Phase 4 for authenticated command-line use. | Identity, ownership, access, and Copilot prerequisites are verified. |
| Repository selection and setup | [Phase 3: GitHub foundation](03-github-foundation.md) | Phase 3 establishes ownership and the remote; Phase 4 attaches the local clone; Phase 5 verifies the workspace and captures the project. | The intended repository, remote, branch, and workspace are verified. |
| Connect and validate | [Phase 4: Git and GitHub CLI](04-git-and-github-cli.md) | Complete Phase 3 first if it is unmet; Phase 4 proves the local-to-remote round trip; continue through Phases 5-7 for the integrated workspace proof. | The required local-to-remote round trip and relevant integrated gate pass. |

Phase 0 and Phase 1 are the cross-cutting operating contract and terminology
orientation. Phases 8 and 9 establish the ongoing engineering loop and
capability plan after initial setup.

## Ordered phase sequence

| Phase | Guide | Primary gate |
|---|---|---|
| 0 | [Guiding LLM contract](00-guiding-llm-contract.md) | The LLM follows an evidence-driven, interactive, recorded progression. |
| 1 | [Mental model and lexicon](01-mental-model-and-lexicon.md) | Historical and current terminology are mapped without loss of meaning. |
| 2 | [Windows 11 baseline](02-windows-11-baseline.md) | PowerShell 7, Windows Terminal, and the development root are verified. |
| 3 | [GitHub foundation](03-github-foundation.md) | Identity, business ownership, repository, security, and Copilot access are verified. |
| 4 | [Git and GitHub CLI](04-git-and-github-cli.md) | A complete local-to-remote Git round trip is proven. |
| 5 | [VS Code and Copilot](05-vscode-and-copilot.md) | The known repository opens correctly and the real project is captured before implementation. |
| 6 | [Python 3.14 and uv](06-python-314-and-uv.md) | The repository has a reproducible uv-managed Python environment. |
| 7 | [First integrated workspace](07-first-integrated-workspace.md) | A bounded vertical slice runs through Polars, Parquet, DuckDB, and validation. |
| 8 | [Daily engineering loop](08-daily-engineering-loop.md) | Inspect, change, validate, commit, push, and state handoff are routine. |
| 9 | [Ramp plan](09-ramp-plan.md) | Capability gates lead to a useful business result rather than calendar completion. |

## Alternative paths

These are not part of the default numbered sequence. They document a
deliberate variant of one phase for developers who want it, without
disturbing the default path or its phase numbering.

| Phase variant | Guide | Default? | Status |
|---|---|---|---|
| 2 — Windows 11 baseline, WSL2 variant | [WSL2 development path](alt-wsl-development-path.md) | No — native Windows 11 (`02-windows-11-baseline.md`) is the default and first-recommended path | stub — not yet authored |

## Operating rule

The unit of progress is a verified state transition, not a command sent or a page read.
