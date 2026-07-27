# 04 — Visual Python, uv, and the Integrated Workspace

This is the mental-model companion for Python, uv, project environments, dependencies, and the local data stack.

Diagram legend: blue = project-stack step, purple = uv control action, amber/cylinder = dependency artifact, teal = data-stack step, green = validation step. See [visuals/README.md](README.md#reading-these-diagrams) for the full shape vocabulary.

```mermaid
flowchart TB
    classDef primary fill:#eff6ff,stroke:#2563eb,color:#111827,stroke-width:1.5px
    classDef control fill:#f5f3ff,stroke:#7c3aed,color:#111827,stroke-width:1.5px
    classDef dependency fill:#fffbeb,stroke:#b45309,color:#111827,stroke-width:1.5px
    classDef data fill:#ecfeff,stroke:#0f766e,color:#111827,stroke-width:1.5px
    classDef proof fill:#f0fdf4,stroke:#15803d,color:#111827,stroke-width:1.5px

    subgraph python_stack["1. Python project stack"]
        direction LR
        p1["Python 3.14<br/>interpreter"] --> p2[("Project environment<br/>(.venv)")] --> p3["Installed dependencies"] --> p4["Application code"]
    end
    class p1,p2,p3,p4 primary
    style python_stack fill:#ffffff,stroke:#cbd5e1

    subgraph uv_control["2. uv is the control plane"]
        direction TB
        subgraph uv_first["Provision and declare"]
            direction LR
            u1["Install Python"] --> u2["Create the project environment"] --> u3["Declare and install dependencies"]
        end
        subgraph uv_second["Reproduce and run"]
            direction LR
            u4["Lock exact versions"] --> u5["Run commands in project context"]
        end
        u3 --> u4
    end
    class u1,u2,u3,u4,u5 control
    style uv_control fill:#ffffff,stroke:#cbd5e1
    style uv_first fill:#f5f3ff,stroke:#cbd5e1
    style uv_second fill:#f5f3ff,stroke:#cbd5e1

    subgraph dependency_state["3. Dependency state"]
        direction TB
        subgraph dependency_first["Declared intent and resolution"]
            direction LR
            dep1[("pyproject.toml declares<br/>project intent")] --> dep2["uv sync resolves and installs"]
        end
        subgraph dependency_second["Isolation and reproducibility"]
            direction LR
            dep3[(".venv holds the<br/>isolated environment")] --> dep4[("uv.lock records exact<br/>resolved versions")]
        end
        dep2 --> dep3
    end
    class dep1,dep2,dep3,dep4 dependency
    style dependency_state fill:#ffffff,stroke:#cbd5e1
    style dependency_first fill:#fffbeb,stroke:#cbd5e1
    style dependency_second fill:#fffbeb,stroke:#cbd5e1

    subgraph data_stack["4. Data-stack mental model"]
        direction TB
        subgraph data_first["Ingest and transform"]
            direction LR
            d1["MSSQL, PDFs, and source files"] --> d2["Python orchestration"] --> d3["Polars transforms data"]
        end
        subgraph data_second["Store and consume"]
            direction LR
            d4[("Parquet stores<br/>analytical data")] --> d5["DuckDB queries with SQL"] --> d6["Validation, reporting, and exports"]
        end
        d3 --> d4
    end
    class d1,d2,d3,d4,d5,d6 data
    style data_stack fill:#ffffff,stroke:#cbd5e1
    style data_first fill:#ecfeff,stroke:#cbd5e1
    style data_second fill:#ecfeff,stroke:#cbd5e1

    subgraph proof["5. First integrated proof"]
        direction TB
        subgraph proof_first["Build the artifact"]
            direction LR
            q1["Create a small representative input"] --> q2["Load and transform with Polars"] --> q3["Write Parquet"]
        end
        subgraph proof_second["Query and validate"]
            direction LR
            q4["Query with DuckDB"] --> q5["Validate the expected output"] --> q6["Run Ruff, Pyright, and pytest"]
        end
        q3 --> q4
    end
    class q1,q2,q3,q4,q5,q6 proof
    style proof fill:#ffffff,stroke:#cbd5e1
    style proof_first fill:#f0fdf4,stroke:#cbd5e1
    style proof_second fill:#f0fdf4,stroke:#cbd5e1
```

The procedural guides remain the step-by-step operating layer.

[Back to the guide map](../README.md)
