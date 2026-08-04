# Consultant Process-Capture Lane

An AI-guided lane for turning a real business process into one portable
Markdown artifact a new hire can attach to an LLM session as operating
context.

This is **not** the developer on-ramp. The developer track (root
[`README.md`](../README.md), [`guides/`](../guides/),
[`visuals/`](../visuals/), [`templates/`](../templates/)) teaches someone how
to set up a modern AI development environment. This lane teaches a consultant,
trainer, manager, or other facilitator how to sit with a veteran operator,
elicit a repeatable process — including the pitfalls the veteran rarely writes
down — and produce a structured `PROCESS_CAPTURE.md` that an LLM can use to
walk a new person through that specific process in that specific environment.

```text
Any repeatable business process
  -> Scope with the owner
  -> Observe or interview the SME
  -> Draft PROCESS_CAPTURE.md without inventing steps
  -> Validate and get SME sign-off
  -> Hand the artifact to a new hire's LLM session
```

Examples of in-scope processes: accounts payable, cheques arriving in the
mail, opening a new customer folder, month-end close steps, claim intake,
renewal packet assembly — literally any process a person can demonstrate or
walk through. The lane is process-agnostic; the artifact is always the same
shape.

## Who this lane is for

- A **consultant** (internal or external) facilitating process capture.
- A **trainer, manager, or ops lead** shadowing a veteran before turnover.
- An **LLM** acting as the session guide under
  [`guides/00-consultant-lane-contract.md`](guides/00-consultant-lane-contract.md).

The facilitator does **not** need to be a software developer. They need
permission to observe or interview, discipline about not inventing missing
steps, and a place to store the finished artifact for the people who will use
it.

## Start here

| Layer | Path | Purpose |
|---|---|---|
| Guides | [`guides/`](guides/) | Procedural sequence: contract, scope, elicitation, draft, validate/handoff. |
| Templates | [`templates/`](templates/) | Blank `PROCESS_CAPTURE.md` plus one fully synthetic completed example. |
| Visual | [`visuals/`](visuals/) | One Mermaid flow of the capture-to-attachment journey. |

## Guide sequence

| Phase | Guide | Outcome |
|---|---|---|
| 0 | [Consultant-lane contract](guides/00-consultant-lane-contract.md) | LLM and facilitator behavior: ask, do not invent, gate on SME sign-off. |
| 1 | [Prepare and scope](guides/01-prepare-and-scope.md) | One named process with explicit start/end, owner, SME, and capture goal. |
| 2 | [Elicitation and shadowing](guides/02-elicitation-and-shadowing.md) | Observed or interviewed evidence, including pitfalls and exceptions. |
| 3 | [Drafting the process capture](guides/03-drafting-the-process-capture.md) | Structured draft with gaps marked, not filled by inference. |
| 4 | [Validation and handoff](guides/04-validation-and-handoff.md) | SME-signed artifact ready to attach to a new hire's LLM session. |

## The output artifact

The durable product of this lane is a filled
[`templates/PROCESS_CAPTURE.md`](templates/PROCESS_CAPTURE.md).

That file is designed to be attached to an LLM chat the same way this
repository's own context layer is mounted: as **read-only operating context**
for how to perform one process correctly. For attachment mechanics used by
this repository itself, see the root
[Getting the context layer into an AI chat](../README.md#getting-the-context-layer-into-an-ai-chat)
section and [`CONTEXT_LAYER.md`](../CONTEXT_LAYER.md). A finished process
capture is a *different* document with a *similar* attach pattern: supply the
complete file, tell the model it is the governing procedure for this process,
and require it not to invent steps the file does not contain.

See the synthetic example:
[`templates/PROCESS_CAPTURE.example.md`](templates/PROCESS_CAPTURE.example.md).

## Lane versus track

| Concept | Meaning in this repository |
|---|---|
| **Track** | Same developer-onboarding purpose; different OS, language, or data stack. See root [`CONTRIBUTING.md`](../CONTRIBUTING.md). |
| **Lane** | Different audience and output, reusing the guided-elicitation and durable-artifact mechanism. This directory is a lane. |

Do not fold this material into `guides/00`–`09`. Do not renumber the developer
sequence to make room for it.

## Governing principles for this lane

- Capture one process at a time with an explicit start and end.
- Prefer observation of real work; interview when observation is not possible.
- Preserve the SME's own terms before standardizing vocabulary.
- Distinguish what the SME said from what anyone is inferring.
- Never invent a step, exception, system name, or pitfall to make the draft
  look complete.
- Mark unknowns and open questions explicitly.
- Gate completion on SME sign-off, not on document length.
- Never put credentials, recovery codes, account numbers, or production
  secrets into the artifact or the chat.
- Keep public or shareable examples synthetic.

## Status

This lane is part of the public on-ramp repository. Content is generic and
public-safe. Real client process captures belong in the client's own
repository or knowledge store, not in this public tree.

## Parent repository

- Root entry: [`../README.md`](../README.md)
- Contributing / lane vs track: [`../CONTRIBUTING.md`](../CONTRIBUTING.md)
- Developer guiding contract (related pattern, different audience):
  [`../guides/00-guiding-llm-contract.md`](../guides/00-guiding-llm-contract.md)
