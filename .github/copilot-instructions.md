# GitHub Copilot Instructions

## Mode boundary

These instructions govern **author mode** and maintenance of this repository.
When a user explicitly mounts the developer on-ramp as read-only context,
[`AGENTS.md`](../AGENTS.md) and [`CONTEXT_LAYER.md`](../CONTEXT_LAYER.md)
govern instead. When they explicitly mount the Consultant Process-Capture Lane,
[`AGENTS.md`](../AGENTS.md) and
[`consultant-lane/CONTEXT_LAYER.md`](../consultant-lane/CONTEXT_LAYER.md)
govern instead. Using the repository as context is not authorization to review,
modify, test, or create issues or pull requests for this repository.

## Project Overview

AI Development On-Ramp is a repository-centered, AI-guided transition into
GitHub, VS Code, modern Python, and evidence-driven engineering, for
experienced developers adopting a contemporary toolchain. It is **not** a
beginner programming course — the material addresses the operational gap
(Git, GitHub, VS Code, PowerShell 7, `gh`, uv, modern Python project
isolation, quality tooling, and collaborating with an LLM inside a
repository), not general software design, debugging, or production systems.

The on-ramp is organized as a guide sequence, a Mermaid-based visual
companion, reusable project templates, and per-stack reference material.
Read the root [`README.md`](../README.md) and
[`CONTRIBUTING.md`](../CONTRIBUTING.md) before making structural changes.

## Repository Structure

- `README.md` — entry point: target environment, guide sequence, visual
  companion, governing principles, templates, and stack reference.
- `guides/` — implemented procedural sequence for phases 0–9, indexed by
  `guides/README.md`.
- `visuals/` — implemented Mermaid mental-model companion (one `flowchart`
  per page, indexed by `visuals/README.md`).
- `templates/` — implemented reusable state, decision, project-brief, and
  Copilot-instruction templates, indexed by `templates/README.md`.
- `reference/` — per-stack technical reference content, starting with
  `reference/PYTHON_STYLEGUIDE.md` for today's Python/uv track. This is
  on-ramp teaching material, not this repository's own coding standard —
  the repository itself ships no application code.
- `CONTRIBUTING.md` — repository layout, content conventions, separation of
  reusable and personal content, and the convention for proposing a second
  tech-stack track alongside today's Windows + Python track.

This repository currently has no application code, build step, or test
suite of its own — it is documentation plus diagrams. The Python and
testing sections below apply only when Python example content is authored
under `guides/` or `reference/`.

## Python Example Content

- When writing or editing Python snippets, examples, or a workspace under
  `guides/` or `reference/`, follow
  [`reference/PYTHON_STYLEGUIDE.md`](../reference/PYTHON_STYLEGUIDE.md):
  Google-style docstrings, type hints, `logging` over `print`, import
  discipline, and the required manual review after any automated
  Ruff/Pyright pass.
- Use `uv` exclusively for any Python dependency and environment management
  shown or scripted (`uv add`, `uv sync`, `uv run python ...`). Do not show
  or use `pip` directly, and do not add a dependency without confirming
  it's needed for the task at hand.
- Target Python 3.14, matching the on-ramp's "Target environment" in
  `README.md`. If another stack track is later added, its own reference
  document under `reference/` governs its examples instead.

## Documentation and Diagrams

- Diagrams are Mermaid code blocks, not committed SVG/PNG/binary images —
  see `CONTRIBUTING.md`'s Content conventions, including the `classDef`
  name-collision gotcha.
- Do not add or redesign visuals unless the requested scope includes the
  visual layer.
- Keep directory indexes and the relevant root `README.md` tables in sync
  whenever a page is added, renamed, or removed.
- Write for the stated audience: experienced developers new to *this*
  toolchain, not to software engineering generally. Translate historical
  terminology before correcting it.
- Keep learner-specific context and live state out of the public guides.
  Personal companion repositories should reference the public canonical
  material and contain only their own context, state, decisions, project
  brief, and personalized instructions.

## Testing

- Once Python example code exists, follow a prove-it flow for bug fixes:
  add a failing test first, then implement the fix, then rerun the suite to
  confirm no regressions.
- Prefer `pytest`. Keep tests colocated with the workspace or guide they
  validate rather than inventing a repo-wide test tree ahead of need.

## Engineering Practices

- Make small, reversible changes and validate them before considering a
  task done — this mirrors the on-ramp's own governing principles in
  `README.md`.
- Scope discipline: touch only what the task requires. If you notice an
  adjacent improvement outside scope, note it rather than editing it
  without approval.
- Never request or print credentials, tokens, recovery codes, or secrets in
  chat or commits. This is a public repository.

## Git Workflow

- Use a feature branch for changes (for example `docs/<short-topic>` or
  `chore/<short-topic>`); do not commit directly to `main`.
- Open a pull request for review. Do not merge a pull request — including
  with an admin override — unless the user explicitly approves the merge in
  the current conversation.
- Keep pull requests focused on one concern, matching the branch/PR pattern
  already used in this repository's history.
