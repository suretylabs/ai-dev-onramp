# GitHub Organization, Copilot, and Repository Foundation

> Companion: [GitHub foundation visual](../visuals/01-github-foundation.md)

## Starting-state preflight

The default path in this guide assumes a new business development environment: no intentional personal GitHub account for this work, no business organization, and no Copilot entitlement. Confirm that state before creating anything.

Ask only the questions that change the next decision:

- Does the developer already have an intentional GitHub personal account?
- Does the business already have a GitHub organization, enterprise account, or centrally managed identity environment?
- Who should own billing and receive continuity or recovery notices?
- What organization name is intended?
- Which collaborators or additional owners are expected?

Then choose the verified path:

1. **Clean state** — create the developer's personal account, secure it, create the business organization, create the first organization-owned repository, and activate Copilot on that same identity.
2. **Existing personal account** — inspect and secure the intentional account, then continue without creating a duplicate.
3. **Existing organization** — verify ownership, billing, security, and repository conventions before creating or selecting the project repository.
4. **Centrally managed enterprise or Enterprise Managed Users** — stop before creating unmanaged identities or organizations and follow the company-controlled path.

If GitHub reports an email or username collision, treat that as evidence requiring reconciliation rather than a reason to create another identity. Never place the first business repository under a personal namespace as a temporary shortcut.

## Outcome

Establish GitHub as the durable online anchor for the development environment before local tooling is integrated.

At the end of this phase:

- the developer has one intentional personal GitHub identity;
- the intended personal account is verified, secured, and recoverable;
- the intended business GitHub organization exists under the correct namespace;
- organization ownership, billing responsibility, member access, and baseline policies are understood;
- GitHub Copilot is active for the developer's exact personal account, preferably through organization-managed licensing and otherwise through an explicitly recorded temporary individual entitlement;
- the first project repository exists under the organization with a small, deliberate baseline;
- visibility, naming, default-branch, and repository-convention decisions are explicit;
- lightweight protections reduce destructive mistakes without creating enterprise ceremony;
- the remote organization-owned repository is ready to be cloned and used to verify the local Git and `gh` setup.

## Why GitHub comes before the local toolchain

Do not present GitHub merely as an off-machine backup.

For this workflow, GitHub is the initial **coordination plane**:

```text
The developer's personal GitHub account
    -> human identity and authentication
    -> organization membership and ownership

Business GitHub organization
    -> business repository ownership
    -> preferred Copilot seat and policy administration
    -> collaborator and team access
    -> remote source history
    -> issues, pull requests, and review surface
    -> later: Actions, secrets, environments, and automation
```

The local machine will later attach to this already-known remote state:

```text
Known organization-owned repository on GitHub
        |
        | authenticate the developer with gh
        | clone with Git
        v
Known repository on the Windows machine
        |
        | make, commit, and push one change
        v
Same change visible in the organization repository
```

This round trip proves more than an installer reporting success. It verifies identity, organization access, authentication, Git configuration, remote configuration, filesystem location, and network access as one connected system.

## Interaction rule for this phase

The guiding LLM should use GitHub's current web interface as evidence. Questions are expected throughout this phase when they help distinguish personal identity, business ownership, billing responsibility, security posture, plan capability, or repository policy. Keep them proportionate to the decision at hand and explain why the answer affects the next step.

For every material page:

1. Ask the developer to provide the exact labels or a screenshot.
2. Explain what the choice controls.
3. Distinguish **personal-account**, **organization-wide**, and **repository-specific** settings.
4. Recommend the smallest suitable configuration.
5. Record the decision without recording secrets, recovery codes, or authentication factors.

Do not rely on remembered menu names when the interface differs from current documentation.

## Step 1: establish the developer's personal GitHub account

A GitHub organization is not a shared login. Each human normally authenticates through a personal GitHub account, while the organization owns the business repositories and policy boundary. On a clean-state path, the developer creates the personal account first and uses it to bootstrap the organization. On an existing-account path, inspect and secure that account before proceeding.

Begin with a brief, practical confirmation such as:

> Are you aware of any GitHub account already associated with you, or any GitHub environment already administered by the company?

Follow with any additional question that is genuinely needed to choose the correct identity, email, recovery, ownership, or billing path. When the answers indicate a clean state, guide the developer directly through account creation. Do not spend time searching for nonexistent history, but do not suppress useful questions merely to keep the sequence mechanically short.

Explain the durable model before signup:

- A **personal account** represents the developer as a person.
- The **organization** will represent the business-owned repository and collaboration boundary.
- the developer's personal account will be an owner and member of the organization.
- Human users never share the organization owner's personal login.
- The same personal account should later be used by GitHub.com, `gh`, Git Credential Manager, VS Code, and Copilot.

For a new account, guide the developer through choosing:

- a stable professional username that can outlive this first project;
- a strong, unique password stored in a password manager;
- a durable primary email address they control;
- an optional verified business email as a secondary address when appropriate;
- a profile name and visibility level suitable for professional use.

Do not name the account after the organization or project. The account is the developer's durable identity, not a service account or business namespace.

### Collision or existing-account evidence

If GitHub reports that the email address or intended username is already in use, do not work around it by creating another identity. Stop and use the evidence to recover or inspect the existing account. Once resolved, return to this guide with one confirmed personal account.

If the company unexpectedly uses Enterprise Managed Users or another centrally provisioned identity model, stop before creating an unmanaged account or organization and follow the company process.

## Step 2: secure and verify the new personal account

Immediately after account creation, guide the developer through:

- verifying the primary email address;
- adding and verifying a backup email or recovery destination when appropriate;
- confirming the password is stored in their password manager rather than in the chat or repository;
- reviewing which profile information should be public;
- deciding whether contribution activity should be public or private;
- signing out and back in once when useful to confirm that the account and recovery model are understood.

The account is a durable personal identity that may participate in many organizations and repositories.

### Commit-email privacy decision

Explain that three email concepts can differ:

1. the account's primary email;
2. the address GitHub uses for notifications and recovery;
3. the author email recorded in Git commits.

If the developer does not want a personal address embedded in commit metadata, enable GitHub email privacy and use the GitHub-provided `noreply` commit address later in Git configuration.

When privacy is enabled, consider enabling the setting that blocks command-line pushes exposing a private account email. Explain that this is a guardrail, not a replacement for correct local Git identity.

Record only the selected policy and whether verification is complete. Do not copy actual private email addresses into the onboarding package unless the developer explicitly wants them recorded there.

### Account security and recovery

Account security is a prerequisite, not an optional later hardening exercise.

Guide the developer through:

- enabling two-factor authentication;
- configuring at least two practical authentication or recovery methods;
- saving recovery codes in a secure location outside the repository and outside the chat;
- adding a passkey when the device and password-manager strategy support it;
- confirming they can identify where account-recovery material is stored.

The LLM must never ask the developer to paste:

- passwords;
- TOTP setup secrets;
- one-time authentication codes;
- recovery codes;
- passkey details;
- personal access tokens.

Record only non-secret state, for example:

```text
2FA enabled: yes
Primary factor: TOTP
Additional method: passkey
Recovery codes stored securely: confirmed
```

## Step 3: create the business organization

Assume no organization exists. Once the developer's personal account is verified and secured, create the business GitHub organization from that account.

Do not create the first business repository under the developer's personal namespace as a temporary shortcut. Establish the ownership boundary correctly before project content begins.

If the organization name the developer wants is unavailable, treat that as a naming decision—not a reason to put the project under their personal account. Choose a durable alternative business namespace and record it.

### Organization identity

Choose an organization name that can outlive the first repository.

Prefer a name based on the business, product family, or durable development identity—not the developer's username, a Python version, or the first prototype's name.

Record:

- organization display name;
- organization login/slug;
- business or billing contact destination;
- whether the organization is independent or company-managed;
- the current organization owner accounts.

Do not record payment-card data, tax identifiers, or other sensitive billing details in the repository or chat.

### Organization ownership and recovery

The developer should be an **organization owner** during bootstrap.

Where another trusted business principal or technical administrator exists, add a second organization owner after that person has secured their own account. This protects continuity if the developer loses access or becomes unavailable.

Do not add a nominal second owner merely to satisfy a checklist. When the developer is the only legitimate owner at the moment, record that as a continuity risk to revisit rather than sharing credentials or adding an inappropriate person.

### Organization security baseline

Apply a lightweight organization baseline before adding repositories or collaborators:

- require members to use two-factor authentication when the current plan and organization settings support it;
- verify the developer already satisfies the requirement before enabling it;
- keep organization membership private or public according to business intent;
- do not create shared accounts;
- do not invite collaborators before their access is needed;
- use the least organization role that allows each person to do their work;
- keep default/base repository access minimal;
- restrict broad member repository-creation privileges when the developer is initially the only operator;
- keep new business repositories private by default when the current settings allow that policy.

The exact setting labels and plan capabilities may change. Inspect the actual organization pages rather than relying on remembered names.

### Billing boundary

Make the billing relationship legible:

- the organization owns repository-plan and organization-level charges;
- the developer's personal account receives access through organization membership;
- GitHub repository plans and GitHub Copilot plans are separate product decisions;
- Copilot can be licensed to the developer either through an organization/enterprise seat or an individual plan, but the exact entitlement must be recorded;
- payment details never belong in the repository, onboarding state file, or chat.

Record who is responsible for organization billing and where renewal notices go, without recording payment details.

## Step 4: activate GitHub Copilot for the developer's exact account

Copilot should be ready before VS Code is installed and connected, but **organization creation and organization-managed Copilot licensing are separate operations**. Do not assume that creating a GitHub organization automatically exposes a direct Copilot Business purchase flow.

### Time-sensitive acquisition gate

Before choosing the licensing path, verify the current official GitHub documentation, plan eligibility, pricing, and the actual billing interface. Copilot plans, included usage, acquisition flows, and policy controls change over time. Do not preserve a remembered menu path or purchasing constraint as though it were permanent.

Use this decision order:

1. **Preferred durable path — organization-managed Copilot.** When an appropriate Copilot Business or enterprise-managed path is available, enable it for the organization or enterprise and assign the developer's personal account a seat. A dedicated enterprise can be used as a Copilot licensing and identity-management envelope without requiring the source repositories to move out of the business organization.
2. **Temporary bootstrap path — individual Copilot entitlement.** If organization-managed acquisition is unavailable, disproportionate, or blocked during setup, activate an appropriate current individual Copilot plan on the same personal account. Keep the repository organization-owned. Record the individual entitlement as temporary and define the condition for migrating to organization-managed licensing later.
3. **Never create a second identity to solve licensing.** The same personal account should be the GitHub member, local `gh` identity, VS Code identity, and Copilot user unless a centrally managed enterprise identity model explicitly requires otherwise.

Whichever path is used, confirm:

- the exact personal account that will sign into VS Code has active Copilot access;
- Copilot Chat works on GitHub.com;
- IDE use is included;
- the entitlement is not attached to a different account;
- the billing owner and renewal responsibility are understood;
- the chosen path and any migration condition are recorded in `BOOTSTRAP_STATE.md`.

### Copilot policy review

When Copilot is organization-managed, review the material organization or enterprise policies. When Copilot is individually licensed during bootstrap, review the equivalent personal settings and record that the organization does not yet centrally govern them. Decisions can include:

- whether suggestions matching public code are allowed or blocked;
- whether prompts, suggestions, or code may be retained or used for product improvement;
- whether web search is available to Copilot Chat;
- whether coding-agent or cloud-agent capabilities are available;
- which repositories or members can use specific capabilities;
- whether an enterprise policy overrides the organization or personal setting.

For proprietary business work, begin conservatively:

- block suggestions matching public code unless the developer deliberately chooses otherwise;
- do not enable broad autonomous or cloud-agent access merely because it is available;
- limit repository access to the project scope actually needed;
- review data-use settings rather than accepting them without inspection;
- keep secrets, customer data, production records, and confidential documents out of prompts regardless of policy.

Record each material choice and the scope that controls it: personal, organization, or enterprise. Do not turn this into a legal opinion about intellectual-property ownership.

## Step 5: establish lightweight organization conventions

The organization should provide clarity without pretending to be a large engineering department.

Use these initial conventions:

- business repositories are organization-owned;
- repositories are private by default unless publication is deliberate;
- repository names are short, descriptive, lowercase, and hyphen-separated;
- `main` is the default branch;
- no shared human accounts;
- no credentials or production data in Git;
- collaborators are added only when there is a real need;
- teams are introduced when repeated access grouping appears, not merely because organizations support teams;
- organization-level secrets, environments, runners, and apps are added only when a real workflow requires them;
- material repository changes eventually use focused branches and pull requests, even when the developer is the only developer.

Do not introduce a complex repository taxonomy, mandatory team hierarchy, CODEOWNERS, release governance, or enterprise naming schema during bootstrap.

## Step 6: create the first organization-owned repository

Create the repository under the organization—not under the developer's personal namespace.

### Repository name

Prefer a short, descriptive, lowercase, hyphen-separated name:

```text
project-purpose
```

Avoid dates, technology versions, usernames, or words such as `final`, `new`, or `test` unless they are genuinely part of the project's identity.

### Visibility

Use **private** visibility unless there is a deliberate reason to publish the project.

Private does not mean secret-safe. Credentials, tokens, connection strings, customer records, production PDFs, and production database extracts still do not belong in source control.

### Default branch

Use `main` as the default branch. Verify the actual repository setting rather than assuming it.

### Initial repository content

Create a deliberately small documentation-first baseline:

```text
README.md
.gitignore
.github/copilot-instructions.md
```

The initial `README.md` may contain only:

- the provisional project name;
- a statement that the project is in discovery/bootstrap;
- the owning organization;
- a warning that no production credentials or data belong in the repository.

Choose the Python `.gitignore` template if GitHub offers it, then inspect it later. A template is a starting point, not proof that every local artifact or secret surface is covered.

For a private business repository, do not add an open-source license unless the business has deliberately selected one.

### Bootstrap Copilot instructions

The first `.github/copilot-instructions.md` should be intentionally minimal. Its job is to control the first VS Code Copilot session before the project has been explained fully.

Use the supplied `templates/bootstrap-copilot-instructions.md` or equivalent language that tells Copilot:

1. this is an organization-owned business repository in discovery/bootstrap mode;
2. the developer is an experienced developer changing toolchains;
3. it must first ask the developer to explain the actual business process and first useful outcome;
4. it must distinguish documented facts from inference;
5. it must create or refine `docs/PROJECT_BRIEF.md`;
6. it must replace the bootstrap instructions with the confirmed project contract;
7. it must not generate application code, add dependencies, or invent architecture before review.

This file is not the final repository contract. It ensures Copilot begins by listening and establishing context.

## Step 7: apply lightweight repository protections

The objective is to prevent destructive mistakes while preserving the ability to learn and recover.

Do not configure mandatory reviews from nonexistent collaborators, required CI checks before CI exists, signed-commit enforcement, deployment environments, CODEOWNERS, or complex rulesets during bootstrap.

### Always apply

- Private visibility for proprietary work.
- Organization ownership.
- `main` as the default branch.
- No credentials or production data in tracked files.
- A `.gitignore` that will later be verified locally.
- No shared human account.
- Recovery-capable personal-account and organization ownership.
- A convention that force pushes and branch deletion are never performed on `main` casually.
- Collaborator access only through named personal accounts.

### Apply when the organization's current GitHub plan supports private-repository protection

Create one narrow rule for `main`, or its current equivalent:

- block force pushes;
- block deletion;
- optionally require changes to arrive through a pull request after the developer has completed the first branch-and-PR exercise;
- do not require an approval when the developer is the only developer unless another legitimate reviewer exists;
- do not require status checks until a real CI workflow exists and has run successfully;
- do not block the organization owner from recovery actions without first understanding the bypass model.

GitHub plan availability differs for private organization repositories. Inspect the current organization plan and the actual repository settings. Do not recommend an upgrade solely to create ceremonial controls without discussing the operational benefit.

### When technical branch protection is unavailable

Use a documented workflow convention instead of pretending enforcement exists:

- routine work occurs on a focused branch;
- `main` is updated through a reviewed pull request when practical;
- no force push to `main`;
- no deletion of `main`;
- inspect the diff before merge;
- keep commits small enough to reverse.

Record whether the control is **enforced by GitHub** or **followed by convention**. Those are materially different states.

### Merge and branch cleanup settings

Do not over-optimize merge strategy during bootstrap. Leave supported merge methods available unless the developer already has a strong preference.

Enabling automatic deletion of merged head branches is reasonable once the branch-and-pull-request model has been demonstrated. Explain that this deletes the remote feature branch after merge, not its commits from history.

## Step 8: verify the organization and remote foundation

Before installing local Git tooling, verify in GitHub's web interface:

- the developer's exact personal account is signed in;
- personal email, 2FA, and recovery settings are verified;
- the intended business organization is selected;
- the developer is an organization owner;
- another owner exists when appropriate, or the continuity risk is recorded;
- organization billing responsibility is understood;
- organization security and member-access settings match the lightweight baseline;
- Copilot is active on the developer's exact personal account through the recorded organization-managed or temporary individual entitlement path;
- material Copilot policies are recorded at the correct scope;
- the repository owner is the organization;
- the repository is private;
- `main` is the default branch;
- the expected initial files exist;
- the bootstrap Copilot instructions render correctly;
- lightweight protections are either enforced or explicitly documented as conventions;
- no secret, token, credential, customer data, production extract, or production document has been added.

Capture the repository's canonical organization/name pair:

```text
ORGANIZATION/REPOSITORY
```

This identifier will be used by `gh`, clone commands, issue references, pull requests, and later AI tooling.

## Acceptance gate

This phase passes when:

- the developer has one intentional, secured personal GitHub identity;
- the intended business organization exists under the correct business namespace;
- the developer's organization role, billing boundary, and continuity posture are understood;
- organization security and access defaults have been reviewed;
- Copilot is active for the developer's exact account; the entitlement is organization-managed when available, or a temporary individual path and migration condition are explicitly recorded;
- the organization-owned private repository exists with `main`, `README.md`, `.gitignore`, and bootstrap `.github/copilot-instructions.md`;
- lightweight branch safeguards are technically enforced or accurately recorded as conventions;
- `BOOTSTRAP_STATE.md` contains only non-secret identity, organization, entitlement, and repository state;
- the `ORGANIZATION/REPOSITORY` identifier is known and ready for the local-tooling phase.

## Transition checkpoint

Update `BOOTSTRAP_STATE.md` before leaving this phase. Record the verified personal identity, organization ownership, Copilot entitlement path, canonical `ORGANIZATION/REPOSITORY`, branch-safeguard state, deferred collaborator work, and any licensing migration condition.

Then ask whether the developer would like to:

1. continue to local Git and GitHub CLI so the machine can prove its connection to the organization repository; or
2. remain in GitHub for an optional walkthrough of organization membership, repository settings, and the branch/rules surface.

Recommend continuing to local Git unless another collaborator must be added immediately. If the foundation is incomplete, do not offer the next phase as though it were ready; offer troubleshooting or a recorded pause.

## Official reference points

The guiding LLM should verify current behavior against:

- GitHub account setup: <https://docs.github.com/en/get-started/onboarding/getting-started-with-your-github-account>
- Two-factor authentication: <https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication>
- Recovery methods: <https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication-recovery-methods>
- Organizations: <https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/about-organizations>
- Creating an organization: <https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/creating-a-new-organization-from-scratch>
- Organization roles: <https://docs.github.com/en/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization>
- Requiring two-factor authentication: <https://docs.github.com/en/organizations/keeping-your-organization-secure/managing-two-factor-authentication-for-your-organization/requiring-two-factor-authentication-in-your-organization>
- Copilot organization setup: <https://docs.github.com/en/copilot/how-tos/copilot-on-github/set-up-copilot/enable-copilot/set-up-for-organization>
- Copilot Business enterprise-account option: <https://docs.github.com/en/copilot/concepts/about-enterprise-accounts-for-copilot-business>
- Copilot seat assignment: <https://docs.github.com/en/copilot/reference/copilot-billing/seat-assignment>
- Copilot quickstart and current signup notices: <https://docs.github.com/en/copilot/get-started/quickstart>
- Repository best practices: <https://docs.github.com/en/repositories/creating-and-managing-repositories/best-practices-for-repositories>
- Branch protection: <https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches>
- Rulesets: <https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets>
