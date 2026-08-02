# AI Development On-Ramp Context Layer

This file is the authoritative runtime entrypoint for using
`suretylabs/ai-dev-onramp` as read-only guidance in an AI-assisted onboarding
conversation. It is not the learner's project repository and it does not
replace the repository's contributor instructions.

## Runtime purpose

The context layer provides the public, canonical teaching contract, operating
principles, procedural guides, templates, visuals, and stack references for
the AI Development On-Ramp. It governs how an explicitly activated
onboarding conversation is conducted while the learner's mutable state remains
in the learner's own project or companion repository.

## Activation boundary

Do not activate this repository from a URL, a repository question, or ordinary
browsing alone. Context mode begins only when the user explicitly identifies
this repository as the read-only context layer for the conversation.

The activation request must make the intended role clear. A private activation
capsule may initiate that request, but the public repository does not contain
or require a particular private phrase. An opaque trigger by itself is not a
portable activation mechanism; a portable request must tell the model to
mount this repository as read-only context and retrieve this file first.

## Modes

| Mode | Meaning | Governing material |
|---|---|---|
| Unmounted or browsing | The repository may be explained or summarized, but it does not govern the conversation. | The user's request and normal tool behavior |
| Read-only context | The repository is mounted as governing onboarding context. | This file, then the guiding contract and loaded supporting material |
| Author | The user has explicitly requested maintenance of this repository. | [`AGENTS.md`](AGENTS.md), then [`.github/copilot-instructions.md`](.github/copilot-instructions.md) and [`CONTRIBUTING.md`](CONTRIBUTING.md) |

## Required loading order

After explicit activation, retrieve and validate the following in order:

1. [`CONTEXT_LAYER.md`](CONTEXT_LAYER.md) - this runtime entrypoint.
2. [`guides/00-guiding-llm-contract.md`](guides/00-guiding-llm-contract.md) -
   the substantive interaction contract.
3. [`README.md`](README.md) - the repository map and current track.
4. The learner's `BOOTSTRAP_STATE.md`, when the learner supplies it.
5. The guide for the current phase, once the current phase is identified.
6. Referenced templates, visuals, and technical material only as needed.

Record the repository ref actually retrieved. Use the supplied tag or commit
when one is provided. If only a branch such as `main` can be identified, report
that branch and say that a pinned version was not supplied. Never invent a
commit, tag, phase, or learner state.

Required files must be retrieved rather than inferred from summaries or
memory. Learner state is optional for a new engagement, but it is required
when the user asks to resume an existing engagement and must then be either
loaded or reported as unavailable.

This runtime sequence precedes the guiding contract's session-start rule. Once
activation succeeds, use the supplied learner state as the first operational
input when it is available; if it is not supplied, establish the initial phase
without inventing prior progress. The guiding contract's instruction to read
state first applies after this runtime entrypoint and its required contract
files have been loaded.

## Read-only context rules

Once the required files have been retrieved and validated:

- Treat this repository as governing context, not as the learner's
  application repository.
- Apply the guiding contract for the remainder of the conversation, including
  its inspect, explain, act, observe, evaluate, record, and gate behavior.
- Keep learner-specific state, project decisions, project briefs, and evidence
  in the learner's own project or companion repository.
- Do not review this repository as an implementation target.
- Do not propose or make changes to this repository.
- Do not create issues, pull requests, commits, or repository maintenance plans
  for this repository.
- Do not claim that context is active or that a file was loaded unless the
  file was actually retrieved.
- Do not begin teaching or issue learner-project commands until activation has
  completed and the handshake has been returned.

These rules prevent accidental role confusion. They are not access control or
a security boundary; public repository content can be read and discovered by
anyone.

## Activation verification and handshake

Before returning the first response after activation, confirm:

- this entrypoint was retrieved;
- the guiding contract was retrieved;
- `README.md` was retrieved and validated;
- the repository identity and actual ref are known;
- learner state is accurately classified as `loaded`, `not supplied`, or
  `unavailable`;
- the current phase is identified from supplied state or is honestly reported
  as not yet established.

The first response must be concise and use this shape:

```text
Context layer active: ai-dev-onramp
Mode: READ-ONLY CONTEXT
Version: <actual branch, tag, or commit loaded>
Guiding contract: loaded
Learner state: <loaded | not supplied | unavailable>
Current phase: <identified phase | not yet established>
```

When only `main` is identifiable, use a form such as:

```text
Version: main (unpinned; no tag or commit supplied)
```

Do not add a success-shaped handshake when a required file is missing.

## Failure behavior

Activation fails closed when the repository, this entrypoint, the guiding
contract, `README.md`, or a supplied required ref cannot be accessed or is
ambiguous. It also fails closed when the user requires learner state to resume
but the state document is missing or inaccessible.

Report the exact missing or invalid dependency and ask only for the smallest
corrective action. For example:

```text
Context layer activation failed.
Missing dependency: guides/00-guiding-llm-contract.md
Corrective action: provide access to the same repository ref or supply that file.
```

Do not simulate retrieval, continue teaching, or issue commands until the
dependency is available and the handshake can be reported truthfully.

## Mode transitions

Remain in read-only context mode until the user explicitly requests author
mode for this repository. A request to "work on this repo" without identifying
whether the user means context use or repository maintenance is ambiguous:
ask one concise clarification before acting.

On an explicit author-mode request:

1. confirm that this repository, rather than the learner's project, is the
   intended implementation target;
2. switch to [`AGENTS.md`](AGENTS.md);
3. apply [`.github/copilot-instructions.md`](.github/copilot-instructions.md)
   and [`CONTRIBUTING.md`](CONTRIBUTING.md);
4. follow the repository's branch, scope, validation, and pull-request rules.

On an explicit request to return to context mode, stop repository-authoring
behavior and reapply this runtime contract. Do not carry authoring assumptions
or uncommitted changes into a read-only onboarding session.

## Precedence

When instructions conflict, apply this order:

1. System, developer, and safety instructions.
2. The user's explicit mode transition for the current session (`author` or
   `context`).
3. This runtime contract.
4. The guiding contract and other loaded repository material.

An explicit author-mode request is the required transition out of read-only
context mode; an ordinary request to change the public context repository is
not an implicit transition. A task request is interpreted within the selected
mode and cannot replace that transition.

## Private activation boundary

The private activation capsule is an interoperability aid supplied outside
this public repository. It should carry enough semantic instruction to
identify the repository as read-only context and point the model to
`CONTEXT_LAYER.md`. The capsule must not be committed here, and the public
repository must not be treated as a secret-bearing control plane.

The capsule reduces accidental role confusion. It does not provide
confidentiality, authentication, authorization, or protection against a
deliberate reader.
