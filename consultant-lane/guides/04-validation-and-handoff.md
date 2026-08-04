# Validation and Handoff

> Companion: [Consultant-lane flow](../visuals/00-consultant-lane-flow.md) ·
> Prior phase: [03-drafting-the-process-capture.md](03-drafting-the-process-capture.md)

## Objective

Walk the draft with the SME, correct errors, resolve or consciously defer
open questions, obtain sign-off, version the artifact, and hand it to the
people who will attach it to an LLM session as process context.

## Preconditions

- Phase 3 gate passed.
- SME (and owner, if sign-off requires both) available for review.

## Validation walkthrough

### 1. Read-back, not silent approval

Do not email a long Markdown file and ask "looks good?" Sit with the SME (or
screen-share) and:

1. Restate the scope boundary.
2. Walk the happy path step by step.
3. Stop at each decision branch and exception.
4. Read the pitfalls list and ask what is missing or wrong.
5. Review open questions one by one.

Capture corrections **in the session**.

### 2. Disposition every open question

For each open question, choose one:

| Disposition | Meaning |
|---|---|
| Resolved | Answer written into the correct procedure section; remove from open list. |
| Deferred | Remains open; artifact may still ship if the success definition allows, with the gap visible. |
| Out of scope | Moved to a follow-up process capture or owner backlog. |
| Blocked | Sign-off cannot proceed until answered. |

A signed artifact may still list deferred gaps. It must not pretend they are
closed.

### 3. Owner vs SME conflict

If lived practice and official policy disagree:

1. Document both clearly.
2. Ask the owner which is authoritative for the consumer audience.
3. Do not silently pick the cleaner story.

### 4. Sign-off block

When the SME (and owner if required) agrees the artifact is accurate enough
for the stated success definition, fill:

- last-validated date;
- SME name/role and acknowledgment;
- owner name/role if required;
- artifact version (start at `1.0` unless the team has another scheme);
- status: `signed`.

Sign-off means: "A person following this file for in-scope work will not be
misled on the known happy path and named exceptions." It does not mean every
rare case in the company is documented.

## Versioning after sign-off

| Event | Action |
|---|---|
| Typo or clarification, no behavior change | Patch version; note in revision line. |
| Step, system, or rule change | Minor or major version per team policy; new validation date; SME re-ack if behavior changed. |
| Scope boundary change | New version and explicit scope diff; often treat as re-capture. |
| Process retired | Mark status `retired` and point to replacement if any. |

Keep prior signed versions if the organization's retention rules require it.

## Handoff to a new hire (or their LLM)

### What to give them

1. The signed `PROCESS_CAPTURE.md` (complete file).
2. Where the canonical copy lives.
3. Who to ask when the file and reality diverge.
4. Instruction that the file is **read-only operating context** for this
   process — not a license to invent steps.

### Attaching to an LLM session

The pattern mirrors how this repository mounts its own context layer, but the
document is the process capture, not `CONTEXT_LAYER.md`.

Facilitator or new hire can start with:

```text
I am attaching a signed process-capture document for one business process.
Treat it as the governing procedure for that process in this conversation.

Rules:
1. Do not invent steps, exceptions, systems, or contacts that are not in the file.
2. If the file lists open questions or unknowns, surface them instead of guessing.
3. If I describe a situation outside the file's scope boundary, say so and stop.
4. Walk me through the happy path or a named branch only from the document.
5. Never ask me to paste passwords or full account numbers into chat.
```

Then supply the **complete** signed file (not a summary).

For this repository's own attach mechanics and access-path discipline, see:

- [Getting the context layer into an AI chat](../../README.md#getting-the-context-layer-into-an-ai-chat)
- [`CONTEXT_LAYER.md`](../../CONTEXT_LAYER.md)

Those pages govern mounting **this public on-ramp**. A client process capture
reuses the *idea* (complete file, explicit rules, no invention) without
pretending to be this repository's runtime entrypoint.

### First supervised run

Recommend one observed performance with the SME or backup present while the
new hire (and optional LLM) follows the artifact. Note friction; feed
corrections into the next version.

## Phase gate

Pass only when:

1. SME walkthrough completed and corrections applied.
2. Every former open question is resolved, deferred (visible), out of scope,
   or still blocking (in which case status is not `signed`).
3. Sign-off block is complete and status is `signed` (or an explicit decision
   to remain `draft` is recorded with owner).
4. Canonical storage location is known to the consumer audience.
5. Handoff instructions for LLM attachment are available to the facilitator
   or new hire.

## Checkpoint prompt

> **\<process\>** v\<version\> is signed by \<SME\> on \<date\>. Deferred gaps:
> \<count\>. Canonical path: \<path\>.
>
> Handoff package ready. Next process to scope, or pause?

## Anti-patterns

- "LGTM" on a file the SME never walked through.
- Deleting open questions to make the doc look finished.
- Emailing credentials alongside the artifact.
- Letting the LLM "improve" the procedure after sign-off without re-validation.
- Assuming the public `ai-dev-onramp` context-layer handshake activates a
  client process file automatically — it does not; the process file needs its
  own attach instruction.
