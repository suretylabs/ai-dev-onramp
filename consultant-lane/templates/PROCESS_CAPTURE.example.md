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
- **Ends when**: Deposit batch is submitted in LedgerApp and the physical cheque packet is placed in the locked "treasury pickup" drawer.
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
4. Open envelopes one at a time at the scanner station. For each envelope that contains a cheque payable to Northwind Desk Services (or acceptable DBA on the wall list):
   1. Scan the cheque face and any remittance stub.
   2. In MailRoom Pro, add the scan to today's batch.
   3. Write the MailRoom Pro item number lightly in pencil on the remittance stub (not on the cheque face).
5. If the envelope contents are not a cheque, follow decision **D1**.
6. When all envelopes are processed, run MailRoom Pro → **Close intake batch** and note the batch ID on the paper batch cover sheet.
7. Open LedgerApp → **Deposits** → **New deposit from MailRoom batch** → select today's batch ID.
8. Verify the cheque count and total on screen against the paper cover sheet. If they differ, follow exception **E1** — do not submit.
9. Submit the deposit batch in LedgerApp (Jordan may submit under normal limits; see **D2**).
10. Export the deposit confirmation PDF to `\\files\ap\deposits\YYYY-MM-DD-batch.pdf`.
11. Place physical cheques and cover sheet in the sealed pouch, drop into the locked treasury pickup drawer, and initial the drawer log.
12. Return empty blue bag to the mailroom shelf.

## Decision points and branches

| ID | When | Options | Who decides | Next step / path |
|---|---|---|---|---|
| D1 | Envelope has no cheque (invoice only, junk, or misdelivered) | (a) Invoice only → place in "remit advice" tray; (b) Misdelivered personal mail → return to mailroom; (c) Unknown → Rivera review tray | AP clerk | Do not add to MailRoom batch |
| D2 | LedgerApp shows deposit total at or above the on-screen approval threshold | (a) Under threshold → AP clerk submits; (b) At/over threshold → save as pending and notify Rivera | AP clerk recognizes; Rivera approves | Do not bypass approval |
| D3 | Cheque payee is not on the acceptable payee wall list | Do not deposit; place in Rivera review tray with sticky note | AP clerk | Out of happy path |

## Exceptions and edge cases

| Trigger | What to do | Resume point | Escalate if |
|---|---|---|---|
| E1 — Count or total mismatch between MailRoom Pro and LedgerApp | Do not submit. Re-pull batch listing, rescan missing item if needed, fix in MailRoom Pro, refresh LedgerApp import | Step 8 | Cannot reconcile within 30 minutes → Rivera |
| E2 — Unsigned cheque | Do not include in deposit. Place in Rivera review tray with envelope | Continue other items | Customer follow-up is Rivera's path (out of scope) |
| E3 — Post-dated cheque | Hold in "post-date" sleeve labeled with date; do not scan into today's deposit | End of day log note | If date is next-day and volume high, ask Rivera whether early hold is OK |
| E4 — Scanner PC down | Use phone photo only if Rivera approves for that day; otherwise hold unopened stamped envelopes in locked drawer and document outage | Resume at step 3 when scanner returns | Outage past 14:00 → Rivera decides partial vs full hold |

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
| Q1 | Exact LedgerApp approval threshold amount changes periodically and is not printed on the wall list | New clerk must trust on-screen flag; offline contingency unclear if LedgerApp is up but flag missing | Rivera | deferred — train "believe the on-screen threshold flag"; revisit if flag fails |
| Q2 | Whether foreign-currency cheques ever arrive | No step exists today | Jordan | out of scope — none observed in 18 months; open new capture if one arrives |

## Sign-off

| Role | Name | Date | Acknowledges |
|---|---|---|---|
| SME | Jordan (AP clerk) | 2026-07-15 | Artifact matches lived process for in-scope work at this version |
| Owner (if required) | Rivera (controller) | 2026-07-15 | Artifact is authorized for the stated consumer audience |

### Sign-off statement

> I confirm this version is accurate enough for the capture success definition
> above. Known gaps remain only in **Open questions / unresolved gaps** with
> disposition `deferred` or `out of scope`.

## Revision history

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-07-15 | Sam (facilitator), Jordan (SME) | Initial signed capture after one mail-day observation and one correction pass |
