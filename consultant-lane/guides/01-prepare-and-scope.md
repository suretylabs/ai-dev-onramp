# Prepare and Scope

> Companion: [Consultant-lane flow](../visuals/00-consultant-lane-flow.md) ·
> Contract: [00-consultant-lane-contract.md](00-consultant-lane-contract.md)

## Objective

Before any shadowing or interview, name **one** process, bound where it
starts and ends, identify who owns it and who performs it, and agree what
"captured" means for this engagement.

Skipping this phase produces sprawling notes that never become a usable
artifact.

## Preconditions

- Facilitator has permission to observe or interview.
- There is at least one SME who currently performs the work.
- Destination for the finished file is known (client repo, SharePoint,
  handbook folder, etc.) — even if the path is provisional.

## Steps

### 1. Name the process in operator language

Ask the owner or SME:

> What do you call this work when you train someone?

Prefer their phrase over a consultant rebrand. Record alternate names in the
glossary later if needed.

### 2. Set the scope boundary

Write two sentences and get verbal agreement:

| Boundary | Prompt |
|---|---|
| Starts when | "What is the first event that means this process has begun?" |
| Ends when | "What is the last action after which you would say this instance is done?" |

If the SME cannot end the process without pulling in three other teams,
narrow until one operator's happy path fits a single session series.

### 3. Identify roles

| Role | Question |
|---|---|
| Process owner | Who can change the official procedure? |
| SME / veteran operator | Who actually does it day to day and knows the traps? |
| Backup performer | Who covers when the SME is out? (optional but useful) |
| Artifact consumer | Who will use the capture first (new hire, cross-train, auditor)? |

Owner and SME are often different people. Both matter: SME for accuracy,
owner for authority and sign-off path.

### 4. Agree what "captured" means

Pick an explicit success definition, for example:

- A new hire can perform the happy path with an LLM reading the artifact,
  without the SME present for routine cases; or
- Cross-training material exists for the backup performer; or
- Audit can see the official steps and named exception paths.

Write the chosen definition into the draft header later. Do not imply all
three if only one was requested.

### 5. Choose elicitation mode

| Mode | Use when |
|---|---|
| Observation / shadowing | The work happens on a predictable cadence and access is allowed. Preferred. |
| Live walkthrough | SME can demonstrate with sample or sanitized data. |
| Interview / tabletop | Observation is blocked; SME narrates with screens or checklists. |
| Hybrid | Observe once, then interview for rare exceptions. |

Record the planned mode. Mode can change later; silent switching is what
causes false confidence.

### 6. Timebox and logistics

Agree before the first elicitation session:

- session length and count;
- whether recording is allowed (default: notes only unless policy says
  otherwise);
- what must not be shown (live customer data, credentials, sealed mail
  contents beyond what policy allows);
- who will attend.

### 7. Seed the blank artifact

Copy [`../templates/PROCESS_CAPTURE.md`](../templates/PROCESS_CAPTURE.md) to
the destination path. Fill only:

- process name;
- owner;
- SME;
- planned start/end boundary;
- capture success definition;
- status: `scoping`.

Leave procedure sections empty.

## Phase gate

Pass only when all are true:

1. Process name is agreed in operator language.
2. Start and end boundaries are written and accepted by owner or SME.
3. Owner and SME are named.
4. Success definition for this capture is explicit.
5. Elicitation mode and first session logistics are set.
6. Blank (or header-only) `PROCESS_CAPTURE.md` exists at the destination.

## Checkpoint prompt

> Scope for **\<process name\>** is agreed. It starts when \<start\> and ends
> when \<end\>. SME is \<name\>; owner is \<name\>. Success means \<definition\>.
>
> Next session: \<mode and when\>. Ready to proceed to elicitation, or adjust
> the boundary first?

## Anti-patterns

- "Let's just start talking and see where it goes."
- Capturing an entire department in one document.
- Treating the org chart owner as the only source when they no longer perform
  the work.
- Promising a complete encyclopedia by Friday.
