# Contributing to AI Development On-Ramp

Thanks for considering a contribution. This repository is a curated, AI-guided
on-ramp: a **guide sequence**, a **visual companion**, a set of
**templates**, and per-stack **reference** material — not an application
codebase. Contributions are almost always Markdown and Mermaid, not code.

## Operating modes

This repository can be used as read-only context for an onboarding
conversation or maintained as a documentation repository. Read-only context
mode requires an explicit user activation and is governed by
[`CONTEXT_LAYER.md`](CONTEXT_LAYER.md) and [`AGENTS.md`](AGENTS.md). It does
not authorize review, testing, issue creation, or modification of this
repository.

Author mode begins only when the user explicitly requests repository
maintenance. In that mode, follow [`AGENTS.md`](AGENTS.md), this contributor
guide, and [`.github/copilot-instructions.md`](.github/copilot-instructions.md).

## Before you start

- For anything beyond a small fix (a new guide, a new visual, a
  restructuring, or a new track — see
  [Extending to another tech stack](#extending-to-another-tech-stack)), open
  an issue first and describe the change. Agree on scope before writing
  content, the same way the guides ask a learner to clarify before acting.
- For typos, broken links, or small clarifications, open a pull request
  directly.
- Keep each pull request focused on one concern. Small, reversible changes
  are easier to review and revert.

## Repository layout

| Path | Status | Purpose |
|---|---|---|
| `README.md` | present | Entry point: target environment, guide sequence table, visual companion, governing principles, templates list. |
| `LICENSE` | present | PolyForm Noncommercial License 1.0.0. |
| `guides/` | present | Procedural and instructional sequence for phases 0–9, indexed by `guides/README.md`. |
| `visuals/` | present | Mental-model companion. One Mermaid diagram per page, indexed by `visuals/README.md`. |
| `templates/` | present | Reusable bootstrap state, decision, project brief, and Copilot instruction templates, indexed by `templates/README.md`. |
| `reference/` | present | Per-stack technical reference content, starting with `reference/PYTHON_STYLEGUIDE.md` for the Python/uv track. On-ramp teaching material, not this repository's own coding standard. |

## Content conventions

- **Audience**: experienced developers who are new to this specific
  toolchain, not to software engineering. Translate historical terminology
  before correcting it; do not re-explain general programming concepts.
- **Structure**: use numbered phases and tables for sequential material, the
  way the guide sequence and templates lists already do. Use fenced
  ` ```text ` blocks for environment/flow outlines that are not diagrams.
- **Diagrams are Mermaid, not images.** Do not commit SVG, PNG, or other
  binary image assets for diagrams. Every visual page holds exactly one
  ` ```mermaid ` `flowchart`, with `classDef`/`class` used for the
  color-coded groupings already established in `visuals/`.
- **Mermaid class-name gotcha**: don't give a `classDef` the same name as a
  plain-text node id used elsewhere in the same diagram (for example, a
  class called `sequence` colliding with a node id `sequence`) — Mermaid can
  misparse the collision. Suffix ambiguous class names instead
  (`sequenceNode`, `remoteNode`, `shouldNode`, etc.), matching the pattern
  already used in `visuals/`.
- **Keep the indexes in sync.** Any time a visual, guide, template, or
  reference page is added, renamed, or removed, update its directory index
  and the relevant table or list in the root `README.md` in the same pull
  request.
- **Keep reusable and personal content separate.** Public guides and
  templates must not include names, private repository content, credentials,
  production data, or learner-specific state. Personal overlays should link
  back to this repository rather than duplicating the canonical guides.

## Extending to another tech stack

This repository currently implements exactly one on-ramp track: Windows 11,
GitHub, VS Code + Copilot, Python 3.14 managed by uv, Polars/Parquet/DuckDB
(plus MSSQL/PDF when needed), and Ruff/Pyright/pytest — the block described
under "Target environment" in `README.md`. It is intentionally shaped so a
second track (a different OS, a different language/runtime, a different
data stack, and so on) can sit alongside it later without fighting the first
track's structure. That work is out of scope for most contributions — the
steps below describe how to propose it, not an invitation to build it out
speculatively.

1. **Open an issue first.** Fill out a "Target environment" block for the
   new stack in the same shape as the existing one, and list which phases of
   the existing guide sequence are reused, replaced, or skipped. Get
   agreement on scope before authoring content.
2. **Reserve, don't rename, the namespace.** Once a second track is
   approved, both tracks get a short kebab-case slug (today's implicit track
   is `windows-python`), and stack-specific content moves under it:

   ```text
   guides/<track-slug>/NN-topic.md
   visuals/<track-slug>/NN-topic.md
   ```

   Do not preemptively move today's `guides/*.md` or `visuals/*.md` into a
   `windows-python/` subtree ahead of a second track existing. That move
   belongs in the same pull request that lands the second track, as one
   coordinated rename instead of speculative churn. `reference/` is the
   exception: its files are already self-namespaced by stack-specific
   filenames (`PYTHON_STYLEGUIDE.md`), so a new stack adds its own sibling
   file (for example `TYPESCRIPT_STYLEGUIDE.md`).
3. **Keep stack-agnostic material shared.** The governing principles, the
   guiding-LLM contract, and the `templates/` documents describe how to run
   the on-ramp process itself, not a specific stack. They stay at the top
   level and are reused across tracks unless a track has a concrete reason
   to diverge.
4. **Let the README grow from one sequence into a list of tracks.** Once a
   second track is added, `README.md`'s single guide-sequence table becomes
   a short list of tracks, each linking to its own guide-sequence table and
   visual companion — not before.

This mechanism is for a genuinely separate track — a different OS,
language/runtime, or data stack. It does not apply to an alternative
execution environment for the *same* stack, such as running today's
Windows-hosted track's tools inside WSL2. That kind of in-track variant is
lighter-weight: a single non-numbered stub guide (for example
[`guides/alt-wsl-development-path.md`](guides/alt-wsl-development-path.md))
plus an "Alternative paths" entry in `guides/README.md`, with no new
namespace and no change to the existing numbered sequence.

## Pull requests

- Branch names should describe the change (for example `docs/<short-topic>`
  or `fix/<short-topic>`). External contributors should fork.
- Describe how you validated the change: review Markdown rendering, internal
  links, terminology, current-tooling claims, and any Mermaid affected by
  the pull request. This repository does not currently have an application
  build or test suite of its own.
- Maintainers review and decide when to merge; opening a pull request does
  not merge it.

## License

By contributing, you agree that your contribution is licensed under this
repository's [PolyForm Noncommercial License 1.0.0](LICENSE).
