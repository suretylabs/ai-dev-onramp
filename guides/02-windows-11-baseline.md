# Windows 11 Baseline

> Companion: [Local toolchain visual](../visuals/02-local-toolchain.md)

## Outcome

Establish a native Windows development baseline with:

- current Windows updates;
- Windows Terminal;
- PowerShell 7 available as `pwsh`;
- a deliberate local development directory;
- WinGet available where practical;
- tool installation and version state recorded.

This phase does not install the full development stack in one batch.

## Initial state interview

The guiding LLM should ask only what affects the installation path:

- Is this a personally controlled Windows 11 machine or a managed corporate machine?
- Is the account a local administrator?
- Is OneDrive redirecting or synchronizing Documents/Desktop?
- Is there a corporate proxy, VPN, endpoint security product, or software portal?
- Is the processor x64 or ARM64?
- Does the developer prefer interactive installers for the first pass, CLI installation, or a deliberate mixture?

Do not ask about the business project yet unless it changes security or database access requirements.

## Inspect before installing

Generate read-only PowerShell commands, one at a time, to establish:

- Windows edition, build, and architecture;
- current shell identity and version;
- presence and version of Windows Terminal;
- presence and version of `winget`;
- current PATH visibility for `pwsh`, `git`, `gh`, `code`, `uv`, and Python executables;
- whether a development directory already exists.

Record actual output in `BOOTSTRAP_STATE.md`.

## PowerShell 7 versus Windows PowerShell

Windows 11 may expose two related shells:

| Command | Product | Role in this guide |
|---|---|---|
| `powershell.exe` | Windows PowerShell 5.1 | Legacy Windows component retained for compatibility. |
| `pwsh.exe` | PowerShell 7 | Current cross-platform PowerShell used for development. |

PowerShell 7 installs side-by-side; it does not replace Windows PowerShell 5.1.

The guiding LLM should:

1. verify whether `pwsh` already resolves;
2. install the current stable PowerShell 7 release if required, using an official Microsoft-supported path;
3. open a fresh terminal session;
4. verify version and executable path;
5. make PowerShell 7 the preferred Windows Terminal profile if the developer agrees.

Do not permanently relax the machine execution policy merely to make ordinary development easier. Use process-scoped or command-scoped exceptions only when an official installer requires them, and explain the scope.

## Development directory

Choose a simple local path that is:

- outside synchronized OneDrive folders;
- writable without administrator elevation;
- short enough to avoid unnecessary Windows path friction;
- dedicated to source repositories.

A conventional example is `C:\dev`, but the LLM should ask before creating it.

Explain the modern role:

> This is the parent directory that will contain multiple repository working trees. It is not itself required to be a Git repository or Python project.

Do not put secrets or business data in the source root by default.

## Installation strategy: manual understanding plus CLI leverage

Use a hybrid strategy.

### Interactive installation is useful when

- the installer has consequential options;
- the developer wants to understand machine integration;
- file associations, PATH behavior, shell integration, or credential helpers are being selected;
- a corporate machine presents policy-specific choices.

### CLI installation is useful when

- the package has a well-defined official WinGet identity;
- the install is straightforward;
- the command output is useful evidence;
- the goal is repeatability.

For the first setup, Git for Windows is a good candidate for a guided interactive installer because its options expose important source-control behavior. Repeated machines can later be automated.

## Installer decision rule

Never tell the developer to accept all defaults without examining the screen.

For each material choice:

- state what subsystem it affects;
- state whether the choice is global or project-local;
- state the recommended selection;
- explain why that selection fits a native Windows + PowerShell + VS Code + GitHub workflow;
- note how it can be changed later.

## Fresh-shell rule

After installing any tool that modifies PATH:

1. close the relevant terminal session;
2. open a new `pwsh` session;
3. verify command resolution and version;
4. record the result.

Do not diagnose a new installation from a terminal that predates the PATH change until a fresh shell has been tried.

## Baseline acceptance gate

This phase passes when:

- Windows architecture is known;
- `pwsh` resolves in a new terminal and reports the intended stable version;
- `winget` status is known;
- the development root exists at an agreed location;
- the current shell opens in that location without elevation;
- `BOOTSTRAP_STATE.md` records the evidence and any corporate constraints.


## Transition checkpoint

After the acceptance gate is evaluated, update `BOOTSTRAP_STATE.md` with the verified machine and shell state, any corporate-device constraints, and the exact development-root path.

Then ask whether the developer would like to:

1. continue to the GitHub organization foundation, which is the planned next dependency; or
2. spend additional time on the optional Windows Terminal/PowerShell orientation before creating online accounts.

Recommend continuing to GitHub when `pwsh`, the fresh-shell model, and the development root are understood. If the gate did not pass, offer troubleshooting now or pausing with the blocker and resume point recorded.
