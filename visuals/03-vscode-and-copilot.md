# 03 — Visual VS Code and Copilot

This file explains the coding workspace.

## What VS Code is

```mermaid
flowchart TD
    A[Windows folder] --> B[Open in VS Code]
    B --> C[Workspace]
    C --> D[Editor]
    C --> E[Terminal]
    C --> F[Extensions]
    C --> G[Source control view]
    C --> H[Copilot]
```

## Workspace mental model

```mermaid
flowchart LR
    A[Folder in Windows] --> B[Repository to Git]
    B --> C[Workspace in VS Code]
    C --> D[Codebase to the developer]
```

One folder can serve several roles.

## Copilot positioning

```mermaid
flowchart TD
    A[the developer] --> B[Explains project]
    B --> C[Copilot]
    C --> D[Asks clarifying questions]
    C --> E[Helps generate code]
    C --> F[Helps explain tools]
    C --> G[Helps inspect errors]
    C --> H[Helps summarize next choices]
```

## Correct first use of Copilot

```mermaid
flowchart TD
    A[Open repository] --> B[Copilot reads bootstrap docs]
    B --> C[Copilot restates understanding]
    C --> D[the developer corrects or adds context]
    D --> E[Project brief becomes durable]
    E --> F[Only then start implementation]
```

## What Copilot should not do first

```mermaid
flowchart TD
    A[Do not immediately scaffold a random app]
    A --> B[Do not assume requirements]
    A --> C[Do not overwrite structure without agreement]
    A --> D[Do not confuse inference with fact]
```

## Files that hold shared understanding

```mermaid
flowchart TD
    A[docs/PROJECT_BRIEF.md]
    B[docs/BOOTSTRAP_STATE.md]
    C[.github/copilot-instructions.md]
    D[README.md]

    A --> E[What the project is]
    B --> F[Where setup currently stands]
    C --> G[How the AI should behave]
    D --> H[How to use the repository]
```
