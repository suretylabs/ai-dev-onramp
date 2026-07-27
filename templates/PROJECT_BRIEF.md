# Project Brief

> Start by preserving the operator's explanation of the project in their own terms. Translate into modern technical language only after the behavior is understood. Mark unknowns explicitly; do not complete sections by invention.

## Project explanation

Describe what is being built, why it matters, and how it relates to the current business process. Include relevant historical or Microsoft-stack terminology when that is how the existing system is understood.

## Current workflow and friction

Describe the present MSSQL, PDF, Microsoft-tooling, manual, or system workflow. Identify where time, risk, duplication, opacity, or maintenance burden occurs.

## Problem

State the business problem in operational terms, without prematurely prescribing the Python implementation.

## User and decision

- Who uses the result?
- What decision or action does it support?
- What is the current manual or system process?

## First useful vertical slice

Define the smallest result that has real value.

## Inputs

| Input | Source | Format | Access method | Sensitivity | Expected volume |
|---|---|---|---|---|---|
| | | | | | |

## Outputs

| Output | Format | Consumer | Acceptance criteria |
|---|---|---|---|
| | | | |

## Transformation rules

1. 

## Evidence and audit requirements

- What must be traceable to source?
- Are page, row, query, timestamp, hash, or version references required?
- What constitutes a reviewable exception?

## Security constraints

- Authentication method:
- Read-only requirement:
- Prohibited data in logs/chat/source control:
- Secret-storage method:

## Technical target

- Python 3.14
- uv
- Polars
- Parquet
- DuckDB
- MSSQL integration, if required
- PDF integration, if required
- Ruff
- Pyright
- pytest

## Out of scope for the first slice

- 

## Acceptance criteria

1. 

## Validation plan

- Unit tests:
- Integration test:
- Manual proof:
- Data reconciliation:

## Open decisions

| Decision | Options | Evidence needed | Owner |
|---|---|---|---|
| | | | |
