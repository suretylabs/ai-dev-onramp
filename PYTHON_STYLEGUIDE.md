# Python Styleguide

**Last Updated**: July 26, 2026<br>
**Python Version**: 3.14+ (project targets 3.14)<br>
**Applies To**: All non-test `.py` files in the target repository

## Rule Scope and Enforcement

- This document is the normative engineering standard for non-test Python code. `ruff.toml` defines the
  automatically enforceable subset; a rule that is not represented by a Ruff check is still required.
- Ruff is the source of truth for mechanical formatting, import organization, and lint categories. The concrete
  formatter values, enabled rules, ignores, and per-file exceptions belong in `ruff.toml`; do not duplicate them
  here. Ruff is an initial pass, not a substitute for the required manual review below.
- Any Ruff exceptions configured for tests, scripts, or tools are intentional tooling boundaries. They do not
  override the prose rules below; runtime output in non-test scripts and tools should still use `logging`.
- When a rule is not mechanically enforceable, reviewers and agents should report the exception explicitly rather
  than silently weakening the rule or changing the shared Ruff configuration.

## General Principles

- Use Google-style docstrings for all non-test modules, classes, and concrete functions or methods.
- Include type hints for all non-test function parameters and return types.
- Target Python 3.14. Syntax or standard-library APIs newer than the project's stated floor require an explicit
  change to the supported-version contract before use.
- Follow PEP 8 with Ruff as the primary linter/formatter.

## Configuration

- Put script-level runtime or operator-tunable configuration in a top-level `config` dict unless a global config
  file is used by the project.
- Immutable module constants, parser defaults, and internal structural sets are not required to use the `config`
  dict. Keep those as named constants when that makes their scope and immutability clearer.

## Docstrings

- Every non-test module must have a top-level docstring.
- Every standalone script must have a top-level docstring with a copyable usage example that runs it with
  `uv run python path/to/script.py`.
- Use `uv run python` or `uv run python -m` for execution examples.
- Include a `uv run python -m package.module` example when the module supports module execution. Include both
  forms only when both entry points are supported; do not document an invocation that the file does not provide.
- Every non-test class and concrete function or method, including private helpers, should have a Google-style
  docstring. A concise one-line docstring is sufficient when the behavior is obvious from the name, signature,
  and implementation.
- Use expanded `Args:`, `Returns:`, and `Raises:` sections when behavior is not obvious or when the function
  has meaningful failure modes, side effects, platform-specific behavior, filesystem or network boundaries, or
  safety invariants. Document the contract, not information already clear from the type signature.
- Prefer an expanded docstring whenever it adds useful context for a human engineer or an AI coding agent.
  High-value context includes responsibility, lifecycle or ownership, invariants, source-of-truth relationships,
  failure and recovery posture, operational safety boundaries, and meaningful neighboring symbols or entry points.
- Use the repository's canonical domain vocabulary in docstrings and align equivalent concepts with nearby code,
  runbooks, issue contracts, and architecture documentation. Name exact paths, symbols, configuration keys, and
  CLI flags when they materially improve semantic search or handoff; avoid brittle line-number references.
- Treat docstrings as semantic navigation surfaces across the repository: explain why a behavior exists and how it
  relates to adjacent concepts, not just what each line of the implementation does.
- Do not add expansion that merely restates an obvious type signature or duplicates implementation details likely
  to drift. When a concise docstring communicates the complete contract, keep it concise.
- A local nested helper does not need a separate docstring when its purpose is clear from the enclosing function.
  Document non-obvious nested-helper behavior in the enclosing function's prose instead.
- Test modules and test-only helpers may omit docstrings unless they expose a reusable fixture/helper or document
  a non-obvious contract needed by other tests.

**Example**:

```python
"""Example processing module.

Usage:
    # As module (recommended)
    uv run python -m package.module

    # As script
    uv run python package/module/main.py

    # With options
    uv run python -m package.module --output-dir custom --run-date 2024-06-15
"""
```

## Libraries

- Do not install additional libraries unless discussed with the user first.

## Logging

- Use the `logging` module instead of `print()` for user output in scripts.
- Configure logging in the script's `main()` or other entrypoint path with
  `logging.basicConfig(level=logging.INFO, format='%(message)s')`; do not configure logging as an import-time
  side effect.
- Use `logger.info()` for general messages, `logger.warning()` for warnings, `logger.error()` for errors.

## Imports

- Ensure no unused imports; remove any that are not referenced in the code.
- Avoid inline imports; all imports must be at the top of the file.
- Use `from` imports only when necessary; prefer absolute imports for clarity.
- For scripts requiring future annotations (e.g., for forward references in type hints), place
  `from __future__ import annotations` immediately after the module docstring and before any other imports.

## Validation

### Automated initial pass

- Run Ruff linting and formatting on the changed non-test paths:

  ```pwsh
  uv run ruff check path/to/changed_file.py
  uv run ruff format --check path/to/changed_file.py
  ```

- Run focused tests for the affected behavior. Use `get_errors` on changed non-test files when editor diagnostics
  are part of the review.
- Run Pyright only on the scopes actually configured for it (see `pyrightconfig.json` once one exists in this
  repository). A file is not considered type-checked merely because the repository has Pyright installed if its
  path isn't included in that configuration.

### Required manual review

- After the automated pass, an engineer must manually validate the styleguide preferences for every changed
  non-test `.py` file. Review the complete affected module, not only lines reported by Ruff.
- For a repository-wide or broad hygiene sweep, apply the same review to every non-test `.py` file in the declared
  scope. Tests are outside this non-test style review unless the task explicitly includes test-style cleanup.
- Confirm manually that each reviewed file has the appropriate module usage documentation, type hints, configuration
  posture, logging behavior, import structure, and docstring depth.
- Specifically ask whether expanded docstrings add semantic value for future engineers and AI agents. Expand them
  when they clarify contracts, domain terminology, ownership, invariants, failure posture, safety constraints, or
  navigation to related code and documentation. Do not expand them solely to satisfy a uniform visual format.
- Record intentional deviations from this guide in the review or handoff, including why the deviation is safe and
  whether it should become a documented repository exception.
