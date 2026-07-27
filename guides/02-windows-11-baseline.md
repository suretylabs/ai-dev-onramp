# Windows 11 Baseline

> Companion: [Local toolchain visual](../visuals/02-local-toolchain.md)

> Prefer a Linux-side toolchain on the same Windows 11 host instead? See the [WSL2 alternative path](alt-wsl-development-path.md) — currently a stub — before continuing. Native Windows 11 below remains the default and first-recommended path for this track.

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

## Bash-to-PowerShell equivalents

Most Python and general open-source documentation defaults to Bash syntax. PowerShell 7 is not Bash, so translate rather than paste. Verify uncertain cases with `Get-Help <cmdlet> -Full` rather than assuming.

### Environment variables

| Bash | PowerShell 7 |
|---|---|
| `export VAR=value` | `$env:VAR = "value"` |
| `echo $VAR` | `$env:VAR` |
| `unset VAR` | `Remove-Item Env:VAR` |
| `env` | `Get-ChildItem Env:` |

### Files and directories

| Bash | PowerShell 7 |
|---|---|
| `ls -la` | `Get-ChildItem -Force` |
| `cat file` | `Get-Content file` |
| `rm -rf dir` | `Remove-Item -Recurse -Force dir` |
| `mkdir -p a/b/c` | `New-Item -ItemType Directory -Path a/b/c` (nested directories are created automatically; add `-Force` only to suppress an "already exists" error) |
| `cp -r src dst` | `Copy-Item -Recurse src dst` |
| `mv src dst` | `Move-Item src dst` |
| `touch file` | `New-Item -ItemType File -Path file` |
| `pwd` | `Get-Location` (`pwd` also works as a built-in alias) |

### Search and inspection

| Bash | PowerShell 7 |
|---|---|
| `grep pattern file` | `Select-String -Pattern pattern -Path file` |
| `which cmd` | `Get-Command cmd` (add `.Source` for just the path) |
| `head -n 20 file` | `Get-Content file -TotalCount 20` |
| `tail -n 20 file` | `Get-Content file -Tail 20` |
| `wc -l file` | `(Get-Content file).Count` |

### Python virtual environments

| Bash | PowerShell 7 |
|---|---|
| `source .venv/bin/activate` | `.venv\Scripts\Activate.ps1` |

### Elevation

Bash's `sudo cmd` has no direct PowerShell equivalent on Windows 11. Open a new terminal with "Run as administrator" instead. Some current Windows 11 builds expose an experimental `sudo` command (Settings > For developers); do not depend on it being present until it is confirmed on the developer's build.

### Things that behave differently, not just differently-named

- **Command chaining.** PowerShell 7 supports `&&` and `||` between simple commands, similar to Bash, but they cannot directly follow a block-based keyword (`if`, `foreach`, `while`) or a variable assignment. Use `;` for plain unconditional sequencing when in doubt.
- **Pipes carry objects, not text.** `Get-ChildItem | Select-String pattern` behaves differently from a same-shaped Bash pipeline because PowerShell passes structured objects between commands, not raw text lines. Adapting a Bash one-liner that parses text output often needs a different approach entirely, not just a syntax swap.
- **Exit codes and errors.** A failing native/external command does not stop a script the way Bash's `set -e` does. Cmdlet error behavior is controlled by `$ErrorActionPreference`; a failing external command's status is available via `$LASTEXITCODE` and must be checked explicitly if the script should stop on failure.
- **Quoting.** Double quotes interpolate variables and single quotes do not, similar to Bash, but escaping rules for special characters differ. Verify quoting behavior with a short local test rather than assuming Bash-style escaping.

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
