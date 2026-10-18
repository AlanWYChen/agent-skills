---
name: dependabot-policy
description: Configure or audit Dependabot PR updates with automatic merging for official GitHub Actions and manual review and merging for application dependencies. Use when setting up or checking Dependabot schedules, ecosystem filters, approval workflows, or auto-merge prerequisites in a repository.
---

# Dependabot policy

Keep code dependency updates visible as PRs for the owner to review and merge. Allow verified Dependabot updates to official `actions/*` repositories to approve and auto-merge after required checks, including major upgrades. Third-party Actions remain manual unless the user explicitly expands the allowlist.

## Inspect before editing

Read repository instructions, `.github/dependabot.yml`, workflows, manifests, and existing auto-merge automation. Identify the default branch, package ecosystems/directories, CI check names, merge method, and existing schedules. Preserve unrelated configuration. An audit request calls for findings; a setup request authorizes the necessary local edits. Do not infer permission to publish, change remote rules, or merge existing PRs from a request to create or install this skill.

The SWE Portfolio pattern uses npm and GitHub Actions at `/`, weekly Monday 09:00 `America/Toronto`, `main`, squash merging, and the `build` check from `Publish GitHub Pages`. Treat these as adaptable defaults, not requirements for other repositories.

## Configure updates and merge policy

- Adapt [assets/dependabot.yml](assets/dependabot.yml) to the detected manifests and directories. Keep code and Actions ecosystems separate. Preserve security update coverage and existing schedules unless the task calls for changes. Do not suppress code dependency PRs to make them manual.
- Adapt [assets/dependabot-auto-merge.yml](assets/dependabot-auto-merge.yml) to the target branch and supported merge method. Verify action versions with primary sources before selecting or upgrading them; template tags are examples, not promises of the latest version.
- Require the actual PR author to be `dependabot[bot]`, a head in the same repository, verified Dependabot commits, the `github_actions` metadata ecosystem, and a nonempty dependency list where **every** dependency is an official `actions/*` repository. The configuration ecosystem is `github-actions`; fetch-metadata reports `github_actions`. Never use PR labels, titles, branch prefixes, or the triggering actor alone as proof.
- Gate both approval and enabling auto-merge on the same decision. A mixed group containing any disallowed dependency must remain manual. An ecosystem-only filter allows third-party Actions too and does not satisfy the official-only policy.
- Use `pull_request_target` for the privileged metadata/approval job with top-level `permissions: {}` and job-level `contents: write` and `pull-requests: write`. Never check out a PR, install its dependencies, execute its scripts, or consume its artifacts in this job. Keep ordinary PR CI separate and read-only.
- Keep fetch-metadata verification enabled. Its implementation dependency, `dependabot/fetch-metadata`, is outside the default `actions/*` allowlist and is therefore reviewed manually too. Do not broaden the allowlist merely because an action is on the Marketplace or marked verified.
- Use `gh pr merge --auto` with `--match-head-commit`; do not bypass branch protections or add an admin merge. Pass event values and metadata through environment variables, not interpolated shell source. Include major Actions upgrades; do not impose a patch/minor restriction by default.
- Leave npm and other code ecosystems, including their security PRs, without bot approval or auto-merge. Check for other workflows or repository automation that would undermine that policy. Manual merging does not require a formal approving review by the repository owner, who cannot approve their own PRs.

## Repository prerequisites and publication

When remote setup is requested and authorized, inspect current settings before changing them. Otherwise document the exact remaining settings:

- Enable **Allow auto-merge** and the selected merge method in repository settings.
- Enable **Allow GitHub Actions to create and approve pull requests** under Actions workflow permissions if automatic approval is used.
- Require the real PR CI check on the default branch through a branch rule or ruleset. `--auto` does not wait for optional checks; without required checks it can merge immediately. Do not claim CI gating until the remote rule is verified.
- Preserve human review requirements and other protections. Bot approval might not satisfy all review rules. A merge queue can require a GitHub App token instead of the built-in token; report the limitation instead of weakening protection.

`GITHUB_TOKEN` merges can suppress follow-up push workflows, including deployment. Inspect publication triggers. Document a manual `workflow_dispatch` fallback where available; do not silently install a PAT or claim automatic publication works without verification. Treat invalid CLI authentication as a blocked remote operation, not proof of the current remote settings. Distinguish local configuration from active configuration on the default branch.

## Verify and report

Run the available YAML formatter, `actionlint` against changed workflows, and diff checks. Validate the allowlist decision with representative metadata: official major update eligible; npm, third-party Action, mixed group, empty list, and malformed metadata ineligible. Confirm non-Dependabot and fork PRs fail the job guard and that both write steps share the eligibility gate. Repository CI still tests compatibility of major upgrades.

Report changed files, checks run, any existing policy mismatch, and any remote settings or publication steps still required. Do not overwrite unrelated user changes.

## Primary references

Consult these when verifying current platform behavior or adapting the template:

- [GitHub: Automating Dependabot with Actions](https://docs.github.com/en/code-security/tutorials/secure-your-dependencies/automate-dependabot-with-actions)
- [dependabot/fetch-metadata inputs, verification, and outputs](https://github.com/dependabot/fetch-metadata)
- [GitHub: Triggering workflows from a workflow](https://docs.github.com/en/actions/how-tos/writing-workflows/choosing-when-your-workflow-runs/triggering-a-workflow)
