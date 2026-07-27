# VS Code, GitHub Copilot, and Project Articulation

> Companion: [VS Code and Copilot visual](../visuals/03-vscode-and-copilot.md)

## Outcome

Configure VS Code as the integrated workspace, connect the intended personal GitHub identity to the organization-owned repository already proven from PowerShell, and use the first Copilot session to capture what the developer is actually building before Python or application code is introduced.

VS Code is the integration surface. Git, GitHub, the filesystem, the shell, and Copilot remain distinct systems whose state can be inspected independently.

## Why this phase begins with a known repository

The business organization and remote repository already exist, the intended account is secured, Copilot is active on that exact account through the recorded entitlement path, and the repository has been cloned successfully.

That gives VS Code a stable context on first launch:

```text
Known personal GitHub account
        +
Known Copilot entitlement on that account
        +
Known organization-owned remote repository
        +
Verified local clone
        |
        | code .
        v
VS Code workspace with Git and Copilot context
```

The developer is not opening an empty editor and being asked to invent a modern workflow. They are opening a project whose identity and location are already known.

## Install VS Code

Use the current official VS Code installer or official WinGet package. For a single-user development machine, the user installer is often appropriate because it supports per-user updates without requiring elevation, but the LLM should verify current official guidance and the machine's management policy.

When using the interactive installer, explain material options such as:

- adding `code` to PATH;
- adding “Open with Code” context-menu entries;
- file associations;
- desktop shortcuts;
- per-user versus all-user installation.

Adding `code` to PATH is important because it lets the developer and the AI open a known directory as a workspace from PowerShell.

After installation, open a fresh `pwsh` session and verify the `code` executable and version.

## Open the existing repository

From the verified repository root, use:

```text
code .
```

The guiding LLM should generate the actual command at runtime and then verify:

- the expected folder is the workspace root;
- the Explorer shows the remote baseline files;
- Source Control recognizes the existing Git repository;
- the current branch is `main`;
- the workspace is clean;
- the integrated terminal starts in the repository root.

## Workspace model

Demonstrate the relationship:

```text
Windows folder
    -> opened by VS Code as a workspace folder
    -> contains the Git working tree
    -> contains the project files
    -> later contains a uv-managed Python project
```

A VS Code workspace can contain one folder or several. The first project should use one repository folder so the boundaries remain explicit.

## Initial extensions

Install only the extensions needed for the current stack:

- GitHub Copilot;
- Python;
- Pylance;
- Ruff.

VS Code includes Git integration, but Git for Windows remains the source-control implementation underneath it.

Do not install a broad extension pack or multiple AI assistants without a reason. Each extension adds behavior, settings, permissions, update surface, and possible conflicts.

## Sign into the same GitHub account

The Copilot entitlement was established in `03-github-foundation.md`, and `gh` authentication was verified in `04-git-and-github-cli.md`. Now verify the VS Code identity separately.

Confirm:

- VS Code is signed into the intended GitHub account;
- the username matches the account used by `gh`;
- Copilot reports the organization-assigned entitlement as active;
- the current repository remote belongs to the expected organization;
- Copilot can use the organization-owned repository context under the intended policy;
- no second GitHub account has been selected accidentally.

A successful sign-in in one component does not authenticate every other component.

## Integrated terminal

Configure PowerShell 7 as the normal terminal profile. Then verify inside VS Code:

- the shell reports PowerShell 7;
- `git` and `gh` resolve to the same installations proven externally;
- the terminal begins in the intended workspace root;
- `git status` matches the Source Control panel;
- later, `uv` and Python commands resolve after those tools are installed.

Do not use Git Bash as the default terminal for this guide.

## Source Control panel: connect UI to Git state

Use one small documentation edit to connect the graphical view to Git's actual state:

1. Modify `README.md` in VS Code.
2. Save the file.
3. Observe the change in Source Control.
4. Run `git status` in the terminal.
5. Compare the UI representation with Git's output.
6. View the diff.
7. Stage in one interface and verify state in the other.
8. Unstage if appropriate and verify again.

The Source Control panel is a view and control surface over Git. It is not a second version-control database.

## First Copilot session: let the developer explain the project

The repository contains a small bootstrap `.github/copilot-instructions.md`. Its purpose is to make the first Copilot interaction a project-discovery session rather than a code-generation exercise.

Do not ask Copilot to “write a Python app.”

Open Copilot Chat in the repository and begin with a prompt equivalent to:

> Read the current repository, beginning with `docs/BOOTSTRAP_STATE.md` when present, then `.github/copilot-instructions.md` and `README.md`. Restate where the setup currently stands and ask whether I want to resume the recorded path. Do not create application code. I am going to explain the business project in the language I naturally use. Ask focused questions, distinguish what I state from what you infer, and help me create a durable project brief, repository instructions, and an updated next checkpoint that accurately capture the work.

The developer should then explain, in their own terms:

- what the current business process does;
- where existing platforms, databases, documents, programs, people, and manual steps fit;
- what is painful, slow, risky, repetitive, or newly possible;
- who uses the result and what decision or action it supports;
- the first useful outcome they want;
- known inputs and outputs;
- audit, traceability, security, deployment, or operational constraints;
- what should wait until later;
- what they know is uncertain.

The guiding LLM should not force this into a large questionnaire. Questions are welcome throughout the discussion. Ask one coherent cluster at a time, follow the actual explanation, and ask additional focused questions whenever they resolve a material ambiguity or expose a boundary the developer has not yet described.

## Historical vocabulary during project discovery

The developer may describe the project using terms rooted in earlier development environments, a particular vendor stack, or established internal vocabulary.

Copilot and the guiding LLM should:

1. understand the behavior they mean;
2. preserve the developer's explanation;
3. identify the modern term or terms that now separate the concept;
4. explain any meaningful boundary;
5. confirm the mapping before rewriting the developer's description.

Example:

> “When you say the program directory, I think you mean both the physical source folder and the unit we would now treat as a repository-backed project. I will keep those distinct in the documentation. Is that the behavior you mean?”

Do not interrupt every sentence to correct terminology. Translate where the distinction affects design, operation, or communication.

## Create the durable project context

From the discussion, create or refine:

```text
docs/PROJECT_BRIEF.md
.github/copilot-instructions.md
docs/BOOTSTRAP_STATE.md
```

Use the supplied templates as starting structures, not as forms that must be completed mechanically.

### `docs/PROJECT_BRIEF.md`

This is the fuller business and delivery record. It should capture:

- business context and current process;
- intended user and decision or action;
- problem and opportunity;
- first useful capability;
- sources and outputs;
- constraints and evidence requirements;
- non-goals;
- open questions;
- initial acceptance criteria.

It should preserve uncertainty explicitly rather than inventing a complete specification.

### `.github/copilot-instructions.md`

Replace the bootstrap-only content with a concise repository operating contract that points to the project brief and tells Copilot:

- what the project is and why it exists;
- what the first useful capability is;
- what remains unresolved;
- what must not be done yet;
- how to treat credentials and business data;
- how to preserve scope;
- that Python and uv commands are still provisional until the next phase establishes them.

At this point, entries such as project package structure, execution commands, validation commands, and exact dependencies may remain marked:

```text
TBD — establish during the Python 3.14 and uv phase.
```

That is better than fabricating commands.

## Copilot must restate its understanding

Before the developer approves the documents, require Copilot to:

1. restate the business problem;
2. identify the intended user and first useful result;
3. distinguish repository facts from AI inference;
4. identify ambiguities that would materially change the first vertical slice;
5. list explicit non-goals;
6. make no code or configuration changes beyond the agreed documentation.

The developer should correct the restatement. Durable corrections belong in the repository files, not only in the chat.

The acceptance question is:

> If a new AI session read only this repository, would it understand what is being built, why it matters, the first useful result, the current boundaries, and what is still unknown?

## Review and commit the project contract

Before implementation:

- inspect both Markdown files in VS Code;
- review the diff;
- correct language that sounds generic, inflated, or unlike the actual project;
- verify that no credentials, confidential records, customer documents, or production data were included;
- stage the documentation intentionally;
- inspect the staged diff;
- commit and push.

This is the first meaningful AI-assisted repository change. Its output is project understanding, not code.

## Copilot operating modes

UI labels evolve. Teach the enduring behaviors rather than relying on one button name.

### Explanation mode

Use for:

- translating terminology;
- explaining a command or diagnostic;
- inspecting a file;
- comparing approaches;
- identifying where behavior is defined.

### Planning mode

Use before a nontrivial change. Require:

- intended outcome;
- files likely affected;
- assumptions;
- edge cases;
- validation plan;
- explicit out-of-scope items.

### Editing mode

Use for a small, bounded change. After the edit:

- inspect the diff;
- run targeted validation;
- review any new dependency or configuration change;
- do not accept generated code solely because it runs.

### Agentic mode

Use only after repository instructions and validation commands exist. Define the task boundary and require a final evidence report.

## Prompting patterns to establish

The developer should become comfortable saying:

> Inspect the current repository and explain where this behavior is implemented. Do not change files.

> Give me only the next PowerShell command. I will paste the full output before we continue.

> Translate what I am calling the source directory into the precise Git, VS Code, and Python terms that apply here.

> Propose a plan. Name the files you expect to change and the validation you will run. Do not edit yet.

> Make only the agreed change. Then show me the diff and run the targeted tests.

> Do not assume the command succeeded. Evaluate the output I pasted.

> Tell me what you know from evidence, what you inferred, and what remains unverified.

## Repository instructions evolve in two passes

The initial project-context pass is completed in this phase.

The second pass occurs after Python and uv are established. At that point, update `.github/copilot-instructions.md` with:

- authoritative Python version;
- uv-only dependency and execution commands;
- source and test layout;
- Ruff, Pyright, and pytest commands;
- repository-specific validation and security rules.

Repository instructions should be concise enough to remain useful and specific enough to prevent repeated exploration and generic tooling mistakes.

### `docs/BOOTSTRAP_STATE.md`

This is the running operational record, not the business specification. Copilot should update it with:

- the phase and objective now in progress;
- the project-articulation gate result;
- open questions that still affect the next step;
- optional work deferred;
- the exact resume point;
- the next paths the developer should be offered and the recommended path.

Keep unresolved business content in `docs/PROJECT_BRIEF.md`; keep durable architecture and toolchain decisions in `docs/DECISIONS.md`. Do not make the state document a duplicate of either one.

## Settings discipline

Prefer repository or workspace settings for project-specific behavior. Use VS Code user settings only when they genuinely apply to every project.

The LLM should explain whether a setting is:

- machine-wide;
- VS Code user-wide;
- workspace-specific;
- repository-tracked;
- generated and untracked.

Do not copy old VS Code setting keys blindly. Verify current extension documentation because settings and extension responsibilities change.

## Acceptance gate

This phase passes when:

- `code .` opens the intended cloned repository;
- Source Control recognizes the same Git state as the terminal;
- the integrated terminal uses PowerShell 7;
- VS Code and `gh` align to the developer's intended personal account, while Copilot and the repository align to the intended business organization;
- Copilot is active before application coding begins;
- the developer has explained the real project in their own terms;
- Copilot has distinguished fact from inference and surfaced material ambiguities;
- `docs/PROJECT_BRIEF.md` and the first project-specific `.github/copilot-instructions.md` have been reviewed, committed, and pushed;
- no application code or dependency was introduced prematurely;
- Python, Pylance, and Ruff extensions are installed and ready for the next phase.

## Transition checkpoint

Update `docs/BOOTSTRAP_STATE.md` with the verified editor, terminal, account, Copilot, and project-articulation state. Record unresolved business questions in `docs/PROJECT_BRIEF.md`, not as invented answers.

Then ask whether the developer would like to:

1. continue to Python 3.14 and uv, using the now-reviewed project context; or
2. remain in project articulation to refine the first useful delivery slice before installing the Python toolchain.

Recommend continuing when the project brief is accurate enough to constrain the first implementation. Recommend more articulation when input, output, user, or first useful result is still materially ambiguous.
