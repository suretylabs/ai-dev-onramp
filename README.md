# AI Development On-Ramp

A repository-centered, AI-guided transition into GitHub, VS Code, modern Python, and evidence-driven engineering for experienced developers adopting a contemporary toolchain.

This is not a beginner programming course. It assumes the reader already understands software design, debugging, databases, production systems, and the discipline of building software. The gap addressed here is operational: Git, GitHub, VS Code, PowerShell 7, `gh`, uv, modern Python project isolation, quality tooling, and effective collaboration with an LLM inside a repository.

## Target environment

```text
Windows 11
  -> Windows Terminal + PowerShell 7
  -> Personal GitHub identity + business GitHub organization
  -> Organization-owned repository
  -> Git for Windows + GitHub CLI
  -> VS Code + GitHub Copilot
  -> uv-managed Python 3.14
  -> Polars + Parquet + DuckDB
  -> MSSQL and PDF integration when the project requires them
  -> Ruff + Pyright + pytest
```

The default path is native Windows 11. WSL is intentionally outside this on-ramp.

This is the first on-ramp track. See [`CONTRIBUTING.md`](CONTRIBUTING.md) for how additional tracks (other operating systems, languages, or data stacks) can be proposed.

## Start here

The material has four layers:

- [`guides/`](guides/) contains the procedural and instructional system.
- [`visuals/`](visuals/) contains the mental-model companion.
- [`templates/`](templates/) contains reusable state, decision, and instruction templates.
- [`reference/`](reference/) contains per-stack technical standards, starting with the Python/uv track.

For an AI-guided session, provide the LLM with:

1. [`guides/00-guiding-llm-contract.md`](guides/00-guiding-llm-contract.md)
2. this `README.md`
3. the guide for the current phase
4. [`templates/BOOTSTRAP_STATE.md`](templates/BOOTSTRAP_STATE.md) once work begins

The LLM should normally work interactively:

```text
Orient -> Clarify -> Inspect -> Explain -> Act -> Observe -> Evaluate -> Record -> Gate
```

The unit of progress is a **verified state transition**, not a command sent.

## Guide sequence

| Phase | Guide | Outcome |
|---|---|---|
| 0 | [Guiding LLM contract](guides/00-guiding-llm-contract.md) | Defines the teaching, command, evidence, question, and gating behavior. |
| 1 | [Mental model and lexicon](guides/01-mental-model-and-lexicon.md) | Maps established development terminology to current Git, GitHub, VS Code, and Python concepts. |
| 2 | [Windows 11 baseline](guides/02-windows-11-baseline.md) | Establishes PowerShell 7, Windows Terminal, WinGet awareness, and the development root. |
| 3 | [GitHub foundation](guides/03-github-foundation.md) | Establishes identity, organization ownership, Copilot access, repository conventions, and lightweight safeguards. |
| 4 | [Git and GitHub CLI](guides/04-git-and-github-cli.md) | Installs local Git and `gh`, clones the known remote, and proves the local/remote round trip. |
| 5 | [VS Code and Copilot](guides/05-vscode-and-copilot.md) | Integrates the editor and AI, then captures the real project before application code is generated. |
| 6 | [Python 3.14 and uv](guides/06-python-314-and-uv.md) | Creates a reproducible Python environment managed exclusively by uv. |
| 7 | [First integrated workspace](guides/07-first-integrated-workspace.md) | Proves Polars, Parquet, DuckDB, Ruff, Pyright, and pytest as one working system. |
| 8 | [Daily engineering loop](guides/08-daily-engineering-loop.md) | Establishes the normal inspect, plan, edit, validate, commit, push, and review cycle. |
| 9 | [Ramp plan](guides/09-ramp-plan.md) | Provides a capability-based path from setup to a useful business vertical slice. |

## Visual companion

Start with [the meta flow](visuals/00-meta-flow.md), then use the visual matching the current procedural phase.

These companion pages use editable Mermaid diagrams so they render natively in GitHub web and GitHub mobile without maintaining separate image assets.

The visual layer explains:

- GitHub identity, organization, and repository ownership;
- local versus remote state;
- working tree, staging, commit, and push;
- VS Code and Copilot positioning;
- Python, uv, `.venv`, and dependency state;
- Polars, Parquet, DuckDB, MSSQL, and PDF boundaries;
- technical gates, choice gates, and durable state.

## Governing principles

- Treat an experienced developer as an experienced developer.
- Translate historical terminology before correcting it.
- Ask reasonable questions when the answer changes the next decision.
- Generate commands at the point of need and evaluate their actual output.
- Use GitHub as a coordination plane, not merely remote backup.
- Capture the real project before generating architecture or application code.
- Keep durable context in repository documents rather than conversational memory.
- Prefer small, reversible changes and explicit validation.
- Never request credentials, recovery codes, private keys, production data, or secrets in chat.

## Templates

- [`BOOTSTRAP_STATE.md`](templates/BOOTSTRAP_STATE.md) — verified machine, account, repository, and project state
- [`DECISIONS.md`](templates/DECISIONS.md) — durable decisions and revisit conditions
- [`PROJECT_BRIEF.md`](templates/PROJECT_BRIEF.md) — business process, first useful slice, data boundaries, and acceptance criteria
- [`bootstrap-copilot-instructions.md`](templates/bootstrap-copilot-instructions.md) — minimal project-discovery behavior before implementation
- [`copilot-instructions.template.md`](templates/copilot-instructions.template.md) — project-specific operating contract after discovery

## Stack reference

Each on-ramp track keeps its own technical standard under `reference/`, separate
from this repository's own contributor conventions:

- [`PYTHON_STYLEGUIDE.md`](reference/PYTHON_STYLEGUIDE.md) — the Python coding
  standard for today's Python/uv track. This is on-ramp reference material,
  not a claim that this repository ships a Python codebase of its own.

Adding a track for a different language or runtime brings its own reference
document alongside this one; see [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Current-tooling rule

Installer interfaces, GitHub plans, Copilot controls, and tool behavior evolve. The guiding LLM must verify material current-state claims against official documentation and the actual UI rather than relying on remembered menu paths.

Primary references:

- GitHub documentation: <https://docs.github.com/>
- VS Code on Windows: <https://code.visualstudio.com/docs/setup/windows>
- PowerShell on Windows: <https://learn.microsoft.com/powershell/scripting/install/install-powershell-on-windows>
- uv documentation: <https://docs.astral.sh/uv/>

## Status

The procedural guides, reusable templates, visual companion, and Python reference layer are now authored. This repository remains an initial public release candidate. The intended validation path is:

```text
Repository review
    -> clean Windows 11 trial
    -> observed-friction revisions
    -> stable v1.0
```

## Contributing

Contributions are welcome — see [`CONTRIBUTING.md`](CONTRIBUTING.md) for
repository layout, content conventions, and how to propose a new tech-stack
track.

## License

MIT. See [`LICENSE`](LICENSE).
