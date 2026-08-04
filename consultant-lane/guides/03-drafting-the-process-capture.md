# Drafting the Process Capture

> Companion: [Consultant-lane flow](../visuals/00-consultant-lane-flow.md) ·
> Template: [../templates/PROCESS_CAPTURE.md](../templates/PROCESS_CAPTURE.md) ·
> Example shape: [../templates/PROCESS_CAPTURE.example.md](../templates/PROCESS_CAPTURE.example.md)

## Objective

Turn elicitation notes or normalized existing evidence into a single structured
`PROCESS_CAPTURE.md` without inventing missing steps. Preserve the SME's
terms first; standardize only where it helps the next reader.

## Preconditions

- Phase 2 gate passed (or explicitly partial with open questions listed).
- Destination file path known.
- Raw source evidence is retained separately, with enough provenance to
  reference it from the draft.

## Drafting order

Fill the template in this order so structure stays honest:

1. Document control, process identity, owner, SME, and status (`draft`).
2. Source evidence and provenance (source IDs and references, not raw dumps).
3. Trigger and frequency.
4. Scope boundary (starts when / ends when) — copy from phase 1, adjust only
   if elicitation proved the boundary wrong (and note the change).
5. Systems and tools table.
6. Step-by-step happy path.
7. Decision points and branches.
8. Exceptions and edge cases.
9. Pitfalls and tribal knowledge.
10. Escalation and who to ask.
11. Glossary.
12. Source documents / systems of record.
13. Open questions / unresolved gaps.
14. Leave sign-off empty until phase 4.

## Writing rules

### Preserve operator language

First draft should sound like the SME. If they say "the blue tray," write
"the blue tray" and add a glossary entry if a formal name exists.

### One action per step

Prefer:

```text
3. Open MailRoom Pro and select today's intake batch.
```

over multi-action paragraphs that hide decision points.

### Make branches explicit

Do not bury "unless" clauses only inside happy-path prose. Lift real choices
into **Decision points and branches** and reference them from the step list.

### Mark uncertainty; do not smooth it

| Situation | Action |
|---|---|
| SME stated a step clearly | Write it as procedure. |
| Two SMEs disagreed | Record both; add open question for owner. |
| Facilitator is guessing | Do not write as procedure. Open question. |
| Rare path not fully known | Name the trigger; mark steps `unknown`. |
| Official SOP conflicts with practice | Capture both; label which is lived practice. |

### Keep secrets out

Replace sensitive values with placeholders the organization accepts:

```text
account ending ··4210
[redacted cheque number]
```

If the destination system must not hold even partial identifiers, omit them
and describe the field by purpose only.

## Mapping notes → template sections

| Notes cluster | Template section |
|---|---|
| Name, owner, SME | Process identity and owner |
| Transcript, voice-to-text, notes, SOP, or sanitized excerpt metadata | Source evidence and provenance |
| Cadence, deadlines | Trigger and frequency |
| Start/end agreement | Scope boundary |
| Apps, trays, printers, fileshares | Systems and tools touched |
| Numbered walkthrough | Step-by-step procedure |
| If/then choices | Decision points and branches |
| Breakage and recoveries | Exceptions and edge cases |
| "New people always…" | Pitfalls and tribal knowledge |
| Who to call | Escalation and who to ask |
| Local jargon | Glossary |
| Binders, SOPs, system of record | Source documents / systems of record |
| Unconfirmed items | Open questions / unresolved gaps |

## LLM-assisted drafting constraints

When an LLM helps rewrite notes or an evidence dump into the template:

- Provide the notes or approved evidence, source identifiers, and the blank
  template sections being filled.
- Instruct: do not add steps, systems, or pitfalls absent from the supplied
  sources.
- Require it to preserve raw sources separately and add only lightweight
  provenance references to the draft.
- Require a short "inferences attempted" list after each drafting pass.
- Require contradictions, ambiguous statements, and time-dependent claims to
  become targeted SME questions or open questions.
- Facilitator must delete or relocate every unconfirmed inference before SME
  review.

Useful instruction pattern:

> Rewrite only from the approved source evidence below into the listed
> sections. Keep source IDs and provenance, but do not embed the raw source.
> If a required detail is missing, contradictory, ambiguous, or time-dependent,
> put a bullet under Open questions and generate a targeted SME question
> instead of inventing it. Preserve the SME's terms.

## Quality self-check before validation

- [ ] Happy path stays inside the stated start/end boundary.
- [ ] Every system mentioned in steps appears in the systems table (or vice
  versa gap is listed).
- [ ] Every decision in the prose appears in the decision table.
- [ ] Source provenance identifies every retained source used for the draft;
  the raw transcript, notes, and images are not embedded.
- [ ] Contradictory, ambiguous, and time-dependent statements have become
  open questions or SME follow-up questions.
- [ ] Open questions are non-empty if any `unknown` remains — or explicitly
  state none.
- [ ] No credentials or full account/cheque numbers.
- [ ] Status is still `draft` (not signed).

## Phase gate

Pass only when:

1. The draft uses the `PROCESS_CAPTURE.md` structure.
2. Happy path and known branches are written from SME evidence.
3. Gaps live in **Open questions / unresolved gaps**, not as fake steps.
4. Facilitator has removed unconfirmed LLM inferences from procedure text.
5. Source provenance is traceable without duplicating the raw evidence dump.
6. File is ready for SME walkthrough (phase 4).

## Checkpoint prompt

> Draft for **\<process\>** is ready for SME review. Open questions remaining:
> \<count\>. No procedure text is still tagged inferred.
>
> Next: schedule validation walkthrough with \<SME\>?

## Anti-patterns

- Completing every template heading with plausible filler.
- Translating everything into corporate jargon the SME does not use.
- Dropping pitfalls because they feel "unprofessional."
- Marking status `signed` before the SME has reviewed.
