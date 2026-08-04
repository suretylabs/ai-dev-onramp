# Consultant Process-Capture Templates

Copy the blank template into the destination knowledge store or repository
for the organization whose process is being captured. Keep this public
repository's copies generic; real process content lives with the client or
internal owner.

| Template | Typical target path | Purpose |
|---|---|---|
| [PROCESS_CAPTURE.md](PROCESS_CAPTURE.md) | `docs/processes/<process-slug>.md` or the team's knowledge store | Blank structure for one business process. |
| [PROCESS_CAPTURE.example.md](PROCESS_CAPTURE.example.md) | reference only — do not treat as a real process | Fully synthetic filled example showing the intended shape. |

## Usage rule

Do not invent content to fill empty sections. Leave unknowns in **Open
questions / unresolved gaps** until the SME supplies them or the scope is
explicitly reduced. Retain raw transcripts, notes, screenshots, and other
source evidence separately in an approved client location; use the
`PROCESS_CAPTURE.md` provenance table to reference them rather than embedding
large source material in the durable process artifact.

When a process capture is attached to an LLM, use the canonical signed file
only where its contents are approved for that chat. Otherwise attach a
complete chat-safe session copy that replaces prohibited identifiers and
locations without becoming a second canonical process artifact.
