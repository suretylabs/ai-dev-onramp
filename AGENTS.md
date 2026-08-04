# Agent Mode Router

Determine the repository role before taking action.

- If the user points specifically at the Consultant Process-Capture Lane as
  their guide, coach, or read-only context for capturing a business process
  with an SME, read
  [`consultant-lane/CONTEXT_LAYER.md`](consultant-lane/CONTEXT_LAYER.md)
  immediately and follow its loading order, handshake, and read-only rules.
  Soft process-capture intent counts; formal "mount context layer" wording is
  not required.
- If the user points at this repository as their guide, coach, onboarding
  path, setup help, or read-only context for developer setup, read
  [`CONTEXT_LAYER.md`](CONTEXT_LAYER.md) immediately and follow its loading
  order, handshake, and read-only rules. Soft guide intent counts; formal
  "mount context layer" wording is not required.
- If the user explicitly requests maintenance of this repository or asks to
  enter author mode, read
  [`.github/copilot-instructions.md`](.github/copilot-instructions.md) and
  [`CONTRIBUTING.md`](CONTRIBUTING.md), then follow the repository workflow.
- If the user is only browsing or asking what the repository is, summarize it
  without activating context mode.
- If the user says to "work on this repo" without identifying the mode, ask
  whether they mean read-only guide/context use or repository maintenance.

While read-only context mode is active, do not review, refactor, test, create
issues or pull requests, or modify this repository. This router does not
contain or imply any private activation phrase.
