# GitHub Copilot Instructions

> This file begins as a provisional repository contract. Populate it from the operator's explanation of the real project before generating project code. Do not infer missing business facts. Keep the fuller contract in `docs/PROJECT_BRIEF.md` and update both files when understanding changes.

## Project identity

- **Business context:** Describe the process or operational setting in the operator's own terms.
- **Problem being solved:** State the concrete pain, risk, delay, or missing capability.
- **Primary user or operator:** State who uses the result and what action or decision it supports.
- **First useful capability:** Define the smallest outcome that would create real value.
- **Primary inputs:** Identify known sources such as MSSQL tables/views, PDFs, files, or manual inputs.
- **Primary outputs:** Identify the expected artifact, report, dataset, decision support, or workflow result.
- **Current phase:** State whether the repository is documenting, prototyping, integrating, or hardening.
- **Explicit non-goals:** State what is intentionally deferred.
- **Open questions:** Preserve unresolved decisions rather than inventing answers.

For fuller requirements, evidence expectations, security boundaries, and acceptance criteria, read `docs/PROJECT_BRIEF.md`.

## Development environment

- Native Windows 11 development environment.
- Use PowerShell 7 (`pwsh`) for shell commands.
- Target Python 3.14.
- Use uv exclusively for Python installation, dependency management, locking, environments, and command execution.
- Do not use global `pip` or introduce another Python environment manager.
- Run Python and project tools through `uv run`.

## Repository orientation

Before changing code:

1. Read `docs/BOOTSTRAP_STATE.md` first when present, then `README.md`, `docs/PROJECT_BRIEF.md`, and `docs/DECISIONS.md`.
2. Restate the current phase, last verified checkpoint, blocker if any, and proposed resume action.
3. Inspect `pyproject.toml`, the relevant source files, and existing tests.
4. State assumptions and identify the files likely to change.
5. Do not invent missing project contracts or configuration.

## Coding approach

- Use modern Python 3.14 syntax and complete type annotations.
- Prefer small modules and explicit interfaces.
- Prefer functions for stateless transformations and classes when state/lifecycle warrants them.
- Use Polars as the default DataFrame engine.
- Use DuckDB for local analytical SQL and direct Parquet queries.
- Use `mssql-python` for MSSQL connectivity unless `docs/DECISIONS.md` records an approved reason to use another library.
- Treat Parquet as a typed columnar artifact, not as a database server.
- Keep extraction, transformation, persistence, and query concerns testable independently.
- Do not add dependencies without explaining the missing capability and confirming Python 3.14 support.

## Data and security

- Never hardcode credentials, tokens, connection strings, or sensitive paths.
- Keep local secrets in ignored environment/configuration surfaces approved by the project.
- Maintain `.env.example` with safe placeholders only when environment variables are used.
- Use read-only MSSQL access for extraction unless write access is explicitly approved.
- Do not log sensitive row contents by default; prefer counts, schemas, hashes, and bounded diagnostics.
- Preserve source documents and source data as immutable inputs unless the project contract states otherwise.

## Scope discipline

- Change only what the task requires.
- Do not perform unrelated cleanup or architectural refactoring.
- Record adjacent concerns separately rather than silently expanding scope.
- For multi-file work, propose a plan before editing.
- After editing, summarize the diff and identify any generated artifacts.

## Validation

Use the commands configured by this repository. The expected baseline is:

- Ruff formatting and linting;
- Pyright type checking;
- pytest tests;
- a targeted end-to-end command when the task affects the data path.

Do not claim completion until the relevant commands have run successfully. Report warnings, skipped checks, and unverified external integrations explicitly.

## Git workflow

- Inspect `git status` before work.
- Use a focused branch for a coherent change when appropriate.
- Review the diff before staging.
- Review the staged diff before committing.
- Do not commit generated data, `.venv`, local secrets, or temporary files.
- Use clear commit messages that describe the behavior change.

## Interaction with the operator

The operator is an experienced developer transitioning to this toolchain. When historical terminology differs from current usage, map the concepts precisely and use modern terminology without patronizing explanation.

When asked for step-by-step terminal help, provide one PowerShell command at a time, wait for the complete output, evaluate it, and then decide the next action.

Maintain `docs/BOOTSTRAP_STATE.md` as a concise operational record of verified state, completed gates, decisions, blockers, deferred work, and the exact resume point. Update it at meaningful state transitions and at the end of each session. Do not turn it into a transcript.

At meaningful boundaries, present a checkpoint: summarize what is verified, state whether the gate passed, offer no more than two or three legitimate next paths, explain their consequences, recommend one when warranted, and ask the operator which path to take. If a prerequisite is unmet, offer troubleshooting or a recorded pause rather than pretending the next phase is ready.
