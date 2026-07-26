# 04 — Visual Python, uv, and the Integrated Workspace

This file explains the Python development environment.

## The Python stack

```mermaid
flowchart TD
    A[Python 3.14] --> B[Project environment .venv]
    B --> C[Dependencies]
    C --> D[Application code]
```

## uv’s role

```mermaid
flowchart TD
    A[uv] --> B[Installs Python]
    A --> C[Creates project environment]
    A --> D[Manages dependencies]
    A --> E[Locks versions]
    A --> F[Runs Python commands]
```

## Dependency model

```mermaid
flowchart LR
    A[pyproject.toml] --> B[Declares project intent]
    B --> C[uv sync]
    C --> D[.venv]
    D --> E[Installed packages]
    C --> F[uv.lock]
```

## Data stack mental model

```mermaid
flowchart TD
    A[MSSQL / PDFs / source files] --> B[Python]
    B --> C[Polars]
    C --> D[Parquet]
    D --> E[DuckDB]
    E --> F[Validation / reporting / exports]
```

## Roles of the core tools

```mermaid
flowchart LR
    A[Polars] --> A1[Transform and shape data]
    B[Parquet] --> B1[Store analytical data efficiently]
    C[DuckDB] --> C1[Query data with SQL]
```

## First integrated proof

```mermaid
flowchart TD
    A[Create small sample or project-relevant input]
    A --> B[Load in Python]
    B --> C[Transform with Polars]
    C --> D[Write Parquet]
    D --> E[Query with DuckDB]
    E --> F[Validate output]
    F --> G[Run tests, lint, and type checks]
```

## Quality gates

```mermaid
flowchart LR
    A[ruff] --> B[Formatting and lint]
    C[pyright] --> D[Type checking]
    E[pytest] --> F[Automated verification]
```
