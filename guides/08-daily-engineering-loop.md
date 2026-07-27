# Daily AI-Assisted Engineering Loop

> Companion: [Daily engineering loop visual](../visuals/05-daily-engineering-loop.md)

## Purpose

Turn the installed tools into a disciplined operating system for real development.

The objective is not to make the developer dependent on AI for every keystroke. It is to make the AI useful for navigation, translation, planning, implementation, and validation while keeping engineering judgment and evidence visible.

## Start-of-session state check

At the beginning of a work session, the AI should read `docs/BOOTSTRAP_STATE.md` first and restate the recorded phase, last verified checkpoint, blocker, deferred work, and proposed resume point. It should then verify whether the developer wants to resume that path or change direction.

After that orientation, establish:

- current repository and branch;
- working-tree status;
- remote synchronization state;
- current task or issue;
- relevant project instructions;
- whether the environment is synchronized;
- latest test status if known.

Do not begin a new task on unexplained local changes. Re-verify any recorded state that could have changed outside the prior session, then update the state document if reality differs.

## Task contract

For any change larger than a trivial edit, define:

- problem;
- intended behavior;
- in-scope files or components;
- out-of-scope items;
- acceptance criteria;
- validation commands;
- data/security constraints.

Store meaningful task contracts in an issue, project brief, or repository document rather than only in chat.

## Normal change cycle

```text
Inspect -> Plan -> Branch -> Edit -> Diff -> Validate -> Commit -> Push -> Review
```

### Inspect

Ask the AI to read the relevant repository files and identify the current behavior. It should cite file paths and distinguish evidence from inference.

### Plan

Require a bounded plan. The AI should name likely files, dependencies, risks, and tests before editing.

### Branch

Use a branch for a coherent unit of work once branch mechanics are understood. Keep branch names descriptive and short.

### Edit

Allow the AI to make a small vertical change. Avoid unrelated cleanup. If adjacent problems are noticed, record them without silently expanding scope.

### Diff

Review the actual diff. Ask:

- Did the implementation match the contract?
- Did configuration or dependencies change?
- Were secrets or generated files introduced?
- Is the code more complex than the problem requires?
- Did the AI change anything it did not mention?

### Validate

Run targeted checks first, then the agreed broader checks. The AI must report exact commands and outcomes.

### Commit

Stage intentionally. Review the staged diff, then commit a coherent state. A commit message should explain the change, not the mechanics of editing.

### Push and review

Push the branch. Use `gh` or GitHub to open a pull request when the change warrants review or when practicing the workflow. Verify CI rather than assuming local success guarantees remote success.

## AI request patterns

### Repository orientation

> Read the project instructions, README, project definition, and relevant source files. Explain the architecture that matters to this task. Do not edit anything.

### Terminology bridge

> I would historically describe this as a source-directory/build problem. Map that to the precise Git, Python, and VS Code concepts in this repository before proposing a fix.

### Command gating

> Give me one PowerShell command that inspects the current state. I will return the complete output. Do not provide the next command yet.

### Plan before edit

> Propose the smallest implementation plan that satisfies these acceptance criteria. Name the files you expect to touch and the tests you will run. Do not edit yet.

### Controlled implementation

> Implement only the agreed plan. Do not refactor adjacent code. Afterward, show the diff summary and run the targeted validation.

### Evidence handoff

> Report what changed, what commands ran, their results, what remains unverified, and any decision I need to make.

## Validation hierarchy

Use the project’s actual configuration, but the conceptual order is:

1. import or syntax-level execution;
2. targeted test;
3. Ruff formatting/linting;
4. Pyright;
5. relevant pytest subset;
6. full test suite when warranted;
7. manual end-to-end proof;
8. CI result after push.

Do not rerun the largest check repeatedly when a smaller targeted check will isolate the issue.

## Dependency discipline

Before adding a package, the AI should answer:

- What capability is missing?
- Is it already provided by the standard library or an existing dependency?
- Does the package support Python 3.14 and Windows?
- What native binaries or drivers does it require?
- Is it maintained?
- Does it affect licensing or security posture?
- Can it be tested without production systems?

All project dependencies are added through uv and reviewed in `pyproject.toml` and `uv.lock`.

## Configuration discipline

Classify configuration by scope:

| Scope | Examples |
|---|---|
| Machine | PATH, installed applications, Windows certificate store. |
| User | Git identity, VS Code user preferences. |
| Repository | `.gitattributes`, `.gitignore`, `pyproject.toml`, Copilot instructions. |
| Environment | `.env`, process variables, credentials. |
| Runtime | CLI flags, configuration files, database connection choices. |

The AI should not solve a repository problem with a machine-global setting unless that scope is deliberate.

## End-of-session handoff

At the end of a session:

1. Update the canonical `docs/BOOTSTRAP_STATE.md` directly when the AI has repository write access; otherwise provide the smallest exact edit needed and verify that the developer saved it.
2. Produce:
   - current branch and working-tree state;
   - commits created and pushed;
   - validation results;
   - decisions made;
   - unresolved errors or warnings;
   - optional work deferred;
   - the exact resume point;
   - any update required in `docs/DECISIONS.md` or `docs/PROJECT_BRIEF.md`.
3. Present a transition checkpoint. Examples:
   - continue the current implementation slice;
   - stop coding and review the diff/architecture;
   - move to the next accepted slice;
   - pause with a clean, recorded handoff.

The handoff should allow another LLM session to continue by reading the state document first, without reconstructing the entire history from chat.

## Mature operator standard

The developer is operating effectively when they can:

- describe the desired state without knowing every command;
- ask the AI to produce the next command and evaluate evidence;
- recognize when the AI has crossed a state boundary;
- inspect diffs and tool output;
- distinguish local, generated, committed, and remote state;
- require validation before accepting a change;
- use repository instructions to shape future AI behavior;
- intervene when a proposal is architecturally wrong even if the syntax is correct.
