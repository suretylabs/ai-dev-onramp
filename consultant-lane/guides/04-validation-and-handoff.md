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
6. Review source provenance where a claim was ambiguous, conflicting, or
   time-dependent; confirm that the final procedure reflects the current rule.

Capture corrections **in the session**.

### 2. Disposition every open question

For each entry in the pre-validation open-question table, use this lifecycle:

| Disposition | Meaning |
|---|---|
| Open | Still awaiting validation or an owner decision. A signed capture cannot retain this status. |
| Resolved | Answer written into the correct procedure section; remove from open list. |
| Deferred | Remains open; artifact may still ship if the success definition allows, with the gap visible. |
| Out of scope | Moved to a follow-up process capture or owner backlog. |
| Blocked | Sign-off cannot proceed until answered. |

A signed artifact may still list deferred gaps. It must not pretend they are
closed. `Resolved` is a lifecycle result rather than a persistent table value:
after writing the answer into procedure, remove the resolved row. The template
therefore permits only `open`, `deferred`, `out of scope`, and `blocked`.

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

1. The signed canonical `PROCESS_CAPTURE.md` in its approved internal
   location.
2. A complete chat-safe session copy only when the canonical file contains
   names, identifiers, locations, or other data not approved for the LLM
   chat. Keep the procedure complete, replace prohibited content with roles
   or approved placeholders, and do not make the copy a second canonical
   artifact.
3. Where the canonical copy lives.
4. Who to ask when the file and reality diverge.
5. Instruction that the file is **read-only operating context** for this
   process — not a license to invent steps.

### Attaching to an LLM session

The pattern mirrors how this repository mounts its own context layer, but the
document is the process capture, not `CONTEXT_LAYER.md`. First decide which
content is approved for the chat. Do not upload a raw transcript or a
canonical signed capture containing employee identifiers or internal
locations when those are not allowed in the chat. Attach the complete
chat-safe session copy in that case.

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

Then supply the **complete approved procedure context** (not a summary). The
canonical signed capture remains the durable source of truth; a chat-safe
copy is only a temporary attachment.

For this repository's own attach mechanics and access-path discipline, see:

- [Getting the developer context layer into an AI chat](../../README.md#getting-the-developer-context-layer-into-an-ai-chat)
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
   with no `blocked` question remaining.
3. Sign-off block is complete and status is `signed`.
4. Canonical storage location is known to the consumer audience.
5. Handoff instructions for LLM attachment are available to the facilitator
   or new hire.

If a question remains `blocked` or the artifact remains `draft`, this phase
does **not** pass. Record the exact blocker and return to evidence gathering
or drafting; do not hand off the process as complete.

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
- Attaching an unredacted canonical capture to a chat that is not approved for
  its names, identifiers, provenance locations, or other internal content.
- Assuming the public `ai-dev-onramp` context-layer handshake activates a
  client process file automatically — it does not; the process file needs its
  own attach instruction.
