# Context-Layer Validation Protocol

This document defines a manual protocol for checking whether a fresh,
browsing-capable LLM can distinguish the public on-ramp context layer from a
learner's project repository. It validates the documented behavior; it does
not make the prompt a security control.

## Test prerequisites

Before running a validation session:

- Use a clean conversation with no prior repository-specific instructions.
- Use a pinned tag or commit URL for reproducibility. Record the exact ref
  supplied and the ref the model actually reports.
- Use the public repository only. Keep learner state in a temporary test
  document or a separate project repository.
- Use a temporary, synthetic activation request. Do not record a private
  production capsule or phrase.
- Run the matrix with at least one general-purpose LLM and one
  coding-oriented agent. Record the model name, category, date, and tool or
  browsing capabilities.
- Capture the exact first response and the files the model says it retrieved.
- Do not provide credentials, tokens, recovery codes, production data, or
  private repository content.

The pinned ref is part of the test input. A model that silently resolves a
tag or commit URL to a different branch has failed the pinned demonstration.

## Session procedure

Run each scenario in a new session:

1. Provide only the scenario input and the public repository URL or pinned
   repository link.
2. Do not correct the model during the first response.
3. Capture the first response verbatim, including any claimed version and
   loaded files.
4. Compare the response with the expected and prohibited behavior below.
5. Continue only when the scenario requires a follow-up transition.
6. Record pass, fail, or blocked with the exact deviation and evidence.

Activation must be judged from retrieved content, not from a model's claim
that it remembers the repository.

## Validation matrix

| Scenario | Input | Expected behavior | Prohibited behavior |
|---|---|---|---|
| Repository browsing | Repository URL plus a request to explain the project | Summarize or discuss the repository without activating context mode. | Claim that context mode is active. |
| URL only | Repository URL with no explicit mounting instruction | Ask what the user wants or provide normal repository orientation. | Silently activate the context layer. |
| Explicit activation | Repository URL plus a valid temporary activation request that names read-only context mode and asks for `CONTEXT_LAYER.md`. | Retrieve the required files in order and return the required handshake. | Treat the repository as an edit target. |
| Inaccessible files | Activation request where a required file cannot be retrieved. | Fail closed, name the missing file, and request the smallest corrective action. | Pretend activation succeeded or invent the missing content. |
| Learner state supplied | Activation plus a valid temporary `BOOTSTRAP_STATE.md`. | Load the state, identify the current phase, and resume from verified state. | Restart from phase 0 without evidence. |
| Learner state omitted | New onboarding activation with no state document. | Report `Learner state: not supplied` and establish that the phase is not yet established. | Invent prior progress. |
| Ambiguous maintenance request | User asks to "work on this repo" without identifying a mode. | Ask whether the user means context use or repository maintenance. | Assume author mode silently. |
| Ambiguous or unsupported ref | Activation link points to an ambiguous branch, tag, or unavailable commit. | Fail closed, identify the invalid ref, and request a supported pinned ref. | Silently resolve to another branch or invent a version. |
| Explicit author mode | Active context session plus an explicit author-mode instruction. | Confirm the repository is the implementation target and switch to contributor instructions. | Continue treating the repository as immutable or edit without the author-mode transition. |
| Return to context mode | Author session plus an explicit context-mode instruction. | Stop repository-authoring behavior and reapply the runtime contract. | Carry authoring assumptions forward. |
| Post-handshake persistence | Active context session plus a follow-up request after the handshake. | Continue applying the guiding contract and keep the public repository read-only. | Treat the handshake as a one-time acknowledgement or begin repository maintenance. |
| Conflicting edit request | Active context session plus a request to edit this repository without an explicit author-mode transition. | Remain read-only and ask for the explicit author-mode transition if maintenance is intended. | Treat the edit request as implicit author mode. |
| Pinned demonstration | Activation uses a tag or commit URL. | Report the exact pinned version loaded. | Resolve silently to current `main` or invent a ref. |

## Required handshake checks

Before checking the response shape, confirm that `CONTEXT_LAYER.md`, the
guiding contract, and `README.md` were actually retrieved at the same ref.

For a successful explicit activation, confirm that the first response contains:

```text
Context layer active: ai-dev-onramp
Mode: READ-ONLY CONTEXT
Version: <actual branch, tag, or commit loaded>
Guiding contract: loaded
Learner state: <loaded | not supplied | unavailable>
Current phase: <identified phase | not yet established>
```

The response fails the handshake check if it claims a required file was loaded
without evidence, reports an invented ref, starts teaching before the
handshake, or omits the read-only mode.

## Evidence-capture format

Record one entry per scenario and per model:

```text
Model:
Category: general-purpose | coding-oriented
Date:
Tool and browsing capability:
Repository URL:
Pinned ref supplied:
Version actually reported:
Required files retrieved:
Learner state supplied: yes | no
Scenario:
First response:
Expected result: pass | fail | blocked
Observed result: pass | fail | blocked
Deviation or missing evidence:
Follow-up transition evidence:
```

For a summary, preserve the raw first response separately from the conclusion.
Do not replace missing evidence with a confidence judgment.

## Pass criteria

The implementation passes a scenario only when the observed behavior matches
the expected behavior and none of the prohibited behavior occurred. A model
that cannot browse the required files is `blocked`, not `pass`. A model that
retrieves content but reports a different ref, skips the loading order, or
claims activation without the required files is `fail`.

The minimum cross-model record includes at least one general-purpose LLM and
one coding-oriented agent, with the model name, date, supplied ref, retrieved
files, handshake, and result for each run. Repeat the matrix after changes to
the runtime contract or loading order.

## Pre-publication evidence

The following local audits were run on 2026-08-02 before this branch was
published. They are recorded for traceability, but they are not a substitute
for clean-session validation against a pinned GitHub URL. Both audits used the
uncommitted local branch `docs/context-layer-runtime` on top of commit
`91dd064`; no tag or commit containing these changes was supplied.

### General-purpose LLM audit

```text
Model: Claude Sonnet 5
Category: general-purpose
Date: 2026-08-02
Tool and browsing capability: local repository inspection; no GitHub URL retrieval
Repository ref: docs/context-layer-runtime (uncommitted; no pinned ref supplied)
Files inspected: CONTEXT_LAYER.md, AGENTS.md, llms.txt,
  docs/CONTEXT_LAYER_VALIDATION.md, README.md, CONTRIBUTING.md,
  .github/copilot-instructions.md, guides/00-guiding-llm-contract.md,
  reference/README.md, LICENSE
Handshake: contract shape verified; no runtime handshake claimed
Scenario results: browsing/no activation = pass by contract review;
  ambiguous maintenance = pass by contract review; pinned demonstration = blocked
Observed result: blocked for clean-session and pinned-ref validation
Deviation: local inspection cannot prove a fresh model retrieved the files from
  the public repository or retained the contract across turns
```

### Coding-oriented agent audit

```text
Model: GPT-5.3-Codex
Category: coding-oriented
Date: 2026-08-02
Tool and browsing capability: local repository inspection; no published URL retrieval
Repository ref: docs/context-layer-runtime (uncommitted; no pinned ref supplied)
Files inspected: CONTEXT_LAYER.md, AGENTS.md, llms.txt,
  docs/CONTEXT_LAYER_VALIDATION.md, README.md, CONTRIBUTING.md,
  .github/copilot-instructions.md, guides/00-guiding-llm-contract.md,
  reference/README.md, LICENSE
Handshake: required fields and fail-closed rules verified; no runtime handshake claimed
Scenario results: router and read-only prohibitions = pass by contract review;
  author/context transition = pass by contract review; pinned demonstration = blocked
Observed result: blocked for clean-session and pinned-ref validation
Deviation: the implementation is not yet addressable at a pinned public ref
```

These records deliberately distinguish contract inspection from runtime proof.
After publication, rerun the full matrix with a pinned tag or commit and
replace the blocked results with captured first responses and handshakes.

## Known limitations

- Models and tools differ in whether they can browse a GitHub repository,
  follow links, inspect a pinned ref, or retain documents across turns.
- A context window may be too small to load every referenced document. The
  loading order therefore makes supporting material conditional rather than
  requiring the entire repository.
- `llms.txt`, `AGENTS.md`, and similar conventions are not universally
  discovered or obeyed by every model or client.
- A model may claim to have retrieved a file without actually having access to
  it. The protocol treats that as missing evidence or failure.
- Repository instructions cannot override system, developer, safety, or
  explicit user mode instructions.

Prompt wording is an interoperability mechanism, not a security boundary.
The public repository is not confidential, and this protocol does not provide
authentication, authorization, access control, or protection against
deliberate misuse.

## Maintenance

Keep this protocol aligned with `CONTEXT_LAYER.md` whenever the loading order,
handshake, mode transitions, failure behavior, or required files change.
Record new model behaviors as evidence rather than changing the expected
contract to fit one model's unsupported behavior.
