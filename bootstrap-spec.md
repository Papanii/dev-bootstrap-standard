# Personal Dev Bootstrap Standard (PDBS)

Owner: Papanii Okai\
Version: See VERSION file\
Status: Active

------------------------------------------------------------------------

## 1. Purpose

Define the canonical way projects are initialized within my development
ecosystem.

This standard ensures:

-   Consistency across projects\
-   AI-agent readiness\
-   Enforced PR discipline\
-   Safe execution boundaries\
-   Idempotent initialization behavior

Bootstrap is not a convenience script.\
It is infrastructure.

------------------------------------------------------------------------

## 2. Scope

This standard primarily applies to projects created under:

\$HOME/Development/

It may be used elsewhere only with explicit confirmation (`--force`).

------------------------------------------------------------------------

## 3. Enforcement Command

This standard is enforced via:

    dev-init

The command must:

1.  Validate execution context
2.  Collect user inputs upfront (description, Kanban board title)
3.  Ensure `CLAUDE.md` compliance
4.  Generate a `README.md` from project description
5.  Install the PR template at `.github/PULL_REQUEST_TEMPLATE.md`
6.  Create an initial commit
7.  Create the GitHub repository
8.  Create the GitHub Projects (v2) board
9.  Remain idempotent
10. Fail safely on missing required dependencies

------------------------------------------------------------------------

## 4. Execution Safety Rules

Before modifying anything:

-   Resolve the current working directory (handle symlinks).

-   Determine whether the directory is inside:

    \$HOME/Development/

If outside:

-   Prompt for explicit confirmation.\
-   Abort if not confirmed.\
-   In non-interactive environments, require `--force`.

This prevents accidental modification of unintended directories.

------------------------------------------------------------------------

## 5. User Inputs

`dev-init` collects all user input **before** touching the filesystem.
This ensures no partial state is written if the user aborts.

| Prompt                    | Used for                              |
|---------------------------|---------------------------------------|
| Short project description | README.md overview section            |
| GitHub Projects board title | `gh project create --title`         |

The **repository name** is always derived from the local directory name.
It is not prompted — it is inferred.

------------------------------------------------------------------------

## 6. Initialization Sequence

Steps execute in this order:

1.  `git init` — initialize the repository if not already done
2.  Collect user inputs (description, Kanban title)
3.  Generate `README.md` using the project description
4.  Copy PR template to `.github/PULL_REQUEST_TEMPLATE.md`
5.  Ensure `CLAUDE.md` contains the canonical section
6.  `git add` + `git commit -m "chore: initial project setup"`
7.  `gh repo create <folder-name> --source=. --private --push`
8.  `gh project create --owner @me --title "<kanban-title>"` (if title provided)

------------------------------------------------------------------------

## 7. CLAUDE.md Standard

Every initialized project must contain:

    CLAUDE.md

At the top of the file, the following canonical section must exist:

    ## Instructions for the Claude Agent

### Rules

-   If `CLAUDE.md` does not exist → create it.\
-   If it exists → ensure the canonical section:
    -   Exists exactly once
    -   Is updated if the template has changed
    -   Is positioned at the top of the file
-   No duplication is permitted.\
-   The operation must be idempotent.

The canonical section content is sourced from:

    templates/CLAUDE.section.md

The implementation must not hardcode this content.

------------------------------------------------------------------------

## 8. PR Template Standard

Every initialized project must contain a PR template at:

    .github/PULL_REQUEST_TEMPLATE.md

This template is sourced from:

    templates/Pr-Template.md

The template enforces structured pull requests for both human contributors
and AI agents. It is non-negotiable — every repository must have it.

------------------------------------------------------------------------

## 9. Idempotency Requirements

Running `dev-init` multiple times must:

-   Not duplicate `CLAUDE.md` sections
-   Not overwrite an existing `README.md`
-   Not overwrite an existing PR template
-   Not create duplicate commits
-   Not fail if the GitHub repository already has a remote origin set

Re-running initialization must be safe and predictable.

------------------------------------------------------------------------

## 10. Dependencies

Required:

-   `git`
-   `gh` (GitHub CLI)

Missing required dependencies result in warnings, not hard failures,
for `gh`-dependent steps. Missing `git` is a hard failure.

------------------------------------------------------------------------

## 11. Canonical Folder Structure

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

## 12. Versioning

The active version of this standard is defined in:

    VERSION

Versioning follows:

    MAJOR.MINOR.PATCH

-   MAJOR → Breaking changes\
-   MINOR → Backward-compatible enhancements\
-   PATCH → Bug fixes or refinements

Git tags should align with VERSION.

------------------------------------------------------------------------

## 13. Installation & Activation

Make the CLI executable:

    chmod +x dev-bootstrap-standard/bin/dev-init

Add the binary directory to PATH:

    export PATH="$HOME/Development/dev-bootstrap-standard/bin:$PATH"

Persist this change by adding the export line to:

\~/.zshrc

After updating \~/.zshrc, reload your shell:

    source ~/.zshrc

------------------------------------------------------------------------

## 14. Philosophy

Projects initialized under this standard should be:

-   AI-native\
-   Reproducible\
-   Safe\
-   GitHub-native\
-   Iteratively improvable

This standard exists to industrialize development at the personal level.
