# 02 — Visual Local Toolchain

This is the mental-model companion for the Windows workstation, local tooling, and the Git round trip.

Diagram legend: blue = local-stack step, purple = round-trip step, teal/cylinder = durable remote store, amber stadium = tracked Git state, gray = explanatory note. See [visuals/README.md](README.md#reading-these-diagrams) for the full shape vocabulary.

```mermaid
flowchart TB
    classDef primary fill:#eff6ff,stroke:#2563eb,color:#111827,stroke-width:1.5px
    classDef model fill:#f5f3ff,stroke:#7c3aed,color:#111827,stroke-width:1.5px
    classDef remoteNode fill:#ecfeff,stroke:#0f766e,color:#111827,stroke-width:1.5px
    classDef state fill:#f0fdf4,stroke:#15803d,color:#111827,stroke-width:1.5px
    classDef note fill:#f8fafc,stroke:#cbd5e1,color:#1f2937,stroke-width:1.5px

    subgraph local_stack["1. Local stack"]
        direction TB
        subgraph local_stack_first["Operating system and tools"]
            direction LR
            l1["Windows 11"] --> l2["PowerShell 7"] --> l3["Git for Windows"] --> l4["GitHub CLI (gh)"]
        end
        subgraph local_stack_second["Workspace and runtime"]
            direction LR
            l5["VS Code"] --> l6["uv"] --> l7["Python 3.14"]
        end
        l4 --> l5
    end
    class l1,l2,l3,l4,l5,l6,l7 primary
    style local_stack fill:#ffffff,stroke:#cbd5e1
    style local_stack_first fill:#eff6ff,stroke:#cbd5e1
    style local_stack_second fill:#eff6ff,stroke:#cbd5e1

    subgraph powershell["2. Why PowerShell matters"]
        direction TB
        ps["Inspectable control plane<br/><br/>Commands run in PowerShell produce exact output.<br/>The developer can return that output to the LLM,<br/>which can evaluate actual machine state instead of<br/>guessing what happened in an installer or GUI."]
    end
    class ps note
    style powershell fill:#ffffff,stroke:#cbd5e1

    subgraph local_remote["3. Local versus remote"]
        direction LR
        local["Local machine<br/><br/>PowerShell<br/>VS Code<br/>Local repository<br/>Local files and project environment"]
        remote[("Remote GitHub<br/><br/>Organization repository<br/>Canonical history<br/>Collaboration surface<br/>Copilot account context")]
        local -. "syncs with" .-> remote
    end
    class local note
    class remote remoteNode
    style local_remote fill:#ffffff,stroke:#cbd5e1

    subgraph round_trip["4. Git round trip"]
        direction TB
        subgraph round_trip_first["Local history"]
            direction LR
            r1["Edit a file locally"] --> r2["Inspect with git status"] --> r3["Stage with git add"]
        end
        subgraph round_trip_second["Shared history"]
            direction LR
            r4["Create a local commit"] --> r5["Push to GitHub"] --> r6["Verify the same commit remotely"]
        end
        r3 --> r4
    end
    class r1,r2,r3,r4,r5,r6 model
    style round_trip fill:#ffffff,stroke:#cbd5e1
    style round_trip_first fill:#f5f3ff,stroke:#cbd5e1
    style round_trip_second fill:#f5f3ff,stroke:#cbd5e1

    subgraph git_state["5. Meaning of Git state"]
        direction LR
        st1(["Untracked"]) --> st2(["Tracked and staged"]) --> st3(["Committed locally"]) --> st4(["Pushed remotely"])
    end
    class st1,st2,st3,st4 state
    style git_state fill:#ffffff,stroke:#cbd5e1
```

The procedural guides remain the step-by-step operating layer.

[Back to the guide map](../README.md)
