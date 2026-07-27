# Alternative Path: WSL2 Development Environment

> Companion: [Local toolchain visual](../visuals/02-local-toolchain.md) (describes the native path; not yet updated for WSL2).

## Status

**Stub.** This file is referenced from [`guides/README.md`](README.md#alternative-paths), [`guides/00-guiding-llm-contract.md`](00-guiding-llm-contract.md), and the root [`README.md`](../README.md), but the procedural content below has not been authored yet. Do not treat the section headings as complete guidance — they mark where that content will go.

## Scope

This is an alternative to [`02-windows-11-baseline.md`](02-windows-11-baseline.md) for developers who prefer to run the Linux-side toolchain (Git, uv, Python, and the rest of the stack) inside WSL2, while still working from a Windows 11 host machine, the same GitHub organization, VS Code, and Copilot.

Native Windows 11 remains the default and first-recommended path for this track. Choose this alternative deliberately — before or during phase 2 — rather than switching to it silently mid-session or introducing it as an ad hoc workaround for a native-Windows problem encountered elsewhere in the sequence.

## What changes versus the native path

- The development root, Git working tree, Python environment, and shell commands move inside the WSL2 Linux filesystem and distribution instead of the native Windows filesystem.
- VS Code attaches through its WSL remote connection instead of editing the Windows filesystem directly.
- Windows Terminal still hosts the session, but the active shell for project work becomes the WSL2 distribution's shell rather than PowerShell 7.

## What stays the same

- GitHub identity, organization, repository, and Copilot entitlement (`03-github-foundation.md`).
- Python 3.14 managed by uv, and the Polars/Parquet/DuckDB/Ruff/Pyright/pytest stack.
- The guiding LLM contract, the daily engineering loop, and the gating discipline.

## To be authored

- WSL2 installation and distribution choice.
- Filesystem boundary rule: keep active project files inside the Linux filesystem, not under `/mnt/c`, to preserve the I/O-performance reason for using WSL2 at all.
- VS Code Remote - WSL setup and verification.
- Git configuration inside WSL2 (identity, credential helper, line endings) and how it interacts with Git for Windows on the same machine.
- Which later-phase steps in the numbered sequence stay identical, and which need a WSL2-specific substitution.
- A dedicated visual, if the differences are large enough to warrant one.

[Back to the guide index](README.md)
