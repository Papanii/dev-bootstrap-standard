## Instructions for the Claude Agent

- Use GitHub for source control. If git is not installed or configured, give a warning.
- Use GitHub Issues for issue tracking. If the repository has no issues configured, give a warning.
- Use GitHub Projects (v2) for kanban board management and epic tracking.
- All pull requests must follow the PR template at `.github/PULL_REQUEST_TEMPLATE.md`.
- Human review is mandatory before merging any pull request.

## Repo Creation

When creating a repo:

- Use `dev-init` to initialize the project.
- The repo name matches the local directory name.
- The repo is created as public via `gh repo create <name> --source=. --public --push`.
- A GitHub Projects (v2) board should be created for tracking work.
- The PR template is automatically placed at `.github/PULL_REQUEST_TEMPLATE.md`.
