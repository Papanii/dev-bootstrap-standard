## Instructions for the Claude Agent

- Use GitHub for source control. If git is not installed or configured, give a warning.
- Use GitHub Issues for issue tracking. If the repository has no issues configured, give a warning.
- Use GitHub Projects (v2) for kanban board management and epic tracking.
- Human review is mandatory before merging any pull request.

## Pull Request Guidelines

Use `.github/PULL_REQUEST_TEMPLATE.md` as a reference, not a form. The goal is a PR that reads clearly and contains exactly the information a reviewer needs — nothing more.

**Always include:**
- Intent: what problem this solves and any linked issue or spec
- Change Summary: the type of change and a concise list of what changed
- Rollback Plan: how to revert if something goes wrong
- AI Agent Disclosure: if the PR was AI-assisted, include model used and confirmation checklist

**Include only when relevant:**
- Why This Matters: for features and significant changes; skip for typo fixes or trivial refactors
- Technical Approach: for non-trivial implementation decisions; skip for straightforward changes
- Tests & Validation: only list tests that were actually written or run; omit subsections with nothing to report
- Observability: only if the change adds or modifies logs, metrics, traces, or feature flags
- Security & Compliance: only if the change touches auth, data handling, access control, or dependencies
- Performance Impact: only if the change could plausibly affect latency, memory, or throughput

**Rules:**
- Never leave placeholder text, empty bullets, or N/A values in the final PR
- Remove entire sections that do not apply to the change
- Write in plain language — use bullets only when listing genuinely distinct items
- A short, accurate PR is better than a long one padded with irrelevant sections

## Repo Creation

When creating a repo:

- Use `dev-init` to initialize the project.
- The repo name matches the local directory name.
- The repo is created as public via `gh repo create <name> --source=. --public --push`.
- A GitHub Projects (v2) board should be created for tracking work.
- The PR template is automatically placed at `.github/PULL_REQUEST_TEMPLATE.md`.
