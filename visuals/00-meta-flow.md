# 00 — Visual Meta Flow

This is the mental-model companion for the complete on-ramp.

Diagram legend: blue = platform-setup step, teal = workspace/delivery step, purple = mental-model concept, amber diamond = gate, green stadium = verified outcome. See [visuals/README.md](README.md#reading-these-diagrams) for the full shape vocabulary.

```mermaid
flowchart TB
    classDef primary fill:#eff6ff,stroke:#2563eb,color:#111827,stroke-width:1.5px
    classDef delivery fill:#ecfeff,stroke:#0f766e,color:#111827,stroke-width:1.5px
    classDef model fill:#f5f3ff,stroke:#7c3aed,color:#111827,stroke-width:1.5px
    classDef note fill:#f8fafc,stroke:#cbd5e1,color:#1f2937,stroke-width:1.5px
    classDef gate fill:#fffbeb,stroke:#b45309,color:#111827,stroke-width:1.5px
    classDef outcome fill:#f0fdf4,stroke:#15803d,color:#111827,stroke-width:1.5px

    subgraph journey["1. Overall journey"]
        direction TB
        subgraph platform_setup["Platform setup"]
            direction LR
            j1["Clean Windows 11 machine"] --> j2["Create personal GitHub identity"] --> j3["Create business GitHub organization"] --> j4["Create organization-owned repository"] --> j5["Install Git and GitHub CLI"] --> j6["Clone repository locally"]
        end
        subgraph adoption["Workspace and delivery"]
            direction LR
            j7["Open repository in VS Code"] --> j8["Enable Copilot and AI assistance"] --> j9["Articulate the real business project"] --> j10["Install Python 3.14 with uv"] --> j11["Create the integrated workspace"] --> j12["Build the first useful workflow"] --> j13(["Adopt the daily<br/>engineering loop"])
        end
        j6 --> j7
    end
    class j1,j2,j3,j4,j5,j6 primary
    class j7,j8,j9,j10,j11,j12 delivery
    class j13 outcome
    style journey fill:#ffffff,stroke:#cbd5e1
    style platform_setup fill:#f8fafc,stroke:#cbd5e1
    style adoption fill:#f8fafc,stroke:#cbd5e1

    subgraph tracks["2. Two tracks run at once"]
        direction LR
        platform["Platform setup<br/>GitHub identity -> organization -> repository -><br/>Git / gh -> VS Code -> Python / uv"]
        mental["Mental model<br/>Local vs remote -> repository vs workspace vs codebase -><br/>tracked / staged / committed / pushed -> AI as collaborator -><br/>environment vs dependencies -> data flow and validation"]
        platform -.->|"runs alongside"| mental
    end
    class platform,mental note
    style tracks fill:#ffffff,stroke:#cbd5e1

    subgraph llm_loop["3. Guiding loop for the LLM"]
        direction TB
        subgraph llm_first["Understand and act"]
            direction LR
            l1["Orient"] --> l2["Clarify"] --> l3["Inspect"] --> l4["Explain"] --> l5["Act"]
        end
        subgraph llm_second["Observe and gate"]
            direction LR
            l6["Observe"] --> l7["Evaluate"] --> l8["Record"] --> l9{"Evidence<br/>sufficient?"}
        end
        l5 --> l6
        l9 -->|"yes"| l10(["Continue"])
        l9 -->|"no"| l11["Pause and surface the blocker"]
        l11 -.->|"resume when unblocked"| l1
    end
    class l1,l2,l3,l4,l5,l6,l7,l8,l11 model
    class l9 gate
    class l10 outcome
    style llm_loop fill:#ffffff,stroke:#cbd5e1
    style llm_first fill:#f5f3ff,stroke:#cbd5e1
    style llm_second fill:#f5f3ff,stroke:#cbd5e1

    subgraph completion["4. Completion standard"]
        direction TB
        subgraph completion_first["Platform and tooling"]
            direction LR
            c1["GitHub identity works"] --> c2["Organization exists"] --> c3["Repository exists and is cloned"] --> c4["VS Code opens the correct workspace"] --> c5["Copilot is active"] --> c6["Python 3.14 and uv work"]
        end
        subgraph completion_second["Integrated proof"]
            direction LR
            c7["The first integrated project runs"] --> c8["Ruff, Pyright, and pytest pass"] --> c9(["Developer can reopen<br/>tomorrow and continue"])
        end
        c6 --> c7
    end
    class c1,c2,c3,c4,c5,c6,c7,c8 delivery
    class c9 outcome
    style completion fill:#ffffff,stroke:#cbd5e1
    style completion_first fill:#ecfeff,stroke:#cbd5e1
    style completion_second fill:#ecfeff,stroke:#cbd5e1
```

The procedural guides remain the step-by-step operating layer.

[Back to the guide map](../README.md)
