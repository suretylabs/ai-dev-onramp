# Process Capture: Incoming cheque mail handling

> **Synthetic example only.** Fictional organization, roles, and systems for
> teaching the template shape. Do not treat as a real procedure.

## Document control

| Field | Value |
|---|---|
| Status | `signed` |
| Version | 1.0 |
| Last validated | 2026-07-15 |
| Canonical path | `docs/processes/incoming-cheque-mail-handling.md` (example) |
| Facilitator | Sam (internal consultant, example) |
| Related captures | Deposit discrepancy follow-up (not yet captured) |

## Source evidence and provenance

> **Synthetic source references only.** Raw sources are separately retained;
> this table records the evidence that supported the capture without embedding
> a full transcript or observation log.

| Source ID | Source type | Date | Participant or origin | Evidence label(s) | Which portions of this capture it supports | Canonical retained location | Limitations / follow-up |
|---|---|---|---|---|---|---|---|
| SRC-01 | Interview transcript | 2026-07-08 | Jordan, AP clerk | `stated` | Trigger, steps 1–8, E2, E3, local terms | `evidence/interviews/2026-07-08-jordan-ap.md` (example) | Jordan said "if it is close to the threshold, I normally ask Rivera." That ambiguous claim became draft question Q-01 before validation. |
| SRC-02 | Observation notes | 2026-07-10 | Sam, facilitator | `observed` | Steps 1–7, blue/red bag distinction, drawer handoff | `evidence/observations/2026-07-10-mail-run.md` (example) | One normal-volume run; it did not demonstrate a threshold approval or scanner outage. |
| SRC-03 | LedgerApp approval-screen walkthrough | 2026-07-15 | Rivera, controller | `document`, `stated` | D2, Q-01 resolution | `evidence/validation/2026-07-15-rivera-approval.md` (example) | Current on-screen flag is authoritative; exact threshold value is intentionally not copied into this capture. |

### Evidence-normalization note

Before SME validation, `SRC-01`'s phrase "close to the threshold" had no
defined meaning. It became **draft question Q-01**, not a procedure step.
During validation, Rivera confirmed that LedgerApp's on-screen approval flag
is authoritative, so Q-01 was resolved and removed from **Open questions /
unresolved gaps**. Decision D2 records the validated rule below.

## Process identity and owner

| Field | Value |
|---|---|
| Process name (operator language) | Incoming cheque mail handling |
| Alternate names | "cheque batch", "mail deposit prep" |
| Process owner (role, name if internal policy allows) | Controller — Rivera |
| Primary SME / veteran operator | AP clerk — Jordan |
| Backup performer | AP clerk — Morgan |
| Primary consumer of this artifact | New AP clerk in first 30 days |
| Capture success definition | New AP clerk can complete a normal mail-day happy path with LLM assistance and without Jordan present; known exceptions are escalated correctly |

## Trigger and frequency

- **Trigger** (what starts an instance): Mailroom delivers the AP mesh bag to the AP desk and Jordan (or backup) accepts it.
- **Frequency / cadence**: Business days; bag usually arrives 09:30–10:30 local.
- **Typical volume**: About 15–40 envelopes on a normal day; month-start heavier.
- **Deadlines or calendar constraints**: Same-day deposit batch should be submitted in LedgerApp before 15:00 so treasury can include it in the evening file.

## Scope boundary

- **Starts when**: AP desk accepts the mesh bag from the mailroom runner.
- **Ends when**: Deposit batch is submitted in LedgerApp, the physical cheque packet is placed in the locked "treasury pickup" drawer, and the empty blue bag is returned to the mailroom shelf.
- **Explicitly out of scope** (adjacent work not covered here): Mailroom sorting before AP receives the bag; bank portal reconciliation next morning; customer payment application after deposit; stop-payment requests.

## Systems and tools touched

| System or tool | Purpose in this process | Access by role | Notes |
|---|---|---|---|
| Physical mesh bag + date stamp | Receive and date mail | AP clerk | Blue bag only — red bag is facilities, ignore |
| Letter opener / cheque scanner station | Open envelopes, scan images | AP clerk | Scanner PC is shared; profile is `AP-Scan` |
| MailRoom Pro | Create daily intake batch, attach scan images | AP clerk (create batch); controller (void batch) | |
| LedgerApp | Build and submit deposit batch | AP clerk (prepare); controller (approve if over threshold) | Threshold rules are owner-controlled |
| Shared drive `\\files\ap\deposits\` | Drop export PDF for treasury | AP clerk read/write | |
| Locked "treasury pickup" drawer | Hold physical cheques for pickup | AP clerk + controller keys | |

## Step-by-step procedure (happy path)

1. Accept the blue mesh bag from the mailroom runner and initial the runner log.
2. Date-stamp the outside of each envelope with today's date.
3. Open MailRoom Pro → **Intake** → **New batch** → date defaults to today → confirm.
4. Open envelopes one at a time at the scanner station:
   1. If the envelope contains no cheque, follow decision **D1**.
   2. If the cheque payee is not Northwind Desk Services (or an acceptable DBA on the wall list), follow decision **D3**.
   3. If the cheque is unsigned, follow exception **E2**.
   4. If the cheque is post-dated, follow exception **E3**.
   5. If the approved scanner station is unavailable, follow exception **E4**.
   6. For an eligible cheque, scan the cheque face and any remittance stub, add the scan to today's MailRoom Pro batch, and write the MailRoom Pro item number lightly in pencil on the remittance stub (not on the cheque face).
5. When all envelopes are processed, run MailRoom Pro → **Close intake batch** and note the batch ID on the paper batch cover sheet.
6. Open LedgerApp → **Deposits** → **New deposit from MailRoom batch** → select today's batch ID.
7. Verify the cheque count and total on screen against the paper cover sheet. If they differ, follow exception **E1** — do not submit.
8. Follow decision **D2** before any submission.
9. Submit the deposit only when D2 directs the AP clerk to submit it. If Rivera must approve, wait for Rivera's approved submission before continuing.
10. After submission, export the deposit confirmation PDF to `\\files\ap\deposits\YYYY-MM-DD-batch.pdf`.
11. Place physical cheques and cover sheet in the sealed pouch, drop into the locked treasury pickup drawer, and initial the drawer log.
12. Return empty blue bag to the mailroom shelf.

## Decision points and branches

| ID | When | Options | Who decides | Next step / path |
|---|---|---|---|---|
| D1 | Envelope has no cheque (invoice only, junk, or misdelivered) | (a) Invoice only → place in "remit advice" tray; (b) Misdelivered personal mail → return to mailroom; (c) Unknown → Rivera review tray | AP clerk | Do not add to MailRoom batch |
| D2 | After counts match, inspect LedgerApp's on-screen approval-status control | (a) Control explicitly shows **no approval required** → AP clerk submits at step 9; (b) Control shows **approval required** → save as pending and notify Rivera; (c) Control is unavailable, blank, or unreliable → do not submit; stop and escalate to Rivera | AP clerk recognizes; Rivera approves or submits | Do not infer "no approval required" from a missing control. Continue at step 10 only after submission |
| D3 | Cheque payee is not on the acceptable payee wall list | Do not scan or deposit; place in Rivera review tray with sticky note | AP clerk | Continue with the next envelope at step 4 |

## Exceptions and edge cases

| Trigger | What to do | Resume point | Escalate if |
|---|---|---|---|
| E1 — Count or total mismatch between MailRoom Pro and LedgerApp | Do not submit. Re-pull batch listing, rescan missing item if needed, fix in MailRoom Pro, refresh LedgerApp import | Step 7 | Cannot reconcile within 30 minutes → Rivera |
| E2 — Unsigned cheque | Do not scan or include in deposit. Place in Rivera review tray with envelope | Continue with the next envelope at step 4 | Customer follow-up is Rivera's path (out of scope) |
| E3 — Post-dated cheque | Hold in "post-date" sleeve labeled with date; do not scan into today's deposit | Continue with the next envelope at step 4 | If date is next-day and volume high, ask Rivera whether early hold is OK |
| E4 — Scanner PC down | Do not use a phone, personal device, or unapproved capture method. Leave the current MailRoom Pro batch open, record its ID on the cover sheet, and hold remaining date-stamped envelopes and any opened items in the locked drawer; document the outage and notify IT | Reopen the **same** batch and resume at step 4 when the approved scanner returns; do not create a second batch | Outage past 14:00 → Rivera decides partial vs full hold |

## Pitfalls and tribal knowledge

| Pitfall or tribal note |
|---|
| New clerks often date-stamp *after* opening and lose track of which envelope arrived today — stamp first. |
| The red mesh bag is facilities hardware returns; processing it "to be helpful" mixes inventories. |
| Pencil item numbers go on the stub, never the cheque face — bank has rejected writing on the MICR area before (per Jordan). |
| Lived practice: Morgan sometimes submits just under the threshold by splitting batches. **Official rule (Rivera): do not split to avoid approval.** This capture follows the official rule. |
| Month-start volume spikes; start by 09:45 or the 15:00 submit target slips. |

## Escalation and who to ask

| Situation | Contact (role; name if allowed) | Channel | Expected response |
|---|---|---|---|
| Cannot reconcile batch (E1) | Controller — Rivera | Teams "AP-Desk" channel or office | Same morning |
| Payee / unsigned / suspicious item | Controller — Rivera | Physical review tray + short note | Same day |
| Mail bag never arrives by 11:00 | Mailroom lead — Chris | Phone extension on wall list | Confirm delay vs missed delivery |
| LedgerApp access failure | IT service desk | Portal ticket type "Finance apps" | Severity per IT matrix |

## Glossary

| Term as used here | Meaning |
|---|---|
| Blue bag | AP incoming payment mail bag from mailroom |
| Cover sheet | Paper tally of count and total for the day |
| MailRoom Pro batch ID | System identifier linking scans to the deposit import |
| Remittance stub | Paper advice accompanying a cheque |
| Treasury pickup drawer | Locked drawer treasury empties each afternoon |

## Source documents and systems of record

| Source | What it authorizes or records | Location / how to find |
|---|---|---|
| Acceptable payee wall list | Which payee lines may be deposited | Laminated sheet above scanner |
| LedgerApp deposit record | Official deposit submission | LedgerApp → Deposits → date |
| MailRoom Pro batch | Image evidence of cheques | MailRoom Pro → Intake → batch ID |
| Drawer log | Physical custody handoff | Clipboard on treasury drawer |

## Open questions / unresolved gaps

| ID | Gap | Why it matters | Owner | Disposition |
|---|---|---|---|---|
| Q2 | Written fallback if the approval-status control is unavailable and Rivera cannot respond before the deposit deadline | D2 safely stops submission, but a business-continuity rule is not yet defined | Rivera | deferred — do not submit; revisit when owner defines a fallback |
| Q3 | Whether foreign-currency cheques ever arrive | No step exists today | Jordan | out of scope — none observed in 18 months; open new capture if one arrives |

## Sign-off

| Role | Name | Date | Acknowledges |
|---|---|---|---|
| SME | Jordan (AP clerk) | 2026-07-15 | Artifact matches lived process for in-scope work at this version |
| Owner (if required) | Rivera (controller) | 2026-07-15 | Artifact is authorized for the stated consumer audience |

### Sign-off statement

> I confirm this version is accurate enough for the capture success definition
> above. Known gaps remain only in **Open questions / unresolved gaps** with
> disposition `deferred` or `out of scope`.

## LLM attachment boundary

This signed example is the canonical process artifact. A real organization
would attach a complete, chat-safe session copy when its LLM chat is not
approved for the canonical copy's names, internal evidence locations, or
other identifiers. That temporary copy would use roles such as `AP clerk` and
`controller`; it would not replace this signed artifact or include the raw
source transcript.

## Revision history

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-07-15 | Sam (facilitator), Jordan (SME) | Initial signed capture after transcript normalization, one mail-day observation, and one correction pass |
