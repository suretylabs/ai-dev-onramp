# Elicitation and Shadowing

> Companion: [Consultant-lane flow](../visuals/00-consultant-lane-flow.md) ·
> Prior phase: [01-prepare-and-scope.md](01-prepare-and-scope.md)

## Objective

Gather process facts from the SME **or** normalize existing source evidence:
happy path, decision branches, systems touched, timing, exceptions,
escalation contacts, and the pitfalls new people usually hit. Prefer watching
real work. Do not invent what was not shown, stated, or documented.

## Preconditions

- Phase 1 gate passed.
- Header-only or blank `PROCESS_CAPTURE.md` exists.
- One entry path is selected: guided elicitation or existing evidence dump.
- Any evidence sent to an LLM has passed the organization's approved
  data-sharing and redaction boundary.

## Two entry paths

| Path | Use when | Do not assume |
|---|---|---|
| Guided elicitation | The facilitator can shadow, run a walkthrough, or interview the SME. | A single observed run covers every branch. |
| Existing evidence dump | A transcript, voice-to-text output, observation notes, checklist/SOP, sanitized screenshot/document excerpt, or mixture already exists. | Detailed source material is current, complete, official, or safe to copy into procedure. |

Both paths converge in **evidence normalization** and then enter the existing
Phase 3 drafting and Phase 4 validation gates.

## Existing evidence-dump ingestion

### 1. Preserve and inventory the sources

Keep each raw source outside `PROCESS_CAPTURE.md` in an approved client
location. Give it a short identifier such as `SRC-01`, then record:

- source type;
- date or capture date;
- participant or origin;
- canonical retained location, if applicable;
- the capture portions it may support; and
- limitations (for example, "undated SOP" or "voice-to-text may have
  misheard product names").

Do not paste a large transcript into the process capture. Do not assume a
source is authoritative because it is detailed.

### 2. Normalize candidates without promoting them to procedure

Create a temporary structured evidence summary that identifies candidate:

- process boundaries;
- actors and roles;
- systems and tools;
- happy-path steps;
- decisions and branches;
- exceptions;
- pitfalls and tribal knowledge;
- escalation paths;
- systems of record;
- local terminology; and
- unresolved gaps.

For each candidate claim, apply the evidence label from the lane contract:
`observed`, `stated`, `document`, `inferred`, or `unknown`. A transcript
claim is normally `stated`; an SOP/checklist claim is normally `document`;
neither label makes it final procedure.

### 3. Detect uncertainty before drafting

List separately any statements that are:

- contradictory across sources;
- ambiguous ("usually," "close to," "sometimes," or undefined pronouns);
- time-dependent (thresholds, names, system screens, cadence, or policy may
  have changed); or
- outside the agreed process boundary.

Unsupported conclusions become **Open questions / unresolved gaps**, not
procedure text.

### 4. Prepare SME follow-up

Generate a concise, prioritized set of questions that resolves the highest
risk gaps first. Each question should name the source ID and ambiguity, for
example:

> `SRC-02` says a high-value batch needs approval; `SRC-04` says the clerk
> submits all batches. Which rule is current, and what is the threshold?

### 5. Produce the draft, then converge

Give the facilitator:

1. the structured evidence summary;
2. contradictions, ambiguities, and unknowns;
3. targeted SME follow-up questions; and
4. a **draft** `PROCESS_CAPTURE.md` with lightweight source provenance.

The output is not signed or supposedly complete. Continue through
[Phase 3](03-drafting-the-process-capture.md) and
[Phase 4](04-validation-and-handoff.md) exactly as for guided elicitation.

## Observation protocol

When shadowing:

1. State the scope boundary again at the start of the session.
2. Ask the SME to work at normal pace and narrate only when it does not
   distort the work.
3. Note systems, screens, paper forms, folders, and handoffs as they appear.
4. When something surprising happens, mark it and ask about it at a pause —
   not mid-keystroke if that breaks concentration.
5. After the run, walk the notes back with the SME for corrections.

Capture **what happened**, then ask **what usually happens** if this run was
unusual.

## Interview protocol

When observation is not possible:

1. Start at the trigger: "What makes you start this process?"
2. Walk forward one step at a time: "What do you do next?"
3. At each step ask: system, input, output, who else is involved.
4. Only after the happy path, ask for branches: "When does that not work?"
5. End with pitfalls and "what do new people get wrong?"

Do not bounce randomly across the process; lost structure produces lost
exceptions.

## Question patterns that surface tacit knowledge

Use short prompts. Prefer the SME's words in the notes.

| Goal | Example prompts |
|---|---|
| Happy path | "Walk me through a normal one from start to finish." |
| Trigger | "What shows up that tells you to start?" |
| Systems | "What do you open or touch for this step? Paper counts." |
| Access by role | "Who is allowed to do that screen or drawer — which job title?" |
| Timing | "How often? Busy days? Deadlines?" |
| Volume | "Roughly how many per day or week?" |
| Decisions | "Where do you have to choose A vs B?" |
| Exceptions | "What breaks this? What do you do then?" |
| Pitfalls | "What do new people usually mess up?" |
| Workarounds | "Is there a way people actually do it that is not in the binder?" |
| Escalation | "When do you stop and who do you call?" |
| Definition of done | "How do you know this instance is finished?" |
| Evidence | "What gets filed, stamped, emailed, or logged?" |

## Always collect (if in scope)

- Systems and tools touched (product names as the SME uses them).
- Login or access **by role**, never passwords.
- Inputs and outputs per major step.
- Decision points with named branches.
- Exception paths and dead ends.
- Timing, frequency, volume, and calendar constraints.
- Escalation contacts by role (and name only if the organization wants names
  in the internal artifact).
- Pitfalls and tribal knowledge the SME can actually name.
- Source documents or systems of record the SME trusts.

## Never collect into the artifact

- Passwords, tokens, recovery codes.
- Full account, card, or cheque numbers.
- Unredacted customer secrets beyond what the internal audience is allowed to
  store in that location.
- Speculative steps "they must be doing" that the SME did not confirm.

## Note-taking discipline

For each fact, keep a light source tag when practical:

```text
[SRC-01 observed] Opens MailRoom Pro batch for today's date
[SRC-02 stated] If cheque is unsigned, puts in Rivera review tray
[SRC-03 document] SOP says controller approves flagged batches
[inferred — confirm] Maybe same tray is used for stop-payments?
```

Move every `inferred` item to confirmation or to open questions before draft
finalization. Add a source-provenance entry for every retained source used to
support the draft.

## Mid-session checkpoints

Pause when:

- the SME crossed the agreed end boundary;
- a second process started ("while I'm in here I also…");
- two conflicting rules appeared;
- access or data sensitivity blocked detail.

Options: narrow scope, schedule a second process capture, or mark a hard stop
in open questions.

## Phase gate

Pass only when guided elicitation or normalized evidence includes:

1. A coherent happy path inside the agreed boundary.
2. Major decision branches the SME considers real (or an explicit "no major
   branches").
3. Systems/tools list with access-by-role where relevant.
4. At least the exceptions and pitfalls the SME could name (including "none
   that I can think of" if truly empty after prompting).
5. Escalation path for stuck cases.
6. A working list of open questions for anything still unknown.
7. For existing evidence, source provenance plus an explicit contradiction and
   ambiguity review.

## Checkpoint prompt

> Elicitation for **\<process\>** produced a happy path of N steps, M named
> branches, and K open questions. Highest-risk gap: \<gap\>.
>
> Next: draft into `PROCESS_CAPTURE.md`, or run one more focused session on
> \<gap\> first?

## Anti-patterns

- Writing polished procedure language during the first watch.
- Skipping "what do new people get wrong?"
- Accepting "just use common sense" as a step.
- Recording credentials "so the new hire has them."
- Following the SME into a second process without rescoping.
- Treating a detailed transcript or SOP as signed procedure.
- Embedding the raw evidence dump in `PROCESS_CAPTURE.md`.
