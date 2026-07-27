# 01 — Visual GitHub Foundation

This is the mental-model companion for GitHub identity, organization ownership, repositories, and lightweight protections.

```mermaid
flowchart TB
    classDef primary fill:#eff6ff,stroke:#2563eb,color:#111827,stroke-width:1.5px
    classDef sequenceNode fill:#f5f3ff,stroke:#7c3aed,color:#111827,stroke-width:1.5px
    classDef protection fill:#f0fdf4,stroke:#15803d,color:#111827,stroke-width:1.5px
    classDef context fill:#ecfeff,stroke:#0f766e,color:#111827,stroke-width:1.5px

    subgraph ownership["1. Identity and ownership"]
        direction LR
        account["Personal GitHub account<br/><br/>Authenticates the human developer.<br/>Holds verified email, recovery methods,<br/>2FA or passkeys, and the sign-in used by<br/>gh, VS Code, and Copilot."]
        organization["Business GitHub organization<br/><br/>Owns repositories, controls access, and<br/>becomes the durable home for collaboration,<br/>future automation, and organization-managed<br/>Copilot policy."]
        account -->|"authenticates and operates"| organization
    end
    class account,organization primary
    style ownership fill:#ffffff,stroke:#cbd5e1

    subgraph sequence["2. GitHub-first sequence"]
        direction TB
        subgraph sequence_first["Identity and remote"]
            direction LR
            s1["1. Create account"] --> s2["2. Secure account"] --> s3["3. Create organization"]
        end
        subgraph sequence_second["Repository and local connection"]
            direction LR
            s4["4. Create private repository"] --> s5["5. Install local tools"] --> s6["6. Clone the known remote"]
        end
        s3 --> s4
    end
    class s1,s2,s3,s4,s5,s6 sequenceNode
    style sequence fill:#ffffff,stroke:#cbd5e1
    style sequence_first fill:#f5f3ff,stroke:#cbd5e1
    style sequence_second fill:#f5f3ff,stroke:#cbd5e1

    subgraph protections["3. Lightweight repository protections"]
        direction TB
        subgraph protection_row_one["Default posture"]
            direction LR
            p1["Private repository by default"] --> p2["main is the default branch"]
            p3["No force-pushing main"] --> p4["No deleting main"]
        end
        subgraph protection_row_two["Change discipline"]
            direction LR
            p5["Small reversible commits"] --> p6["Review diffs before merge when practical"]
            p7["Never commit secrets or production data"] --> p8["Add heavier controls only when risk requires them"]
        end
    end
    class p1,p2,p3,p4,p5,p6,p7,p8 protection
    style protections fill:#ffffff,stroke:#cbd5e1
    style protection_row_one fill:#f0fdf4,stroke:#cbd5e1
    style protection_row_two fill:#f0fdf4,stroke:#cbd5e1

    subgraph github_role["4. GitHub is more than remote backup"]
        direction TB
        subgraph github_role_first["Identity and collaboration"]
            direction LR
            g1["1. Identity"] --> g2["2. Organization ownership"] --> g3["3. Collaboration"]
        end
        subgraph github_role_second["Durable context"]
            direction LR
            g4["4. Copilot account context"] --> g5["5. Remote source of truth"] --> g6["6. Future automation and policy"]
        end
        g3 --> g4
    end
    class g1,g2,g3,g4,g5,g6 context
    style github_role fill:#ffffff,stroke:#cbd5e1
    style github_role_first fill:#ecfeff,stroke:#cbd5e1
    style github_role_second fill:#ecfeff,stroke:#cbd5e1
```

The procedural guides remain the step-by-step operating layer.

[Back to the guide map](../README.md)
