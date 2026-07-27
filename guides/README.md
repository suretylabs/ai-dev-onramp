# Procedural Guides

These guides are the step-by-step operating layer for the first AI Development On-Ramp track. Use the matching page under [`../visuals/`](../visuals/) as the mental-model companion.

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
