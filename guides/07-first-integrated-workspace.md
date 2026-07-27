# First Integrated Workspace

> Companion: [Python workspace visual](../visuals/04-python-uv-and-workspace.md) · [Python style guide](../reference/PYTHON_STYLEGUIDE.md)

## Purpose

Prove the entire toolchain with a small end-to-end data workflow before introducing production MSSQL, business PDFs, authentication complexity, or a large codebase.

This is not a toy language lesson. It is a systems integration proof.

## Capability proof

The first workspace should demonstrate:

1. Python 3.14 execution through uv.
2. Typed, modular Python source.
3. A Polars DataFrame transformation.
4. Parquet output.
5. A DuckDB SQL query against that Parquet output.
6. A deterministic test.
7. Ruff formatting and linting.
8. Pyright type checking.
9. pytest execution.
10. Git commit and GitHub push.
11. Copilot operating under repository instructions.

## Keep the first dataset synthetic

Use a small synthetic dataset that resembles the shape of the future problem without containing business data. The LLM should ask for a few domain-relevant columns, then generate the records deterministically.

For example, a document-oriented business workflow might include:

- document ID;
- source filename;
- account identifier;
- document type;
- received date;
- page count;
- extraction status;
- confidence or review status.

The exact schema should be chosen with the developer, not assumed.

## Recommended repository shape

The LLM should propose a structure and explain every directory before creating it. A reasonable starting point is:

```text
<project-root>/
  .github/
    copilot-instructions.md
  data/
    raw/                 ignored or contains only safe samples
    processed/           generated and usually ignored
  docs/
    PROJECT_BRIEF.md
    DECISIONS.md
  src/
    <package_name>/
      __init__.py
      models.py
      pipeline.py
      queries.py
      main.py
  tests/
    test_pipeline.py
  .env.example
  .gitignore
  .python-version
  pyproject.toml
  uv.lock
  README.md
```

Do not create empty architectural layers solely to resemble an enterprise repository. Add structure as responsibility appears.

## Implementation sequence

### 1. Refine the first vertical-slice contract

Start from the existing `docs/PROJECT_BRIEF.md`. Narrow the already-described business project into the first executable slice by confirming:

- input shape;
- output artifact;
- transformation rules;
- SQL question to answer;
- acceptance criteria;
- deliberately excluded features.

Have Copilot restate this slice and identify assumptions before coding. The AI should not begin implementation until the developer agrees that the slice is both useful and bounded.

### 2. Refine repository instructions

Update the existing `.github/copilot-instructions.md` with:

- Python 3.14 and uv-only rules;
- package structure;
- typing and docstring expectations;
- no hardcoded secrets;
- Polars as the DataFrame default;
- DuckDB for local analytical SQL;
- validation commands;
- scope discipline;
- a pointer to `docs/PROJECT_BRIEF.md` as the fuller business contract.

Do not duplicate the entire project brief in Copilot instructions. Keep the instructions concise and operational.

### 3. Create the smallest vertical slice

Build one command that:

- creates or reads the safe sample data;
- constructs a typed Polars DataFrame;
- validates required columns and data types;
- performs one meaningful transformation;
- writes a Parquet file to the agreed generated-data directory;
- runs one DuckDB query directly against the Parquet file;
- prints or logs a concise result.

Do not add PDF or MSSQL integration yet.

### 4. Add tests

Test behavior rather than implementation trivia. At minimum:

- expected row count or aggregation;
- output schema/data types;
- transformation rule;
- Parquet artifact can be queried by DuckDB;
- invalid input fails clearly.

### 5. Validate

The AI must run the repository’s commands for:

- Ruff format check or formatting;
- Ruff lint;
- Pyright;
- pytest.

A successful manual run is not a substitute for these checks.

### 6. Review the diff

Before commit, explain:

- files added;
- dependencies added;
- generated files intentionally ignored;
- design decisions;
- validation evidence;
- any warnings or compromises.

### 7. Commit and push

Use a coherent commit message. Verify a clean working tree and remote visibility.

## Introduce MSSQL second

After the local vertical slice is stable:

1. Clarify authentication: Windows integrated, SQL login, Azure identity, or another approved method.
2. Identify the current supported Python library and Windows prerequisites.
3. Use a read-only account.
4. Put secret names in `.env.example`, actual values in ignored `.env` or approved secret storage.
5. Begin with a metadata or small bounded query.
6. Log row counts and schema, not sensitive data.
7. Preserve the local sample path so tests do not require database access.

The architecture should separate extraction from transformation so the same transformation can run against a test fixture.

## Introduce PDF handling third

Clarify the PDF problem before choosing a library:

- native text versus scanned image;
- simple text extraction versus layout-aware extraction;
- tables;
- forms;
- page rendering;
- metadata;
- encrypted files;
- evidence/citation requirements.

Then select the narrowest library that fits. Do not introduce OCR unless the files require it.

Use a safe sample PDF and record:

- parser selected;
- reason;
- expected failure modes;
- how page-level evidence will be retained;
- whether original files are immutable inputs.

## Data-boundary model

```text
External source (MSSQL or PDF)
         |
         v
Extraction boundary
         |
         v
Typed Polars representation
         |
         v
Validated transformation
         |
         +--> Parquet artifact
         |
         `--> DuckDB analytical query
```

Keep extraction, transformation, persistence, and query concerns distinct enough to test independently.

## Acceptance gate

This phase passes when:

- the end-to-end local command succeeds from a fresh clone after `uv sync`;
- the Parquet artifact is created and queried by DuckDB;
- tests verify the important behavior;
- Ruff, Pyright, and pytest all pass;
- generated data and secrets are not committed;
- repository instructions are active;
- the commit is pushed to GitHub;
- the developer can explain the role of Polars, Parquet, DuckDB, uv, and the local/remote Git states.

## Transition checkpoint

Update `docs/BOOTSTRAP_STATE.md` with the end-to-end command, artifact locations, test and quality results, Git state, and the specific capabilities now proven.

Then ask whether the developer would like to:

1. move into the daily engineering loop and begin the first real MSSQL-or-PDF vertical slice; or
2. repeat or extend the synthetic data exercise to deepen Polars, Parquet, DuckDB, or testing mechanics.

Recommend beginning the real vertical slice when the local proof is reproducible from declared repository state. Record which external integration will come first and why.
