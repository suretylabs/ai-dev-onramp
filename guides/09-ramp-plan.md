# Multi-Week Ramp Plan

> Companion: [Visual meta flow](../visuals/00-meta-flow.md) · [Gating and state visual](../visuals/06-gating-and-state.md)

## Assumption

This plan is capability-based, not calendar-enforced. Move faster when gates pass cleanly and spend longer where the first business use case demands depth. A session may be brief or may occupy a full workday; elapsed time never substitutes for evidence that the capability gate passed.

The target is productive work within weeks, not mastery of every tool.

## Week 1: machine, source control, editor, and AI operating method

### Goals

- Native Windows development baseline.
- PowerShell 7 and Windows Terminal fluency.
- Git and GitHub mental model.
- GitHub CLI authentication.
- VS Code workspace and terminal integration.
- Copilot used for explanation, planning, and one bounded edit.

### Practical work

- Complete the installer decisions rather than merely obtaining executables.
- Create and push the real project repository with documentation-only first commits.
- Observe each Git state transition.
- Explain the actual business project in the developer's own terms.
- Create and review the initial `docs/PROJECT_BRIEF.md` and `.github/copilot-instructions.md`.
- Use Copilot to restate the project and surface ambiguities before generating code.
- Practice asking for one command and returning output.
- Record decisions and state.

### Exit capability

The developer can move confidently among filesystem, shell, editor, local Git, and GitHub without treating them as one opaque application.

## Week 2: Python 3.14, uv, quality tooling, and data stack

### Goals

- uv-managed Python 3.14.
- Reproducible project environment.
- `pyproject.toml`, `.python-version`, and `uv.lock` understood.
- Ruff, Pyright, and pytest operating.
- Polars, Parquet, and DuckDB capability proof.

### Practical work

- Create the first project from the shell.
- Add dependencies in layers.
- Build the synthetic end-to-end pipeline.
- Use Copilot to plan and implement small functions.
- Review every diff.
- Clone the repository into a second directory or otherwise prove reproducibility from declared state.

### Exit capability

The developer can create, run, validate, commit, and reproduce a modern Python project.

## Week 3: first real use-case vertical slice

### Goals

- Translate the actual business problem into a bounded project contract.
- Integrate either MSSQL or PDF input first, whichever is the most direct path to value.
- Preserve local testability.
- Establish security and data boundaries.

### Practical work

- Refine the existing `docs/PROJECT_BRIEF.md` into a bounded first vertical-slice contract.
- Confirm one useful input and one useful output.
- Add only the required integration library.
- Build a read-only or safe sample path.
- Convert external data into a typed Polars representation.
- persist a Parquet artifact;
- query or validate with DuckDB;
- add tests around transformation logic;
- use a branch and pull request.

### Exit capability

The developer has delivered a real, reviewable business capability using the full platform.

## Week 4 and beyond: hardening and expansion

Potential next capabilities:

- structured configuration;
- logging and error taxonomy;
- MSSQL query modules and connection management;
- PDF page-level evidence and extraction validation;
- richer testing fixtures;
- CI with GitHub Actions;
- release/versioning practices;
- local packaging or command-line entry points;
- Azure integration where the project requires it;
- repository-specific Copilot instructions and skills;
- data lineage, manifests, reconciliation, and audit artifacts.

Add these in response to the project, not as ceremonial enterprise architecture.

## Daily rhythm

A useful work session is not measured by generated-code volume. A balanced session may include:

- 30 minutes: state review and plan;
- 90 minutes: focused concept and mechanical practice;
- 3 hours: implementation in small vertical slices;
- 90 minutes: debugging and evidence-based dialogue with the AI;
- 60 minutes: tests, typing, linting, and diff review;
- 30 minutes: commit, push, and session handoff;
- remaining time: documentation, reading actual library docs, or exploring the business domain.

The exact allocation should adapt to the work.

## Daily and weekly choice gates

Do not treat the calendar as an instruction to advance automatically.

At the end of each substantial block or day:

1. update `docs/BOOTSTRAP_STATE.md`;
2. identify the capability gate that has actually passed;
3. list any optional practice or hardening that was deferred;
4. offer a choice between continuing the current capability, moving to the next bounded capability, or pausing;
5. recommend a path based on evidence, not the nominal week number.

At the end of each week, ask whether the next week’s objective is still the best route to the first useful business result. The ramp plan is a map, not a conveyor belt.

## Progress signals

Progress is demonstrated by operational control, not vocabulary recall.

Strong signals include:

- asking for state inspection before mutation;
- recognizing whether a problem is shell, PATH, Git, environment, package, or code state;
- choosing project-local configuration over global configuration when appropriate;
- challenging an AI plan that adds unnecessary abstraction;
- requiring a test and diff before commit;
- using the CLI to produce evidence;
- rebuilding the environment from the repository contract;
- completing a real vertical slice with clean history.

## Anti-goals

Do not turn the ramp into:

- a survey of every Git command;
- a Python syntax course detached from the business project;
- a fully automated bootstrap script that teaches no state model;
- a giant framework assembled before the first useful output;
- an exercise in accepting AI-generated code without inspection;
- a recreation of the user’s mature repositories on day one.

The mature repositories are patterns to approach progressively. The first project should adopt their operating principles before their full structural complexity.
