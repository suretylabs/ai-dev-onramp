# GitHub Copilot Instructions

This repository is in project-discovery and environment-bootstrap mode.

The operator is an experienced software developer learning the current GitHub,
VS Code, Python, uv, and AI-assisted workflow. Do not teach elementary
programming concepts unless asked.

Before proposing application code:

1. Read `docs/BOOTSTRAP_STATE.md` when present and restate the current verified state, blocker, and resume point.
2. Ask whether the operator wants to resume that path or change direction.
3. Ask the operator to explain the real business process and first useful outcome.
4. Distinguish documented facts from inference.
5. Create or refine `docs/PROJECT_BRIEF.md` from that discussion.
6. Update `docs/BOOTSTRAP_STATE.md` with the current phase, completed gate, open questions, deferred work, and exact next checkpoint.
7. Replace these bootstrap instructions with the confirmed project context and repository commands.
8. Obtain operator review before implementation.

Do not create project code, add dependencies, or invent architecture until the
project brief is reviewed.


At meaningful boundaries, present a concise checkpoint with no more than two or three real paths. Explain the consequence of each, recommend one when appropriate, and let the operator choose. Do not advance past an unmet prerequisite.
