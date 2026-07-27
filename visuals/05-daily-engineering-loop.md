# 05 — Visual Daily Engineering Loop

This is the mental-model companion for the normal inspect, change, validate, commit, and push cycle.

Diagram legend: blue = daily-loop step, teal = AI micro-loop step, amber diamond = validation gate, green stadium = state/outcome, dashed = optional or loop-back path. See [visuals/README.md](README.md#reading-these-diagrams) for the full shape vocabulary.

```mermaid
flowchart TB
    classDef primary fill:#eff6ff,stroke:#2563eb,color:#111827,stroke-width:1.5px
    classDef ai fill:#ecfeff,stroke:#0f766e,color:#111827,stroke-width:1.5px
    classDef validation fill:#fffbeb,stroke:#b45309,color:#111827,stroke-width:1.5px
    classDef progress fill:#f0fdf4,stroke:#15803d,color:#111827,stroke-width:1.5px
    classDef gate fill:#fef3c7,stroke:#d97706,color:#111827,stroke-width:1.5px
    classDef outcome fill:#f0fdf4,stroke:#15803d,color:#111827,stroke-width:1.5px

    subgraph daily["1. Standard daily loop"]
        direction TB
        subgraph daily_first["Orient and change"]
            direction LR
            d1["Open the repository"] --> d2["Read current state"] --> d3["Sync the environment"] --> d4["Clarify today's objective"] --> d5["Make focused changes"]
        end
        subgraph daily_second["Validate and share"]
            direction LR
            d6["Run validation"] --> d7["Review the diff"] --> d8["Commit"] --> d9["Push"]
        end
        d5 --> d6
        d9 -.->|"if needed"| d10["Update brief or state"]
    end
    class d1,d2,d3,d4,d5,d6,d7,d8,d9,d10 primary
    style daily fill:#ffffff,stroke:#cbd5e1
    style daily_first fill:#eff6ff,stroke:#cbd5e1
    style daily_second fill:#eff6ff,stroke:#cbd5e1

    subgraph micro["2. Micro-loop while working with AI"]
        direction TB
        subgraph micro_first["Describe and execute"]
            direction LR
            m1["Describe the change"] --> m2["AI suggests the next step"] --> m3["Developer executes or edits"]
        end
        subgraph micro_second["Observe and decide"]
            direction LR
            m4["Observe the actual result"] --> m5["AI interprets the evidence"] --> m6["Choose the next step"]
        end
        m3 --> m4
    end
    class m1,m2,m3,m4,m5,m6 ai
    style micro fill:#ffffff,stroke:#cbd5e1
    style micro_first fill:#ecfeff,stroke:#cbd5e1
    style micro_second fill:#ecfeff,stroke:#cbd5e1

    subgraph validation_loop["3. Validation loop"]
        direction TB
        subgraph validation_first["Quality checks"]
            direction LR
            v1["Code changes"] --> v2["Run formatting and lint"] --> v3["Run type checks"] --> v4["Run tests"]
        end
        v4 --> v4g{"All checks pass?"}
        v4g -->|"pass"| v6(["Commit"])
        v4g -->|"fail"| v5["Fix and rerun"]
        v5 -.-> v2
    end
    class v1,v2,v3,v4,v5 validation
    class v4g gate
    class v6 outcome
    style validation_loop fill:#ffffff,stroke:#cbd5e1
    style validation_first fill:#fffbeb,stroke:#cbd5e1

    subgraph progress_model["4. Progress model"]
        direction TB
        subgraph progress_first["From thought to verified code"]
            direction LR
            p1(["Thinking"]) --> p2(["Documented plan"]) --> p3(["Working code"]) --> p4(["Verified code"])
        end
        subgraph progress_second["From local to shared state"]
            direction LR
            p5(["Committed history"]) --> p6(["Shared remote state"])
        end
        p4 --> p5
    end
    class p1,p2,p3,p4,p5,p6 progress
    style progress_model fill:#ffffff,stroke:#cbd5e1
    style progress_first fill:#f0fdf4,stroke:#cbd5e1
    style progress_second fill:#f0fdf4,stroke:#cbd5e1
```

The procedural guides remain the step-by-step operating layer.

[Back to the guide map](../README.md)
