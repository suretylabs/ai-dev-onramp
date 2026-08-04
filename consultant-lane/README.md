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
down — **or normalize existing process evidence** into a structured
`PROCESS_CAPTURE.md` that an LLM can use to walk a new person through that
specific process in that specific environment.

```text
Any repeatable business process
  -> Scope with the owner
  -> Guided elicitation OR existing evidence dump
  -> Normalize evidence without inventing procedure
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
permission to observe, interview, or use existing evidence under the
organization's data-handling rules; discipline about not inventing missing
steps; and a place to store the finished artifact for the people who will use
it.

## Activate this lane in an AI chat

Start with this lane's own runtime entrypoint:
[`CONTEXT_LAYER.md`](CONTEXT_LAYER.md). It selects a **read-only consultant
process-capture context**. Do not use the root
[`../CONTEXT_LAYER.md`](../CONTEXT_LAYER.md) for this job; that entrypoint
activates the separate developer on-ramp.

Send an explicit request such as:

```text
Use the Consultant Process-Capture Lane in suretylabs/ai-dev-onramp as
read-only guidance for this conversation.

I am a consultant preparing to capture one business process with an SME.
Load consultant-lane/CONTEXT_LAYER.md first. Act as a process-capture
facilitator, not as a repository reviewer or author.

Do not invent procedure. Preserve supplied evidence, identify unknowns and
contradictions, and require SME validation before treating the capture as
complete.
```

The runtime entrypoint defines direct repository access, manual file supply,
the required loading order, activation handshake, and failure behavior. Do
not begin the capture until the AI returns its consultant-lane activation
handshake.

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
| 2 | [Elicitation and shadowing](guides/02-elicitation-and-shadowing.md) | Guided elicitation or existing-evidence normalization, including pitfalls, exceptions, contradictions, and gaps. |
| 3 | [Drafting the process capture](guides/03-drafting-the-process-capture.md) | Structured draft with gaps marked, not filled by inference. |
| 4 | [Validation and handoff](guides/04-validation-and-handoff.md) | SME-signed artifact ready to attach to a new hire's LLM session. |

## Two Phase 2 entry paths

Both entry paths produce **candidate evidence**, not signed procedure. They
converge before the existing Phase 3 drafting and Phase 4 validation gates.

| Entry path | Use when | Required result |
|---|---|---|
| Guided elicitation | The facilitator can observe work, run a live walkthrough, or interview an SME. | Source-tagged notes from the person doing or explaining the process. |
| Existing evidence dump | The facilitator has a transcript, voice-to-text output, observation notes, checklist/SOP, sanitized screenshot/document excerpt, or a mixture. | A temporary evidence summary with candidate facts, contradictions, unknowns, targeted SME questions, and a **draft** capture. |

The raw evidence remains separately retained in an approved client location.
It is not embedded wholesale in `PROCESS_CAPTURE.md`, and a detailed source
does not become authoritative procedure merely because it is detailed.

## The output artifact

The durable product of this lane is a filled
[`templates/PROCESS_CAPTURE.md`](templates/PROCESS_CAPTURE.md).

The canonical signed artifact records lightweight provenance that points back
to separately retained source evidence. It is designed to guide an LLM chat
as **read-only operating context** for how to perform one process correctly.
If the canonical file contains names, internal locations, or other data not
approved for chat, attach a complete **chat-safe session copy** instead. That
copy preserves the in-scope procedure and replaces prohibited data with roles
or approved placeholders; it is a temporary derived input, not a second
canonical process artifact.

For developer-onramp attachment mechanics used by this repository itself, see
the root
[Getting the developer context layer into an AI chat](../README.md#getting-the-developer-context-layer-into-an-ai-chat)
section and [`CONTEXT_LAYER.md`](../CONTEXT_LAYER.md). A finished process
capture is a *different* document with a *similar* attach pattern: supply the
complete approved procedure context, tell the model it is governing procedure
for this process, and require it not to invent steps the file does not
contain.

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
- Treat an evidence dump as retained source material, not complete procedure.
- Preserve the SME's own terms before standardizing vocabulary.
- Distinguish what the SME said from what anyone is inferring.
- Never invent a step, exception, system name, or pitfall to make the draft
  look complete.
- Mark unknowns and open questions explicitly.
- Gate completion on SME sign-off, not on document length.
- Never put credentials, recovery codes, account numbers, or production
  secrets into the artifact or the chat.
- Use only source material approved for the LLM chat's data boundary; retain
  raw transcripts and evidence separately.
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
