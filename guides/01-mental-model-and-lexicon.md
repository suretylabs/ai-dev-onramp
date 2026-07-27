# Mental Model and Lexicon Bridge

> Companion: [Visual meta flow](../visuals/00-meta-flow.md)

## Purpose

This document tells the guiding LLM how to recognize an established software-development mental model and connect it to current terminology without creating avoidable friction.

Modern development did not replace directories, files, libraries, interpreters, databases, or builds. It attached additional state and coordination mechanisms to them. The primary teaching task is to distinguish those layers.

## A folder can have several simultaneous roles

A physical Windows folder may be all of the following at once:

| Role | Meaning |
|---|---|
| Directory or folder | A filesystem container. |
| Project root | The top-level location whose files define one project. |
| Working tree | The checked-out files that Git compares with committed history. |
| Git repository | The working tree plus Git metadata and local history. |
| VS Code workspace | The set of folders and settings currently opened by the editor. |
| Python project | A project described by `pyproject.toml` and managed as a unit. |
| Codebase | The total implementation: source, tests, configuration, documentation, and related artifacts. |

When the developer says “the directory,” infer the intended role from context. Then answer using both layers:

> “At the filesystem level, yes, that is the directory. Because it contains `.git`, it is also the repository’s working tree. Because it contains `pyproject.toml`, it is also the Python project root.”

## Translation table

| Historical or broad term | Likely intended concept | Modern distinction to introduce |
|---|---|---|
| directory / source directory | Project files | Folder, project root, working tree, repository, or workspace depending on context. |
| source tree | Hierarchical source layout | Repository tree or project structure. |
| code | The implementation | Source code specifically; codebase when including tests, configuration, docs, and automation. |
| program | Something that runs | Script, command-line application, package, service, module, or process. |
| library | Reusable code | Library as a concept; Python package as an installed distribution; module as an importable file or namespace. |
| executable | Runnable artifact | Native executable, interpreter, console command, module entry point, or script. |
| build | Produce runnable software | In Python this can mean resolving dependencies, creating an environment, packaging, validating, or building a wheel; not always compilation. |
| compiler error | Development-time failure | Syntax error, type-checker diagnostic, linter diagnostic, import error, test failure, or runtime exception. |
| check in | Record a source-control change | Git commit locally; push is a separate remote transfer. |
| check out | Retrieve or lock source | In Git, switch branch/commit or populate a working tree; normally no exclusive lock. |
| source-control server | Central repository | Git is distributed; GitHub hosts a remote repository and collaboration services. |
| save | Write current buffer to disk | Save affects the working tree only; it does not stage, commit, or push. |
| backup | Preserve a copy | A commit preserves history locally; a push transfers commits remotely; neither replaces a full backup policy. |
| project file | Tool configuration | `pyproject.toml`, workspace settings, solution metadata, or build configuration depending on context. |
| make/build script | Repeatable project operations | Tool-specific commands, task runners, CI workflows, or scripts; `pyproject.toml` describes the Python project. |
| DLL/reference | External reusable dependency | Python package dependency installed into the project environment. |
| runtime | Execution environment | Python interpreter plus standard library, project environment, installed dependencies, OS, and process configuration. |
| database file | Stored relational data | DuckDB can be a file-backed analytical database; Parquet is a file format, not a database server. |
| SQL engine | Database query processor | MSSQL is a client/server DBMS; DuckDB is an embedded analytical SQL engine. |
| data table | Rows and columns | SQL table, Polars DataFrame, Arrow table, or Parquet dataset depending on where the data lives. |

## Git: four distinct states

A useful old-to-new bridge is that “source control” is no longer one remote operation.

```text
VS Code buffer
   | save
   v
Working tree on disk
   | git add
   v
Staging index
   | git commit
   v
Local repository history
   | git push
   v
GitHub remote repository
```

### Terms

- **Untracked**: A file exists in the working tree but is not yet part of Git history.
- **Tracked and modified**: Git knows the file, and its working-tree content differs from the committed version.
- **Staged**: The exact content selected for the next commit is in Git’s index.
- **Committed**: A snapshot and metadata exist in the local repository history.
- **Pushed**: Local commits have been transferred to a remote repository.
- **Clean working tree**: The checked-out files and staging index contain no uncommitted changes.

Do not use “tracked” as a synonym for “staged.” A tracked file can be modified but not staged.

## Git is distributed, GitHub is remote collaboration

```text
Local machine                                  GitHub
-------------                                  ------
Working tree  -> staging -> local commits  ->  remote commits
                                      push ->
                                      <- pull/fetch
```

Git performs version control locally. GitHub provides remote storage, identity, access control, pull requests, issues, Actions, and collaboration. `gh` is a terminal interface to GitHub. It does not replace `git`.

## Branches and pull requests

- A **branch** is a movable name pointing to a line of commits.
- Creating a branch does not duplicate the entire directory.
- Switching branches changes the working tree to represent another commit line.
- A **pull request** is a proposal to integrate one branch into another, with review, discussion, and automated validation around it.
- A merge records integration. It is not synonymous with copying files.

For the first project, teach branch mechanics after the first clean commit and push, not before the developer has a stable repository model.

## Python: runtime, environment, package, and project

```text
uv
 |-- installs/manages Python 3.14
 |-- creates the project environment (.venv)
 |-- resolves and installs dependencies
 |-- records exact versions in uv.lock
 `-- runs commands in the project environment
```

| Term | Precise meaning |
|---|---|
| Python 3.14 | The interpreter and standard library version targeted by the project. |
| `.venv` | An isolated directory containing the project interpreter linkage and installed packages. It is generated state, not source. |
| Package | Installable reusable Python software. |
| Module | An importable Python file or namespace. |
| Dependency | A package the project requires. |
| `pyproject.toml` | The declarative project definition: identity, Python constraint, dependencies, and tool configuration. |
| `uv.lock` | The resolved, reproducible dependency graph. Commit it. |
| `uv sync` | Make the environment match the project definition and lockfile. |
| `uv add` | Add a dependency through the project manager and update project state. |
| `uv run` | Execute a command within the project environment without depending on manual activation. |

### Activation is not the model

Older virtual-environment tutorials often make shell activation the central mechanism. In this workflow, `uv run` is the reliable execution boundary. Activation can be explained, but it should not become a hidden prerequisite for every command.

## Dynamic language with static analysis

Python is dynamically executed, but a modern Python project can still use strong static feedback:

- Type annotations express expected interfaces.
- Pyright performs static type analysis.
- Ruff performs linting and formatting checks.
- pytest verifies behavior.

Do not frame Python as “untyped.” Distinguish runtime enforcement from static analysis.

## Object orientation in modern Python

The audience already understands OOP. The transition issue is not learning classes; it is learning when Python does not require them.

Guide the AI to prefer:

- modules for namespace and organization;
- functions for stateless transformations;
- dataclasses for structured state;
- protocols or typed interfaces where decoupling matters;
- classes when identity, state, lifecycle, or substitutable behavior warrants them.

Do not recreate Java, C++, or C# class hierarchies by reflex. Explain Pythonic composition and data-oriented pipelines as engineering choices, not as rejection of OOP.

## Data stack boundaries

```text
MSSQL
  | read through an approved driver/query
  v
Polars DataFrame
  | transform, validate, reshape
  v
Parquet files
  | durable columnar interchange/storage
  v
DuckDB
  ` query locally with SQL, including direct Parquet scans
```

- **MSSQL** is the operational or source database server.
- **Polars** is an in-process DataFrame engine used to transform data.
- **Parquet** is a typed columnar file format.
- **DuckDB** is an embedded analytical SQL engine.
- **PyArrow** often supplies interoperability for Arrow/Parquet paths; install it when required by the selected libraries or operations.

Do not call Parquet “local SQL.” DuckDB provides local SQL; Parquet is data storage that DuckDB can query.

## VS Code boundaries

| Component | Responsibility |
|---|---|
| VS Code | Editor, workspace host, terminal host, debugger, extension platform, Git UI. |
| PowerShell 7 | Shell and command environment. |
| Git | Local version-control engine. |
| GitHub | Remote repository and collaboration platform. |
| GitHub CLI (`gh`) | Terminal interface to GitHub services. |
| GitHub Copilot | AI assistance inside the repository and editor context. |
| Python extension/Pylance | Python language support and editor diagnostics. |
| Ruff extension | Fast editor linting and formatting feedback. |

VS Code is not the compiler, package manager, source-control system, or Python runtime. It integrates those tools.

## AI terminology and operating modes

Product labels can change. Teach the enduring distinction:

- **Conversation/explanation**: Ask the AI to explain, inspect, or compare without changing files.
- **Planning**: Ask it to identify files, dependencies, risks, and validation before editing.
- **Scoped editing**: Permit changes to explicitly named files or a defined task.
- **Agentic execution**: Permit the AI to use tools and perform a bounded workflow, while requiring diff and validation evidence.

The AI is not authoritative merely because it can edit files. Repository instructions, tests, tool output, and source documentation remain the evidence.

## Response pattern when terminology diverges

Use this structure:

1. **Acknowledge the intended concept**: “You are describing the source directory.”
2. **Name the current term**: “In Git, the checked-out directory is called the working tree.”
3. **Explain the added boundary**: “The repository also includes local history, which is not visible as ordinary project files.”
4. **Use the modern term going forward**: “We will inspect the working tree with Git status.”

The goal is not vocabulary replacement. It is operational precision.

## Transition checkpoint

Update `BOOTSTRAP_STATE.md` with the terminology mappings that were actually useful and any areas that remain unclear.

Then offer a real choice:

1. move to the Windows 11 baseline and begin inspecting the machine; or
2. stay in the mental-model phase briefly and work through one concrete example from the developer's historical development experience.

Recommend moving to the Windows baseline unless a terminology mismatch would materially interfere with the first installation steps.
