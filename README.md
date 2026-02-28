# Dev Bootstrap Standard

Personal Dev Bootstrap Standard (PDBS)

A disciplined, opinionated bootstrap system for initializing AI-native
projects under `$HOME/Development`.

This tool ensures every project starts with:

-   Git initialized
-   A generated README.md based on project description
-   A standardized PR template at `.github/PULL_REQUEST_TEMPLATE.md`
-   A canonical `CLAUDE.md` for AI-agent guidance
-   A connected GitHub repository
-   A GitHub Projects (v2) board for tracking work

This is not a convenience script. It is development infrastructure.

------------------------------------------------------------------------

## Repository Structure

    dev-bootstrap-standard/
    ├── bin/
    │   └── dev-init
    ├── templates/
    │   ├── CLAUDE.section.md
    │   └── Pr-Template.md
    ├── bootstrap-spec.md
    ├── VERSION
    └── README.md

------------------------------------------------------------------------

## Requirements

**Required:**

-   `git`
-   `gh` (GitHub CLI) — for repo and project board creation

`gh`-dependent steps emit warnings (not failures) if `gh` is not found.

------------------------------------------------------------------------

## Installation

Clone the repository:

``` bash
git clone https://github.com/Papanii/dev-bootstrap-standard.git "$HOME/Development/dev-bootstrap-standard"
```

Make the CLI executable:

``` bash
chmod +x "$HOME/Development/dev-bootstrap-standard/bin/dev-init"
```

Add the binary directory to your PATH:

``` bash
export PATH="$HOME/Development/dev-bootstrap-standard/bin:$PATH"
```

Add that export line to `~/.zshrc`, then reload your shell:

``` bash
source ~/.zshrc
```

------------------------------------------------------------------------

## Usage

Initialize a project (run from inside the project directory):

``` bash
dev-init
```

If running outside `$HOME/Development`, confirm when prompted or
override with the force flag:

``` bash
dev-init --force
```

Check version:

``` bash
dev-init --version
```

Show help:

``` bash
dev-init --help
```

------------------------------------------------------------------------

## What `dev-init` Does

All prompts are collected upfront before any files are written:

1.  Prompts for a short project description
2.  Prompts for a GitHub Projects board title (optional)

Then executes in order:

1.  Validates execution context (must be inside `$HOME/Development` or `--force`)
2.  Initializes a `git` repository (idempotent)
3.  Generates `README.md` using the project name and description
4.  Copies the PR template to `.github/PULL_REQUEST_TEMPLATE.md`
5.  Ensures `CLAUDE.md` exists with the canonical agent instructions section
6.  Creates an initial commit (`chore: initial project setup`)
7.  Creates the GitHub repository via `gh repo create <folder-name> --source=. --public --push`
8.  Creates a GitHub Projects (v2) board via `gh project create --owner @me --title "<title>"`

------------------------------------------------------------------------

## PR Template

Every initialized project receives a PR template at:

    .github/PULL_REQUEST_TEMPLATE.md

This template is sourced from `templates/Pr-Template.md` and enforces
structured pull requests for both human contributors and AI agents.

------------------------------------------------------------------------

## CLAUDE.md Standard

Every initialized project will contain this section at the top of
`CLAUDE.md`, sourced from `templates/CLAUDE.section.md`:

``` markdown
## Instructions for the Claude Agent

- Use GitHub for source control.
- Use GitHub Issues for issue tracking.
- Use GitHub Projects (v2) for kanban board management.
- All pull requests must follow the PR template at `.github/PULL_REQUEST_TEMPLATE.md`.
- Human review is mandatory before merging any pull request.
```

------------------------------------------------------------------------

## Versioning

Version is defined in the `VERSION` file using semantic versioning:

    MAJOR.MINOR.PATCH

-   `MAJOR` — Breaking changes
-   `MINOR` — Backward-compatible enhancements
-   `PATCH` — Bug fixes or refinements

Git tags should align with `VERSION`.

------------------------------------------------------------------------

## Philosophy

Projects initialized under this standard should be:

-   AI-native
-   Reproducible
-   Safe
-   GitHub-native
-   Iteratively improvable

Bootstrap is about discipline, not convenience.
