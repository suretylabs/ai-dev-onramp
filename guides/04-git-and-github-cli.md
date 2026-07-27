# Git for Windows and GitHub CLI

> Companion: [Local toolchain visual](../visuals/02-local-toolchain.md)

## Outcome

Install and verify the local Git and GitHub CLI tools, authenticate the intended personal account, verify its access to the established business organization, clone the known organization-owned repository, and prove a complete local-to-remote round trip.

This phase does not create the GitHub identity, organization, Copilot entitlement, or repository ownership boundary. Those were established in `03-github-foundation.md`. Its purpose is to attach the Windows machine to that known organization-owned remote state and make the distributed-version-control model observable.

## Installation order

A practical order is:

1. Inspect the machine for existing Git and `gh` installations.
2. Install Git for Windows if needed.
3. Open a fresh PowerShell 7 session and verify `git`.
4. Install GitHub CLI if needed.
5. Verify `gh`.
6. Authenticate `gh` to the exact account recorded in the GitHub foundation phase.
7. Clone the known `ORGANIZATION/REPOSITORY` remote.
8. Inspect Git identity and repository configuration.
9. Make one documentation-only change and observe every Git state.
10. Push and verify the result on GitHub.

The LLM may adjust the mechanics based on actual machine state, but it should preserve the verified-state sequence.

## Inspect before installation

Generate read-only PowerShell commands to determine:

- whether `git` resolves and which executable is found;
- Git version;
- whether `gh` resolves and which executable is found;
- GitHub CLI version;
- whether multiple installations are present on PATH;
- existing system and global Git configuration origins;
- existing Git identity;
- existing GitHub CLI authentication state.

Do not install duplicates or overwrite configuration until the existing state has been interpreted.

## Git for Windows installer: decisions to explain

The exact screens and labels vary by release. Ask for the actual option text or screenshots. Material decision areas commonly include:

### Default editor

VS Code may not yet be installed. Do not let this choice freeze the process.

Choose a simple available editor deliberately, then reconfigure Git to use VS Code after the editor phase. Explain that Git sometimes invokes an editor for commit messages, merge messages, or interactive operations. The editor setting does not make that application the version-control engine.

If VS Code is already present, selecting it is appropriate.

### PATH integration

Choose an option that allows `git` to be called from PowerShell and third-party applications. The target workflow depends on Git being visible to `pwsh`, VS Code, and AI-assisted terminal operations.

### SSH implementation

Explain bundled OpenSSH versus the Windows implementation if the installer asks. Initial GitHub access will normally use HTTPS through GitHub CLI, so SSH is not required for the first proof. Choose based on actual corporate policy or an established SSH strategy rather than habit.

### HTTPS/TLS backend

Explain whether Git will use its bundled TLS stack or the Windows certificate store. On a managed Microsoft environment, Windows certificate integration may matter for corporate roots and proxies. Use the actual environment to decide.

### Line-ending conversion

Explain three distinct layers:

1. Windows and VS Code can edit LF files correctly.
2. Git can apply global checkout and commit transformations.
3. The repository can define explicit policy in `.gitattributes`.

For modern Python and potentially cross-platform execution, prefer repository-owned line-ending policy over opaque global conversion. Do not create a surprising machine-wide rule without explaining it.

A minimal `.gitattributes` that normalizes text to LF in the repository while leaving Windows-only scripts alone:

```gitattributes
* text=auto eol=lf

*.ps1 text eol=crlf
```

Commit this file once, near the start of a project, rather than relying on each developer's global `core.autocrlf` setting to agree.

### Terminal behavior

The primary shell is PowerShell 7 in Windows Terminal. If the Git installer asks how Git Bash should host its terminal, explain that the choice affects Git Bash behavior, not the normal shell for this guide.

### Credential helper

Keep Git Credential Manager enabled unless corporate policy requires another mechanism. Credentials should not be stored in plain-text configuration or pasted into chat.

### Symbolic links and advanced filesystem features

Do not enable advanced options merely because they sound modern. Enable them when the project requires them and the Windows security or developer-mode implications are understood.

## Verify installation in a fresh shell

After installation, close and reopen PowerShell 7 so PATH changes are real rather than assumed.

Generate read-only commands to capture:

- Git version and executable path;
- GitHub CLI version and executable path;
- system and global Git configuration with origins;
- current default-branch setting;
- credential-helper configuration;
- current authentication status.

Record verified versions and paths in `BOOTSTRAP_STATE.md`.

## Authenticate GitHub CLI

Use `gh auth login` or the current supported equivalent. Prefer the browser or device flow. Do not ask anyone to paste a token into chat.

The guiding LLM should explicitly verify:

- the hostname is the intended GitHub service;
- the account matches the username recorded in `03-github-foundation.md`;
- that account can see the intended organization and repository;
- the protocol choice is intentional;
- authentication is not occurring under a stale second account;
- `gh auth status` reports usable access.

Explain the separation:

- Git commit identity becomes author metadata in commits.
- GitHub authentication authorizes operations against the service.
- Copilot access is assigned to the developer's account by the organization.
- Repository ownership belongs to the organization.
- These should align intentionally, but they are not the same setting.

## Clone the known remote repository

Use the canonical `ORGANIZATION/REPOSITORY` identifier recorded in the previous phase.

Before cloning, choose and record a stable development root, for example:

```text
C:\dev
```

The actual path should fit the machine and company policy. Avoid OneDrive-synchronized folders unless there is a deliberate reason and the interaction between synchronization, `.git`, and local environments is understood.

Generate one clone command for the actual state. Then verify:

- the expected folder exists;
- the current directory is the repository root;
- `.git` exists as the local repository metadata boundary;
- `git remote -v` points to the expected organization and repository;
- the checked-out branch is `main`;
- `git status` is clean;
- the files visible locally match the remote baseline.

This is the first proof that the local machine is attached to the intended GitHub project.

## Configure Git identity deliberately

Review the commit-name and commit-email decision from the GitHub foundation phase.

Ask which scope is correct:

- **global** when the identity should apply to every repository on the machine;
- **repository-local** when this project requires a specific business identity or email.

If email privacy was selected, use the exact GitHub-provided `noreply` address associated with the account. Do not guess its format.

After configuration, verify effective values and their origins from inside the repository.

## First local-to-remote repository exercise

Use a documentation-only change so Git mechanics remain visible without implementation complexity.

The guiding LLM should conduct these transitions one at a time:

1. Inspect `git status` while clean.
2. Make one small change to `README.md` or the bootstrap Copilot instructions.
3. Save the file.
4. Inspect status and identify the modified working-tree file.
5. Inspect the unstaged diff.
6. Stage the file.
7. Inspect status and identify the staged state.
8. Inspect the staged diff.
9. Commit locally with a clear message.
10. Inspect the local log.
11. Confirm the local branch is ahead of the remote.
12. Push.
13. Confirm the local working tree is clean.
14. Verify the commit and file change in GitHub's web interface.

Do not compress this into a compound command. The objective is to observe where each state lives.

## The state model

Use the actual exercise to establish:

```text
Working tree
    | git add
    v
Staging area / index
    | git commit
    v
Local repository history
    | git push
    v
GitHub remote repository
```

Saving, staging, committing, and pushing are four different operations.

The remote was created first in this onboarding sequence, but Git is still distributed: complete version history exists locally after cloning, and commits are created locally before being transferred.

## Essential command vocabulary

Teach commands when used, not as a memorization list.

| Command family | Purpose |
|---|---|
| `git status` | Inspect working-tree and staging state. |
| `git diff` | Inspect unstaged changes. |
| `git diff --staged` | Inspect the exact staged change. |
| `git add` | Select content for the next commit. |
| `git commit` | Record a local snapshot and message. |
| `git log` | Inspect local commit history. |
| `git fetch` | Retrieve remote references without integrating them. |
| `git pull` | Retrieve and integrate according to configured strategy. |
| `git push` | Transfer local commits to a remote. |
| `gh auth` | Manage GitHub CLI authentication. |
| `gh repo` | View, clone, or manage GitHub repositories. |
| `gh issue` / `gh pr` | Work with GitHub issues and pull requests. |

## Branch introduction gate

Do not require branch fluency before the first successful round trip.

After the clean commit and push, demonstrate one small branch exercise either in this phase or immediately after VS Code is integrated:

- create a short-lived branch;
- make one bounded documentation change;
- compare the branch with `main`;
- push the branch;
- open a pull request;
- inspect the diff and conversation surface;
- merge;
- update local `main`;
- delete the merged branch locally and, if configured, verify remote cleanup.

If repository protection requiring pull requests was intentionally deferred in the GitHub foundation phase, this exercise is the point at which to decide whether to enable it.

## Project articulation is next, not application code

After the local round trip is proven, proceed to `05-vscode-and-copilot.md`.

The repository already contains bootstrap Copilot instructions telling the AI to begin with project discovery. Once VS Code and Copilot are connected, the developer will explain the actual business project and the AI will create or refine:

```text
docs/PROJECT_BRIEF.md
.github/copilot-instructions.md
```

Do not initialize Python or generate application code before that project-articulation gate is complete.

## Acceptance gate

This phase passes when:

- `git` and `gh` resolve from a fresh `pwsh` session;
- versions and executable paths are recorded;
- `gh` is authenticated to the exact intended GitHub account;
- the known remote repository has been cloned into the deliberate development root;
- the local remote URL, branch, and working tree are correct;
- Git commit identity and email privacy are intentional;
- the developer has observed modified, staged, committed, pushed, and clean states;
- one local commit is visible on GitHub;
- no credentials or recovery data were exposed;
- the repository is ready to open in VS Code for project discovery.

## Transition checkpoint

Once the local-to-remote round trip is proven, move the running state document into the cloned repository as `docs/BOOTSTRAP_STATE.md` if that has not already been done, commit it, and treat that repository copy as canonical.

Then ask whether the developer would like to:

1. open the repository in VS Code and begin the Copilot-assisted project-articulation phase; or
2. complete the optional short-lived branch and pull-request exercise first.

Recommend moving to VS Code unless branch mechanics are still materially unclear. Record a deferred branch exercise and its revisit condition rather than losing it.
