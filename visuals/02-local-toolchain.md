# 02 — Visual Local Toolchain

This file explains the local machine components.

## Local toolchain stack

```mermaid
flowchart TD
    A[Windows 11]
    A --> B[PowerShell]
    A --> C[Git for Windows]
    A --> D[GitHub CLI gh]
    A --> E[VS Code]
    A --> F[uv]
    F --> G[Python 3.14]
```

## Why PowerShell matters

```mermaid
flowchart LR
    A[the developer] --> B[PowerShell]
    B --> C[Runs commands]
    C --> D[Produces inspectable output]
    D --> E[LLM can interpret exact result]
```

## Local vs remote

```mermaid
flowchart LR
    A[Local machine] <--> B[Internet / GitHub]
    A --> C[PowerShell]
    A --> D[VS Code]
    A --> E[Local repository]
    B --> F[Organization repository]
```

## Git round-trip

```mermaid
flowchart TD
    A[Edit file locally] --> B[git status]
    B --> C[git add]
    C --> D[git commit]
    D --> E[git push]
    E --> F[View same commit on GitHub]
```

## Meaning of state

```mermaid
flowchart LR
    A[Untracked] --> B[Tracked / staged]
    B --> C[Committed locally]
    C --> D[Pushed remotely]
```

## The local machine becomes trustworthy when

```mermaid
flowchart TD
    A[git works] --> B[gh auth works]
    B --> C[clone works]
    C --> D[commit works]
    D --> E[push works]
    E --> F[status is understandable]
```
