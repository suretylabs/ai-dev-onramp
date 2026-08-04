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

The default path is native Windows 11, chosen to avoid the cross-filesystem I/O performance penalty of editing and running project files across the Windows/Linux boundary. That default accepts a few trade-offs in return: `\` vs. `/` path-separator friction, CRLF vs. LF line endings (handled explicitly in [`guides/04-git-and-github-cli.md`](guides/04-git-and-github-cli.md#line-ending-conversion)), and the occasional Windows-native-wheel gap for a compiled Python package (checked in [`guides/06-python-314-and-uv.md`](guides/06-python-314-and-uv.md#verify-windows-wheel-availability)).

WSL2 is a real, legitimate alternative for developers ready to level up their environment with a Linux-side toolchain — see [`guides/alt-wsl-development-path.md`](guides/alt-wsl-development-path.md). It is not the first or recommended path for this track, both because native Windows keeps the on-ramp usable for everyone from day one and because WSL2 is not universally available (corporate policy, virtualization settings, or missing administrator rights can block it) or already familiar to a Windows-only developer. It is currently a stub awaiting content.

This is the first on-ramp track. See [`CONTRIBUTING.md`](CONTRIBUTING.md) for how additional tracks (other operating systems, languages, or data stacks) can be proposed.

## Start here

The material has four layers:

- [`guides/`](guides/) contains the procedural and instructional system.
- [`visuals/`](visuals/) contains the mental-model companion.
- [`templates/`](templates/) contains reusable state, decision, and instruction templates.
- [`reference/`](reference/README.md) contains per-stack technical standards, starting with the Python/uv track.

## Lanes (related on-ramps)

A **lane** is a sibling on-ramp with a different audience and output. It reuses
this repository's guided-elicitation and durable-artifact pattern, but it is
**not** a phase in the developer guide sequence below and is **not** a
stack **track** (tracks vary OS/language/data stack for the same developer
purpose — see [`CONTRIBUTING.md`](CONTRIBUTING.md)).

| Lane | Audience | Output | Runtime entrypoint |
|---|---|---|---|
| [Consultant Process-Capture](consultant-lane/README.md) | Consultant, trainer, or manager working with a veteran operator | A signed `PROCESS_CAPTURE.md` a new hire can attach to an LLM session as read-only procedure context for one business process | [`consultant-lane/CONTEXT_LAYER.md`](consultant-lane/CONTEXT_LAYER.md) |

The developer track in this README remains the default path for setting up an
AI development environment.

## Operating modes

This repository has three distinct modes:

- **Read-only developer context mode** uses the public developer on-ramp as
  governing guidance for an AI-assisted developer-onboarding conversation. It
  requires explicit developer-onramp intent; opening the repository or asking
  about it does not activate the mode. Start with
  [`CONTEXT_LAYER.md`](CONTEXT_LAYER.md), which defines the developer runtime
  loading order, activation handshake, failure behavior, and mode transitions.
- **Read-only consultant process-capture context mode** guides a consultant,
  trainer, or manager through capturing one business process with an SME. It
  requires explicit consultant-lane/process-capture intent. Start with
  [`consultant-lane/CONTEXT_LAYER.md`](consultant-lane/CONTEXT_LAYER.md), not
  the root runtime entrypoint.
- **Author mode** maintains this repository itself. Use
  [`AGENTS.md`](AGENTS.md), then [`.github/copilot-instructions.md`](.github/copilot-instructions.md)
  and [`CONTRIBUTING.md`](CONTRIBUTING.md), when the user explicitly asks for
  repository maintenance.

This repository is not the learner's application repository. Learner-specific
state, project decisions, project briefs, and evidence belong in the learner's
own project or companion repository.

## Getting the developer context layer into an AI chat

For a consultant process-capture conversation, use the
[Consultant Process-Capture Lane runtime entrypoint](consultant-lane/CONTEXT_LAYER.md)
instead. The instructions below apply only to the developer on-ramp.

You do not need Git, a local clone, or a client-specific "attach" or "import"
feature to start. Use the access path your AI chat supports.

### Tell the AI agent what to do

Send this instruction before supplying a repository URL or any files:

```text
You are the AI agent I am configuring for the AI Development On-Ramp.

Before activating anything:
1. State whether you can directly open and read public GitHub URLs in this
   conversation.
2. Do not retrieve files, invent a repository URL or ref, or return an
   activation handshake yet.
3. Wait for my next message with either a repository URL plus an explicit
   activation request, or the first complete supplied file.

If I later give a repository URL and an explicit activation request, and you
can open public GitHub URLs:
1. Retrieve CONTEXT_LAYER.md first.
2. Retrieve the guiding contract and README.md from the same repository ref.
3. Report the actual ref and files retrieved.
4. Return the required activation handshake.

If you cannot open public GitHub URLs, or I say I will supply the files:
1. Say plainly that direct repository access is unavailable.
2. Do not claim activation or pretend to have retrieved files.
3. Tell me to supply the three complete files manually, in order.
4. Wait until all three are supplied before returning the handshake.

Use the repository only as read-only onboarding context. Do not modify it.
```

The prompt tells the AI agent how to choose between the direct and manual
paths after the learner supplies a target; it does not give the agent GitHub
access that the chat client does not provide.

### Direct link path

Use a chat that can open public GitHub files. A realistic beginner prompt is
enough:

```text
https://github.com/suretylabs/ai-dev-onramp
this link should help you serve as my guide to understanding and getting my computer ready to develop with AI
```

A more explicit prompt also works:

```text
Use https://github.com/suretylabs/ai-dev-onramp as my read-only guide for this session. Load CONTEXT_LAYER.md first and help me get my computer ready to develop with AI.
```

The chat must retrieve the required files and return the activation handshake
before teaching begins. If it says that it cannot open GitHub URLs, do not
assume activation succeeded. Use the manual file-supply path instead.

Bare curiosity such as "what is this repo?" should not activate the context
layer. Guide, coach, onboarding, or setup intent should.

For reproducible validation, replace the repository URL with a pinned commit
or tag URL and make sure every file comes from that same ref. If you do not
pin a ref, the chat should report the commit or branch it actually loaded.

### Manual file-supply path

This fallback works when the AI chat cannot open GitHub URLs:

1. Send this activation request before supplying any files:

   ```text
   I explicitly identify this repository as the read-only context layer for this conversation. I cannot provide direct GitHub URL access, so I will supply the required files from the same repository ref in the declared order. Do not return the activation handshake until all required files are complete.
   ```

2. Open [`CONTEXT_LAYER.md`](https://github.com/suretylabs/ai-dev-onramp/blob/main/CONTEXT_LAYER.md).
3. Select the file's `Raw` view, copy the complete contents, and paste them
   into the chat with the source URL.
4. Repeat for the
   [`guiding contract`](https://github.com/suretylabs/ai-dev-onramp/blob/main/guides/00-guiding-llm-contract.md),
   then [`README.md`](https://github.com/suretylabs/ai-dev-onramp/blob/main/README.md),
   keeping the same order and repository ref.
5. Wait for the AI to confirm all three required files before supplying
   learner state or asking it to begin onboarding.

The AI must report `Access path: MANUAL FILE SUPPLY`, identify the source ref
as user-attested, and must not claim that it retrieved URLs it only received as
pasted content. Do not use truncated files, files from different refs, or
summaries in place of the complete files. This fallback relies on the learner
supplying the complete contents; it is not an independent integrity or
security check.

For an explicitly activated AI-guided session, follow
[`CONTEXT_LAYER.md`](CONTEXT_LAYER.md) rather than inferring the loading order:

1. retrieve the runtime entrypoint;
2. load the guiding contract and this README;
3. load learner state when supplied;
4. load the current phase guide and other references only as needed.

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

PolyForm Noncommercial License 1.0.0. See [`LICENSE`](LICENSE).
