# 06 — Visual Gating and State

This is the mental-model companion for technical gates, choice gates, and the durable running-state document.

```mermaid
flowchart TB
    classDef primary fill:#eff6ff,stroke:#2563eb,color:#111827,stroke-width:1.5px
    classDef checkpoint fill:#f5f3ff,stroke:#7c3aed,color:#111827,stroke-width:1.5px
    classDef state fill:#fffbeb,stroke:#b45309,color:#111827,stroke-width:1.5px
    classDef choice fill:#ecfeff,stroke:#0f766e,color:#111827,stroke-width:1.5px
    classDef danger fill:#fef2f2,stroke:#dc2626,color:#111827,stroke-width:1.5px
    classDef success fill:#f0fdf4,stroke:#15803d,color:#111827,stroke-width:1.5px

    subgraph gate_model["1. Gate model"]
        direction TB
        subgraph gate_first["Work and evaluate"]
            direction LR
            g1["1. Do the work"] --> g2["2. Collect evidence"] --> g3["3. Evaluate the gate"]
        end
        subgraph gate_second["Record and choose"]
            direction LR
            g4["4. Record success or the blocker"] --> g5["5. Offer legitimate next paths"] --> g6["6. Continue, troubleshoot, or pause"]
        end
        g3 --> g4
    end
    class g1,g2,g3,g4,g5,g6 primary
    style gate_model fill:#ffffff,stroke:#cbd5e1
    style gate_first fill:#eff6ff,stroke:#cbd5e1
    style gate_second fill:#eff6ff,stroke:#cbd5e1

    subgraph gate_types["2. Two types of gating"]
        direction LR
        technical["Technical gate<br/><br/>Did the thing actually work?<br/><br/>Do output, screenshots, files, and observed<br/>state prove the prerequisite is satisfied?"]
        decision["Choice gate<br/><br/>Now that this point is reached, should the<br/>developer continue, deepen the current topic,<br/>troubleshoot, or pause?"]
    end
    class technical primary
    class decision choice
    technical --> decision
    style gate_types fill:#ffffff,stroke:#cbd5e1

    subgraph checkpoint["3. Checkpoint pattern"]
        direction TB
        subgraph checkpoint_first["Summarize and record"]
            direction LR
            c1["1. Summarize verified state"] --> c2["2. Update BOOTSTRAP_STATE.md"] --> c3["3. State whether the gate passed"]
        end
        subgraph checkpoint_second["Offer and choose"]
            direction LR
            c4["4. Present reasonable options"] --> c5["5. Recommend a path when evidence favors one"] --> c6["6. Developer chooses"]
        end
        c3 --> c4
    end
    class c1,c2,c3,c4,c5,c6 checkpoint
    style checkpoint fill:#ffffff,stroke:#cbd5e1
    style checkpoint_first fill:#f5f3ff,stroke:#cbd5e1
    style checkpoint_second fill:#f5f3ff,stroke:#cbd5e1

    subgraph running_state["4. What the running state document contains"]
        direction TB
        subgraph running_state_first["Current operating context"]
            direction LR
            r1["1. Current phase"] --> r2["2. Completed gates and evidence"] --> r3["3. Machine and tool state"] --> r4["4. Open decisions and deferred work"]
        end
        subgraph running_state_second["Recovery context"]
            direction LR
            r5["5. Blockers and evidence needed"] --> r6["6. Last successful command or GUI state"] --> r7["7. Selected path and resume point"] --> r8["8. Next recommended action"]
        end
        r4 --> r5
    end
    class r1,r2,r3,r4,r5,r6,r7,r8 state
    style running_state fill:#ffffff,stroke:#cbd5e1
    style running_state_first fill:#fffbeb,stroke:#cbd5e1
    style running_state_second fill:#fffbeb,stroke:#cbd5e1

    subgraph pause_resume["5. Pause and resume"]
        direction LR
        without_state["Without durable state<br/><br/>Every new AI session must reconstruct reality<br/>and may repeat work or invent assumptions."]
        with_state["With durable state<br/><br/>The AI resumes from verified facts, and the<br/>developer can stop and restart without losing<br/>the exact operating context."]
    end
    class without_state danger
    class with_state success
    style pause_resume fill:#ffffff,stroke:#cbd5e1
```

The procedural guides remain the step-by-step operating layer.

[Back to the guide map](../README.md)
