# 06 — Visual Gating and State

This file explains why gates and a running state document exist.

## Gate model

```mermaid
flowchart TD
    A[Do work] --> B[Collect evidence]
    B --> C[Evaluate gate]
    C --> D{Passed?}
    D -->|Yes| E[Record success]
    E --> F[Offer next paths]
    D -->|No| G[Record blocker]
    G --> H[Choose troubleshoot or pause]
```

## Two types of gating

```mermaid
flowchart LR
    A[Technical gate] --> A1[Did the thing actually work?]
    B[Choice gate] --> B1[Which reasonable path should the developer take next?]
```

## Example checkpoint pattern

```mermaid
flowchart TD
    A[Phase complete] --> B[Summarize verified state]
    B --> C[Update BOOTSTRAP_STATE.md]
    C --> D[Present options]
    D --> E[Recommend path]
    E --> F[the developer chooses]
```

## Running state document

```mermaid
flowchart TD
    A[BOOTSTRAP_STATE.md] --> B[Current phase]
    A --> C[Completed gates]
    A --> D[Evidence]
    A --> E[Open decisions]
    A --> F[Blockers]
    A --> G[Resume point]
    A --> H[Next recommended action]
```

## Why this helps

```mermaid
flowchart LR
    A[Without state tracking] --> B[Every new AI session reconstructs reality]
    C[With state tracking] --> D[AI resumes from durable facts]
```

## Pause / resume model

```mermaid
flowchart TD
    A[Need to stop] --> B[Record actual current state]
    B --> C[Record last successful step]
    C --> D[Record blocker or next step]
    D --> E[Resume later without re-discovery]
```
