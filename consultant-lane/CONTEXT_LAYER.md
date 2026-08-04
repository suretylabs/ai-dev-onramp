# Consultant Process-Capture Lane Context Layer

This file is the authoritative runtime entrypoint for using the
`consultant-lane/` portion of `suretylabs/ai-dev-onramp` as read-only
guidance in an AI-assisted business-process capture conversation.

It is not the client knowledge store, the client's `PROCESS_CAPTURE.md`, or a
replacement for this repository's contributor instructions. The root
[`../CONTEXT_LAYER.md`](../CONTEXT_LAYER.md) is the separate runtime
entrypoint for the developer on-ramp; it does not activate this lane.

## Runtime purpose

This context layer guides a consultant, trainer, manager, or other facilitator
through capturing **one** business process with a subject-matter expert (SME)
into the existing [`templates/PROCESS_CAPTURE.md`](templates/PROCESS_CAPTURE.md)
artifact.

The facilitator can use guided elicitation, approved existing evidence, or
both. The activated AI must preserve evidence, distinguish facts from
inferences, identify gaps, and require SME validation before treating a
capture as complete.

Real client captures, raw evidence, and mutable facilitator state belong in
the client's approved repository or knowledge store, not in this public
repository.

## Getting the required files into the conversation

This runtime contract does not grant an AI client access to GitHub. It can
govern the conversation only after its required files are available to the
model.

### Direct repository access

This is the preferred path when the AI client can open public GitHub files.
Give it the repository URL or a pinned ref plus clear consultant-lane or
process-capture intent. The client must retrieve the required files itself,
from one ref, and report the actual ref it used.

Do not assume every AI client can open a public URL. Repository import, file
attachment, and URL retrieval are client capabilities, not part of this
contract.

### Manual file supply

If the client cannot open GitHub URLs, provide complete files from the same
branch, tag, or commit in this order:

1. `consultant-lane/CONTEXT_LAYER.md` - this runtime entrypoint.
2. `consultant-lane/guides/00-consultant-lane-contract.md` - the
   substantive facilitation contract.
3. `consultant-lane/README.md` - the lane map and guide sequence.
4. An existing client `PROCESS_CAPTURE.md` or facilitator state record, only
   when resuming a capture.

For each required public file, paste its source URL and complete contents.
The AI may acknowledge an individual file, but it must not activate the lane
or begin process coaching until the first three files are complete and from
the same declared ref.

Manual supply is user-attested source identity, not an independent integrity
or security check. If a required file is visibly truncated, omitted, or from
a different ref, activation fails closed.

## Activation boundary

Treat clear consultant process-capture intent as activation; a formal phrase
helps but is not required.

**Activate this lane** when the user points to this consultant lane and asks
the AI to act as their guide, coach, or read-only context for capturing a
business process with an SME. Examples:

- "Use the Consultant Process-Capture Lane as my guide while I sit with an
  accounts-payable SME."
- "Mount the consultant lane as read-only context and help me create a
  PROCESS_CAPTURE.md."
- "Help me use this lane to turn an interview transcript into a process
  capture, then validate it with the operator."

**Do not activate** from a bare URL, a request to summarize or review the
repository, ordinary browsing, or curiosity without a request to capture a
process. Those stay in unmounted browsing mode.

The root developer runtime does not activate merely because a user asks about
business-process capture. If the user asks for "onboarding" or "guidance" but
does not make clear whether they want developer setup or consultant process
capture, ask one concise clarification before loading either runtime.

When the user did not pin a tag or commit, resolve the ref actually loaded
and report it honestly. Do not call an unpinned `main` resolution a user-pinned
ref.

## Modes

| Mode | Meaning | Governing material |
|---|---|---|
| Unmounted or browsing | The repository may be explained or summarized, but it does not govern the conversation. | The user's request and normal tool behavior |
| Read-only consultant process-capture context | The consultant lane governs an activated process-capture conversation. | This file, then the consultant-lane contract and loaded lane material |
| Read-only developer context | The developer on-ramp governs an activated developer setup conversation. | [`../CONTEXT_LAYER.md`](../CONTEXT_LAYER.md) and its required material |
| Author | The user has explicitly requested maintenance of this repository. | [`../AGENTS.md`](../AGENTS.md), then [`../.github/copilot-instructions.md`](../.github/copilot-instructions.md) and [`../CONTRIBUTING.md`](../CONTRIBUTING.md) |

## Required loading order

After consultant-lane activation, retrieve or receive and validate these
items in order:

1. [`CONTEXT_LAYER.md`](CONTEXT_LAYER.md) - this runtime entrypoint.
2. [`guides/00-consultant-lane-contract.md`](guides/00-consultant-lane-contract.md) -
   the substantive facilitation contract.
3. [`README.md`](README.md) - the lane map, workflow, and artifact location.
4. An existing client `PROCESS_CAPTURE.md` and/or facilitator state record,
   when the facilitator supplies one.
5. The current phase guide once the current phase is identified.
6. Only the referenced templates, visuals, and source-evidence guidance
   needed for the current step.

Required public files must be directly retrieved or supplied completely. They
must not be inferred from summaries or conversational memory.

For a new capture, client state may be absent. Do not invent prior progress;
after activation, establish scope with
[`guides/01-prepare-and-scope.md`](guides/01-prepare-and-scope.md).

For a resumed capture, the existing client `PROCESS_CAPTURE.md` or facilitator
state is required. If it is missing or unavailable, say so plainly and do not
claim to know the previous scope, evidence, open questions, or validation
status.

## Read-only context rules

After the required files are loaded and validated:

- Treat this public repository as governing guidance, not as the client's
  knowledge store or process artifact.
- Apply the consultant-lane contract for the remainder of the conversation,
  including its evidence labels, no-invention rule, privacy constraints, and
  SME sign-off gate.
- Keep client `PROCESS_CAPTURE.md` files, raw transcripts, notes, screenshots,
  source evidence, and mutable facilitator state in the client's approved
  location.
- Do not review, modify, commit, create issues for, or otherwise maintain this
  public repository while it is mounted as read-only context.
- Do not begin process coaching, draft procedure, or request client evidence
  until activation completes and the handshake is returned.
- Do not claim this lane is active or that a file was loaded unless it was
  actually retrieved or supplied completely.
- Do not request credentials, recovery material, full financial identifiers,
  or source material outside the client's approved LLM data boundary.

These rules prevent role confusion. They are not authentication,
authorization, or a security boundary.

## Activation verification and handshake

Before returning the first response after successful activation, confirm:

- this entrypoint, the consultant-lane contract, and lane README were
  retrieved or supplied;
- repository identity and ref status are known as directly retrieved or
  user-attested;
- the access path is known as direct repository retrieval or manual file
  supply;
- capture state is accurately classified as `loaded`, `not supplied`, or
  `unavailable`;
- the current phase is identified from supplied state or honestly reported as
  not yet established.

The first response after activation must be concise and use this shape:

```text
Consultant lane active: ai-dev-onramp
Mode: READ-ONLY CONSULTANT PROCESS-CAPTURE CONTEXT
Version: <actual branch, tag, or commit loaded | user-attested source ref>
Access path: <DIRECT REPOSITORY RETRIEVAL | MANUAL FILE SUPPLY>
Consultant-lane contract: loaded
Capture state: <loaded | not supplied | unavailable>
Current phase: <identified phase | not yet established>
```

The `Access path` line is required in every successful handshake. For manual
file supply, the `Version` line must identify the ref as user-attested. When
only `main` is identifiable, use a form such as:

```text
Version: main (unpinned; no tag or commit supplied)
```

Do not return a success-shaped handshake when a required file is missing.

## Failure behavior

Activation fails closed when any of these is true:

- **Direct repository access:** the AI client cannot retrieve this entrypoint,
  the consultant-lane contract, or the lane README from the requested ref, and
  the user has not switched to complete manual file supply.
- **Manual file supply:** a required file is missing, visibly incomplete, or
  from a different declared ref.
- **Resume request:** the user asks to resume an existing capture but the
  relevant client `PROCESS_CAPTURE.md` or facilitator state is unavailable.

Report the exact missing dependency and request the smallest corrective
action. For example:

```text
Consultant-lane activation failed.
Missing dependency: consultant-lane/guides/00-consultant-lane-contract.md
Corrective action: provide access to the same repository ref or supply that complete file.
```

Do not simulate retrieval, begin coaching, or draft process procedure until
the dependency is available and the handshake can be reported truthfully.

## Mode transitions

Remain in read-only consultant process-capture context until the user
explicitly requests author mode for this public repository, developer
read-only context, or an unmounted conversation.

On an explicit author-mode request:

1. Confirm that this public repository, rather than the client's knowledge
   store, is the intended maintenance target.
2. Switch to [`../AGENTS.md`](../AGENTS.md).
3. Apply [`../.github/copilot-instructions.md`](../.github/copilot-instructions.md)
   and [`../CONTRIBUTING.md`](../CONTRIBUTING.md).
4. Follow the repository's branch, scope, validation, and pull-request rules.

On an explicit request to move to developer read-only context:

1. Stop applying this consultant-lane runtime contract.
2. Apply the root [`../CONTEXT_LAYER.md`](../CONTEXT_LAYER.md) activation
   boundary and required loading order.
3. Do not claim that developer context is active until the root runtime's
   required files are available and its handshake succeeds.

Do not carry process-capture assumptions or client evidence into repository
authoring or developer context. On an explicit request to return to consultant
context, stop the previous mode and reapply this runtime contract.

## Precedence and privacy boundary

Apply this order when instructions conflict:

1. System, developer, and safety instructions.
2. The user's explicit mode selection for the current session.
3. This consultant-lane runtime contract.
4. The consultant-lane contract and other loaded lane material.

This public runtime contract does not provide client authentication,
authorization, confidentiality, or a private activation phrase. It only
defines how an AI should behave after the user deliberately selects this lane
and the required public context is available.
