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
- Record the access path attempted and whether access was achieved as direct
  repository retrieval, manual file supply, unavailable, or not applicable.
- Capture the exact first response and the files the model says it retrieved.
- For manual file supply, provide complete contents for
  `CONTEXT_LAYER.md`, the guiding contract, and `README.md` from the same ref
  in the declared order. Record them as supplied, not retrieved.
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

For the manual file-supply path, provide the source URL and complete raw
contents for each required file one at a time in the declared order, after an
explicit activation request that identifies the repository as read-only
context and says the files will be supplied. Do not provide a summary or tell
the model the expected handshake. Capture every interim response and verify
that it is only a receipt acknowledgement without teaching, commands, or a
success handshake. Capture the first successful activation response after all
required files have been supplied as the handshake candidate.

Activation must be judged from retrieved content, not from a model's claim
that it remembers the repository. Supplied content must be judged as supplied,
not as direct URL retrieval.

## Validation matrix

| Scenario | Input | Expected behavior | Prohibited behavior |
|---|---|---|---|
| Repository browsing | Repository URL plus a request only to explain or summarize the project | Summarize or discuss the repository without activating context mode. | Claim that context mode is active. |
| URL only | Repository URL with no guide, setup, or mounting instruction | Ask what the user wants or provide normal repository orientation. | Silently activate the context layer. |
| Soft guide activation | Repository URL plus realistic guide or setup intent, such as asking the model to use the link as a guide for getting the computer ready to develop with AI | Treat the request as activation, retrieve the required files in order, and return the required handshake. | Stay in pure browse mode, treat the repository as an edit target, or skip the handshake. |
| Explicit activation | Repository URL plus a valid temporary activation request that names read-only context mode and asks for `CONTEXT_LAYER.md`. | Retrieve the required files in order and return the required handshake. | Treat the repository as an edit target. |
| Unsupported client | Explicit activation in a client that cannot open public GitHub files. | Fail closed, explain that repository access is unavailable, and identify the manual file-supply path. | Pretend the URL was retrieved or tell the learner that activation succeeded. |
| Manual file supply | An explicit manual activation request is followed by complete raw contents and source URLs for the three required files from one declared ref, in order. | Check the supplied identities and visibly complete content, record the source ref as user-attested, then return the handshake with `Access path: MANUAL FILE SUPPLY`; do not claim direct retrieval. | Treat pasted content as independently fetched or activate before all three files are complete. |
| Incomplete or mixed-ref file supply | One required file is truncated, omitted, or declares a different ref. | Fail closed, name the missing or mismatched dependency, and request the complete file from the same declared ref. | Combine files from different refs or summarize missing content. |
| Inaccessible files | Activation request where a required file cannot be retrieved. | Fail closed, name the missing file, and request access or complete same-ref file supply. | Pretend activation succeeded or invent the missing content. |
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
guiding contract, and `README.md` were directly retrieved or completely
supplied at the same declared ref. Treat the ref as directly verified for the
direct path and user-attested for the manual path.

For direct repository access, confirm that the first response contains the
handshake shape below. For manual file supply, confirm that the final
handshake candidate after the last required file contains the same shape:

```text
Context layer active: ai-dev-onramp
Mode: READ-ONLY CONTEXT
Version: <actual branch, tag, or commit loaded>
Access path: <DIRECT REPOSITORY RETRIEVAL | MANUAL FILE SUPPLY>
Guiding contract: loaded
Learner state: <loaded | not supplied | unavailable>
Current phase: <identified phase | not yet established>
```

The manual path must report `MANUAL FILE SUPPLY` and identify the `Version` as
a user-attested source ref. A direct-access run must not report manual supply,
and neither path may claim direct retrieval without evidence.

The response fails the handshake check if it claims a required file was loaded
without evidence, reports an invented ref, misstates the access path, starts
teaching before the handshake, or omits the read-only mode.

## Evidence-capture format

Record one entry per scenario and per model:

```text
Model:
Category: general-purpose | coding-oriented
Date:
Tool and browsing capability:
Access path attempted: direct repository retrieval | manual file supply | none
Access path achieved: direct repository retrieval | manual file supply | unavailable | not applicable
Repository URL:
Pinned ref supplied:
Ref status: directly verified | user-attested | unavailable | not applicable
Version actually reported:
Required files retrieved or supplied:
Learner state supplied: yes | no
Scenario:
First response:
Interim responses (manual path, in order):
Final handshake candidate:
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
that cannot browse the required files is `blocked` for the direct-access
activation scenario. Soft guide activation passes when realistic guide or
setup intent plus a repository URL produces the required handshake and does
not treat the repository as an edit target. The unsupported-client scenario
passes when the model fails closed and identifies the manual fallback. The
manual file-supply scenario passes when complete content from the same
declared ref is supplied in order, the ref is reported as user-attested, and
the model reports that access path honestly. A model that reports a different
declared ref, skips the loading order, or claims activation without the
required files is `fail`.

The manual file-supply path can demonstrate correct contract application after
the learner provides the files, but it does not prove that the client can
retrieve a public GitHub URL. Record those as separate access paths rather
than treating one as evidence for the other.

The minimum cross-model record includes at least one general-purpose LLM and
one coding-oriented agent, with the model name, date, access path, supplied
ref, retrieved or supplied files, handshake, and result for each run. Repeat
the matrix after changes to the runtime contract or loading order.

## Clean-session evidence

### General-purpose soft guide activation

Captured from a fresh ChatGPT session against the public repository after
PR #14 landed on `main`.

```text
Model: ChatGPT
Category: general-purpose
Date: 2026-08-03
Tool and browsing capability: public GitHub browsing / file retrieval
Access path attempted: direct repository retrieval
Access path achieved: direct repository retrieval
Repository URL: https://github.com/suretylabs/ai-dev-onramp
Pinned ref supplied: none
Ref status: directly verified by model as commit 0408e936d78bad32d1b606957a2bdaec6bfca995
Version actually reported: commit 0408e936d78bad32d1b606957a2bdaec6bfca995
Required files retrieved or supplied: CONTEXT_LAYER.md;
  guides/00-guiding-llm-contract.md; README.md
Learner state supplied: no
Scenario: Soft guide activation
User input:
  https://github.com/suretylabs/ai-dev-onramp
  this link should help you serve as my guide to understanding and getting my
  computer ready to develop with AI
First response notes: model initially inspected repository metadata and README,
  recognized the context-layer contract, then reloaded required files from one
  resolved commit in order
Final handshake candidate:
  Context layer active: ai-dev-onramp
  Mode: READ-ONLY CONTEXT
  Version: commit 0408e936d78bad32d1b606957a2bdaec6bfca995
  Access path: DIRECT REPOSITORY RETRIEVAL
  Guiding contract: loaded
  Learner state: not supplied
  Current phase: not yet established
Expected result: pass under the soft-guide activation rule
Observed result: pass
Deviation or missing evidence: model briefly used inspect/review framing before
  the handshake; it also described the resolved main commit as pinned even
  though the user did not supply a pin. Handshake fields and required files were
  otherwise correct.
Follow-up transition evidence: not required for this scenario
```

This run is the primary general-purpose proof that realistic beginner wording
can activate the context layer and produce the required handshake.

### Earlier local contract audits

The following local audits were run on 2026-08-02 before the runtime branch was
published. They remain as traceability only. They are not clean-session proof.

```text
Model: Claude Sonnet 5
Category: general-purpose
Date: 2026-08-02
Tool and browsing capability: local repository inspection; no GitHub URL retrieval
Repository ref: docs/context-layer-runtime (uncommitted; no pinned ref supplied)
Observed result: blocked for clean-session and pinned-ref validation
```

```text
Model: GPT-5.3-Codex
Category: coding-oriented
Date: 2026-08-02
Tool and browsing capability: local repository inspection; no published URL retrieval
Repository ref: docs/context-layer-runtime (uncommitted; no pinned ref supplied)
Observed result: blocked for clean-session and pinned-ref validation
```

### Coding-oriented clean-session status

A separate clean coding-oriented agent session should still be recorded when
available. Until then, do not treat the local GPT-5.3-Codex contract audit as
runtime proof. The ChatGPT soft-guide run satisfies the general-purpose
clean-session requirement and justified loosening the activation boundary.

## Known limitations

- Models and tools differ in whether they can browse a GitHub repository,
  follow links, inspect a pinned ref, or retain documents across turns.
- A client that cannot open GitHub URLs may still support the manual file-supply
  path, but that path requires the learner to copy complete files from one
  ref and does not establish direct repository retrieval.
- Manual file supply cannot independently prove that pasted bytes exactly
  match the cited URL; source identity and completeness are user-attested.
  Record that limitation instead of treating the fallback as an integrity or
  security control.
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
