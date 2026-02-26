# Dev Bootstrap Standard

Personal Dev Bootstrap Standard (PDBS)

A disciplined, opinionated bootstrap system for initializing AI-native
projects under `$HOME/Development`.

This tool ensures every project starts with:

-   AI-agent readiness
-   Enforced `bd` task tracking
-   Canonical `CLAUDE.md` structure
-   Safe execution boundaries
-   Idempotent behavior

This is not a convenience script. It is development infrastructure.

------------------------------------------------------------------------

## Repository Structure

    dev-bootstrap-standard/
    ├── bin/
    │   └── dev-init
    ├── templates/
    │   └── CLAUDE.section.md
    ├── bootstrap-spec.md
    ├── VERSION
    └── README.md

------------------------------------------------------------------------

## Requirements

**Required:**

-   [`bd`](https://github.com/Papanii/beads) — task tracking CLI

**Recommended:**

-   `git`
-   `beadsync` — syncs `bd` tasks to GitHub Issues

`dev-init` will fail immediately if `bd` is not found in PATH.

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

1.  Validates the execution context (must be inside `$HOME/Development` or `--force`)
2.  Ensures `CLAUDE.md` exists with the canonical section at the top
3.  Runs `bd init` to initialize task tracking
4.  Remains idempotent — safe to run multiple times without duplication or corruption

------------------------------------------------------------------------

## CLAUDE.md Standard

Every initialized project will contain this section at the top of
`CLAUDE.md`:

``` markdown
## Instructions for the Claude Agent

- Use `bd` for task tracking.
- Use beadsync to upload beads to GitHub as GitHub Issues.
```

This content is sourced from:

    templates/CLAUDE.section.md

The script does not hardcode the section. The template is the source of
truth.

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
-   Measurable
-   Reproducible
-   Safe
-   Iteratively improvable

Bootstrap is about discipline, not convenience.
