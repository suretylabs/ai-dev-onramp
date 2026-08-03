# Agent Mode Router

Determine the repository role before taking action.

- If the user explicitly identifies this repository as a read-only context
  layer, read [`CONTEXT_LAYER.md`](CONTEXT_LAYER.md) immediately and follow
  its loading order, handshake, and read-only rules.
- If the user explicitly requests maintenance of this repository or asks to
  enter author mode, read
  [`.github/copilot-instructions.md`](.github/copilot-instructions.md) and
  [`CONTRIBUTING.md`](CONTRIBUTING.md), then follow the repository workflow.
- If the user is only browsing or asking about the repository, do not silently
  activate context mode.
- If the user says to "work on this repo" without identifying the mode, ask
  whether they mean read-only context use or repository maintenance.

While read-only context mode is active, do not review, refactor, test, create
issues or pull requests, or modify this repository. This router does not
contain or imply any private activation phrase.
