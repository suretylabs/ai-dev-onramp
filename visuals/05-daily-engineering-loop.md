# 05 — Visual Daily Engineering Loop

This file shows the routine after the platform exists.

## Standard daily loop

```mermaid
flowchart TD
    A[Open repository] --> B[Read current state]
    B --> C[Sync environment]
    C --> D[Clarify today's objective]
    D --> E[Make focused changes]
    E --> F[Run validation]
    F --> G[Review diff]
    G --> H[Commit]
    H --> I[Push]
    I --> J[Update brief / state if needed]
```

## Micro-loop while working with AI

```mermaid
flowchart LR
    A[Describe change] --> B[AI suggests next step]
    B --> C[the developer executes or edits]
    C --> D[Observe result]
    D --> E[AI interprets result]
    E --> F[Next step]
```

## Validation loop

```mermaid
flowchart TD
    A[Code changes] --> B[Run formatter/lint]
    B --> C[Run type checks]
    C --> D[Run tests]
    D --> E{Pass?}
    E -->|Yes| F[Commit]
    E -->|No| G[Fix and rerun]
    G --> B
```

## Commit discipline

```mermaid
flowchart TD
    A[One meaningful change] --> B[Review diff]
    B --> C[Commit with clear message]
    C --> D[Push]
```

## Mental model of progress

```mermaid
flowchart LR
    A[Thinking] --> B[Documented plan]
    B --> C[Working code]
    C --> D[Verified code]
    D --> E[Committed history]
    E --> F[Shared remote state]
```
