# Python 3.14 and uv

> Companion: [Python and uv visual](../visuals/04-python-uv-and-workspace.md) · [Python style guide](../reference/PYTHON_STYLEGUIDE.md)

## Outcome

Create a reproducible Python 3.14 project in which uv owns:

- Python version acquisition;
- the project environment;
- dependency resolution;
- the lockfile;
- command execution.

Do not install a separate Python distribution first unless a business constraint requires it. uv can install and manage Python directly.

## Install uv

Use the current official Astral installation path for Windows. The LLM should generate the command at runtime from official documentation and explain whether it invokes an installation script or WinGet.

Before running an internet-delivered PowerShell script:

- identify the official source;
- explain the temporary execution-policy scope;
- offer to inspect the script first if the developer prefers;
- do not make a permanent machine-wide policy change.

After installation:

1. open a fresh `pwsh` session;
2. verify `uv` version and executable path;
3. record both;
4. update uv before relying on newly released Python distributions if necessary.

## Install and verify Python 3.14 through uv

The LLM should guide the operator to:

- inspect Python versions uv can see;
- install the latest supported CPython 3.14 patch release through uv;
- verify that the installation is uv-managed;
- record the exact version and path;
- avoid conflating `python` on PATH with the interpreter selected inside a uv project.

A global `python` command is convenient but not the project authority. The project’s Python constraint and uv selection are authoritative.

## Add Python to the existing project repository

The real project repository should already exist, with its project brief and initial Copilot instructions committed. Initialize the uv/Python project **in that repository** rather than creating a disconnected second project.

If the earlier Git exercise had to use a disposable repository, stop and create the real project repository now, complete the project-articulation gate, and only then initialize Python.

The LLM should initialize the project interactively and then inspect the generated and pre-existing files. The important state is:

```text
<project-root>/
  .git/
  .gitignore
  .python-version
  pyproject.toml
  uv.lock
  .venv/                 generated; not committed
  src/ or package files
  tests/
  README.md
  docs/
    PROJECT_BRIEF.md
    DECISIONS.md
  .github/
    copilot-instructions.md
```

The precise source layout should fit the project. For a durable business project, prefer a `src` layout once the package name is known. Do not overwrite the earlier project documents when running uv initialization.

After the environment and commands are verified, update `.github/copilot-instructions.md` so provisional toolchain entries become exact repository facts: Python requirement, uv commands, package path, and validation commands.

## Python requirement

Set an explicit project requirement targeting Python 3.14, for example the semantic intent:

```text
>=3.14,<3.15
```

The LLM should use current uv project commands rather than asking the developer to hand-edit generated metadata unless the edit itself is being taught.

## Environment model

Explain what occurs when uv synchronizes:

1. Read `pyproject.toml`.
2. Respect the Python version constraint and `.python-version`.
3. Resolve compatible dependency versions.
4. Record the exact graph in `uv.lock`.
5. Create or update `.venv`.
6. Install the resolved packages into that environment.

`.venv` is disposable generated state. `pyproject.toml` and `uv.lock` are durable project state and should be committed.

## Command execution model

Prefer:

```text
uv run <command>
```

This ensures the command runs in the project environment. Do not make shell activation the hidden condition for correct behavior.

Teach the distinction:

- `uv run python ...` runs the project interpreter;
- `uv add ...` changes declared dependencies and lock state;
- `uv sync` reconciles the environment with declared state;
- `uv tool ...` is for standalone tools and is not the default project dependency mechanism;
- global `pip install` bypasses the project contract.

## Add dependencies in layers

Do not install the entire eventual stack in one command. Add packages when their role is about to be demonstrated.

### Development-quality layer

- Ruff
- Pyright
- pytest
- pytest-cov when coverage becomes useful

### Data layer

- Polars
- DuckDB
- PyArrow if required for the selected Parquet/interchange path

### Project integration layer

Choose only when requirements are known:

- MSSQL client library — prefer `mssql-python` (see below);
- PDF parser appropriate to text extraction, layout extraction, table extraction, or rendering;
- `python-dotenv` if local environment-file loading is part of the design.

Do not add both `pypdf` and `pdfplumber` merely because PDFs are in scope. Select based on the first use case.

### MSSQL client library: prefer `mssql-python`

Use `mssql-python` for new MSSQL connectivity work:

```text
uv add mssql-python
```

`mssql-python` is Microsoft's own actively maintained DB-API 2.0 driver for
SQL Server, Azure SQL Database, Azure SQL Managed Instance, and Microsoft
Fabric databases. Prefer it over `pyodbc` or `pymssql` because it bundles its
native connectivity components directly in the wheel — there is no separate
Microsoft ODBC Driver for SQL Server to install and no system driver manager
to configure on Windows. It supports SQL login, Windows-integrated, and
Entra ID (Azure AD) authentication.

```python
import os

import mssql_python

conn = mssql_python.connect(
    f"SERVER={os.environ['MSSQL_SERVER']};"
    f"DATABASE={os.environ['MSSQL_DATABASE']};"
    f"UID={os.environ['MSSQL_USER']};"
    f"PWD={os.environ['MSSQL_PASSWORD']};"
    "Encrypt=yes;"
)
cursor = conn.cursor()
cursor.execute("SELECT @@VERSION")
print(cursor.fetchone())
cursor.close()
conn.close()
```

Read the server, database, user, and password from environment variables (via `.env`/`python-dotenv`) rather than hardcoding them, consistent with the credential handling described in `guides/07-first-integrated-workspace.md` and the generated Copilot instructions.

Only choose `pyodbc` (or another library) instead when a project has an
existing, concrete dependency on it — for example an established codebase
already built around it, or a connectivity requirement `mssql-python` does
not yet cover. Record the reason in `docs/DECISIONS.md` when that happens.

## Verify Windows wheel availability

Some Python packages — particularly scientific, ML, or C-extension-backed libraries — do not publish a prebuilt Windows wheel for every release, or require a native C/C++ toolchain to build from source. This is a real, occasional friction point for native Windows development that most Linux/macOS-oriented tutorials never mention.

Before running `uv add <package>`:

1. Check the package's PyPI "Download files" page for a `win_amd64` wheel matching the target Python version, or note that it ships as pure-Python (`py3-none-any`) and is platform-independent.
2. Run `uv add <package>` and read the resolver output. If uv reports building from a source distribution rather than installing a wheel, a compiler toolchain may be invoked; treat this as evidence to record, not silently accept.

If a dependency has no Windows wheel and no practical build path:

- look for a maintained alternative package or a pure-Python fallback first;
- if neither exists, surface the gap explicitly to the developer rather than working around it silently — this is exactly the kind of situation in which choosing the [WSL2 alternative path](alt-wsl-development-path.md) for that part of the work is a legitimate, deliberate decision, not a default.

## Compatibility evidence

For every dependency group:

1. add through uv;
2. observe the resolver output;
3. run a minimal import/version check through `uv run`;
4. inspect lockfile changes;
5. commit only after the environment is coherent.

If a package fails under Python 3.14, do not silently downgrade Python. Diagnose and present options.

## VS Code interpreter integration

After `.venv` exists:

- verify that VS Code identifies the project interpreter;
- explicitly select the `.venv` interpreter if discovery is wrong;
- confirm Pylance diagnostics use that interpreter;
- confirm the integrated terminal’s `uv run python` reports the expected version;
- avoid hardcoding an absolute interpreter path in a tracked setting when a workspace-relative path is supported.

## First quality commands

The LLM should configure and run the project’s actual commands for:

- formatting;
- linting;
- type checking;
- tests.

Do not merely install these tools. Each must produce a successful result against at least one real source file and test.

## Acceptance gate

This phase passes when:

- uv is installed and verified in a fresh shell;
- uv manages a CPython 3.14 installation;
- the project explicitly targets 3.14;
- `.venv` exists and is ignored by Git;
- `pyproject.toml` and `uv.lock` are committed;
- `uv run python` reports the intended interpreter;
- Ruff, Pyright, and pytest run from the project environment;
- VS Code diagnostics use the project environment;
- no project dependency was installed with global `pip`.

## Transition checkpoint

Update `docs/BOOTSTRAP_STATE.md` with the exact uv and Python versions, interpreter evidence, project constraint, environment location, lockfile state, validation results, and any Python 3.14 compatibility decisions.

Then ask whether the developer would like to:

1. continue to the first integrated Polars/Parquet/DuckDB workspace; or
2. spend additional time inspecting `pyproject.toml`, `uv.lock`, `.venv`, and `uv run` so the environment model is fully clear.

Recommend continuing when they can distinguish the interpreter, project environment, dependency declaration, and lockfile. If any quality command is failing, offer diagnosis or a recorded pause rather than moving forward.
