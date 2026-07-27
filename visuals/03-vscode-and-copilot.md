# 03 — Visual VS Code and Copilot

This is the mental-model companion for the integrated workspace and the correct first use of Copilot.

Diagram legend: blue = one-folder role, purple = workspace tool, teal = first-use step, green = do, red = avoid, cylinder = durable reference document. See [visuals/README.md](README.md#reading-these-diagrams) for the full shape vocabulary.

```mermaid
flowchart TB
    classDef primary fill:#eff6ff,stroke:#2563eb,color:#111827,stroke-width:1.5px
    classDef workspace fill:#f5f3ff,stroke:#7c3aed,color:#111827,stroke-width:1.5px
    classDef durable fill:#ecfeff,stroke:#0f766e,color:#111827,stroke-width:1.5px
    classDef shouldNode fill:#f0fdf4,stroke:#15803d,color:#111827,stroke-width:1.5px
    classDef avoid fill:#fef2f2,stroke:#dc2626,color:#111827,stroke-width:1.5px

    subgraph folder_model["1. One folder, several roles"]
        direction LR
        f1["Windows folder"] --> f2["Git repository"] --> f3["VS Code workspace"] --> f4["Project codebase"]
    end
    class f1,f2,f3,f4 primary
    style folder_model fill:#ffffff,stroke:#cbd5e1

    subgraph vscode["2. What VS Code brings together"]
        direction TB
        subgraph vscode_first["Workspace tools"]
            direction LR
            v1["Editor"] --> v2["Integrated terminal"] --> v3["Extensions"]
        end
        subgraph vscode_second["Project awareness"]
            direction LR
            v4["Source control view"] --> v5["Python tooling"] --> v6["Copilot"]
        end
        v3 --> v4
    end
    class v1,v2,v3,v4,v5,v6 workspace
    style vscode fill:#ffffff,stroke:#cbd5e1
    style vscode_first fill:#f5f3ff,stroke:#cbd5e1
    style vscode_second fill:#f5f3ff,stroke:#cbd5e1

    subgraph first_use["3. Correct first use of Copilot"]
        direction TB
        subgraph first_use_first["Establish shared understanding"]
            direction LR
            c1["Open the repository"] --> c2["Copilot reads bootstrap documents"] --> c3["Copilot restates its understanding"]
        end
        subgraph first_use_second["Make context durable"]
            direction LR
            c4["Developer corrects and adds context"] --> c5["Project brief becomes durable"] --> c6(["Only then begin implementation"])
        end
        c3 --> c4
    end
    class c1,c2,c3,c4,c5,c6 durable
    style first_use fill:#ffffff,stroke:#cbd5e1
    style first_use_first fill:#ecfeff,stroke:#cbd5e1
    style first_use_second fill:#ecfeff,stroke:#cbd5e1

    subgraph behavior["4. Copilot behavior"]
        direction LR
        should["Copilot should<br/><br/>Ask clarifying questions<br/>Explain unfamiliar tools<br/>Inspect errors and evidence<br/>Summarize legitimate next choices<br/>Generate code after the project is understood"]
        should_not["Copilot should not begin by<br/><br/>Scaffolding a random app<br/>Assuming requirements<br/>Overwriting structure without agreement<br/>Presenting inference as documented fact"]
    end
    class should shouldNode
    class should_not avoid
    style behavior fill:#ffffff,stroke:#cbd5e1

    subgraph context["5. Durable context files"]
        direction TB
        subgraph context_first["Project and setup"]
            direction LR
            d1[("docs/PROJECT_BRIEF.md<br/>what the project is")] --> d2[("docs/BOOTSTRAP_STATE.md<br/>where setup stands")]
        end
        subgraph context_second["AI and repository rules"]
            direction LR
            d3[(".github/copilot-instructions.md<br/>how the AI should operate")] --> d4[("README.md<br/>how the repository is used")]
        end
        d2 --> d3
    end
    class d1,d2,d3,d4 primary
    style context fill:#ffffff,stroke:#cbd5e1
    style context_first fill:#eff6ff,stroke:#cbd5e1
    style context_second fill:#eff6ff,stroke:#cbd5e1
```

The procedural guides remain the step-by-step operating layer.

[Back to the guide map](../README.md)
