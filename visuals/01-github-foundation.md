# 01 — Visual GitHub Foundation

This file explains why GitHub comes first.

## Identity model

```mermaid
flowchart TD
    A[the developer the person] --> B[Personal GitHub account]
    B --> C[Member / owner of business organization]
    C --> D[Organization-owned repositories]
    B --> E[Signs into gh CLI]
    B --> F[Signs into VS Code / Copilot]
```

## Ownership model

```mermaid
flowchart LR
    A[the developer personal account] --> B[Authentication]
    C[Business organization] --> D[Repository ownership]
    C --> E[Copilot policy / seat management]
    C --> F[Access control and future collaboration]
```

## Why this order helps

```mermaid
flowchart TD
    A[Create account] --> B[Secure account]
    B --> C[Create organization]
    C --> D[Create private repository]
    D --> E[Install local tools]
    E --> F[Clone known remote]
```

Because of that sequence:

- the remote location exists first;
- the local machine has something concrete to connect to;
- Git becomes easier to understand because the remote is real, not theoretical.

## Lightweight protection model

```mermaid
flowchart TD
    A[Private repository]
    A --> B[main branch]
    B --> C[No force-push]
    B --> D[No branch deletion]
    B --> E[Small reversible commits]
    B --> F[Review before merge when practical]
    B --> G[No secrets or production data in repo]
```

## Mental model: GitHub is not just backup

```mermaid
flowchart LR
    A[GitHub] --> B[Identity]
    A --> C[Collaboration]
    A --> D[Copilot context]
    A --> E[Remote source of truth]
    A --> F[Future automation and policy]
```
