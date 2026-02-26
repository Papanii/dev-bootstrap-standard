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
-   Enforced task tracking discipline\
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

1.  Validate execution context\
2.  Ensure `CLAUDE.md` compliance\
3.  Initialize Beads (`bd init`)\
4.  Remain idempotent\
5.  Fail safely on missing required dependencies

------------------------------------------------------------------------

## 4. Execution Safety Rules

Before modifying anything:

-   Resolve the current working directory (handle symlinks).\

-   Determine whether the directory is inside:

    \$HOME/Development/

If outside:

-   Prompt for explicit confirmation.\
-   Abort if not confirmed.\
-   In non-interactive environments, require `--force`.

This prevents accidental modification of unintended directories.

------------------------------------------------------------------------

## 5. CLAUDE.md Standard

Every initialized project must contain:

CLAUDE.md

At the top of the file, the following canonical section must exist:

    ## Instructions for the Claude Agent

    - Use `bd` for task tracking.
    - Use beadsync to upload beads to GitHub as GitHub Issues.

### Rules

-   If `CLAUDE.md` does not exist → create it.\
-   If it exists → ensure the canonical section:
    -   Exists exactly once\
    -   Is updated if necessary\
    -   Is positioned at the top of the file\
-   No duplication is permitted.\
-   The operation must be idempotent.

The canonical section content must be sourced from:

templates/CLAUDE.section.md

The implementation must not hardcode this content.

------------------------------------------------------------------------

## 6. Task Tracking Standard

Every project initialized under this standard must:

-   Run `bd init`\
-   Use `bd` for task tracking\
-   Use `beadsync` to upload beads to GitHub Issues

This is mandatory.

If `bd` is not installed, initialization must fail.

------------------------------------------------------------------------

## 7. Idempotency Requirements

Running `dev-init` multiple times must:

-   Not duplicate `CLAUDE.md` sections\
-   Not corrupt existing content\
-   Not fail if `bd` has already been initialized

Re-running initialization must be safe and predictable.

------------------------------------------------------------------------

## 8. Dependencies

Required:

-   bd

Recommended:

-   git\
-   beadsync

Missing required dependencies must result in failure.

------------------------------------------------------------------------

## 9. Canonical Folder Structure

    dev-bootstrap-standard/
    ├── bin/
    │   └── dev-init
    ├── templates/
    │   └── CLAUDE.section.md
    ├── bootstrap-spec.md
    ├── VERSION
    └── README.md

------------------------------------------------------------------------

## 10. Versioning

The active version of this standard is defined in:

VERSION

Versioning follows:

MAJOR.MINOR.PATCH

-   MAJOR → Breaking changes\
-   MINOR → Backward-compatible enhancements\
-   PATCH → Bug fixes or refinements

Git tags should align with VERSION.

------------------------------------------------------------------------

## 11. Installation & Activation

Make the CLI executable:

    chmod +x dev-bootstrap-standard/bin/dev-init

Add the binary directory to PATH:

    export PATH="$HOME/Development/dev-bootstrap-standard/bin:$PATH"

Persist this change by adding the export line to:

\~/.zshrc

After updating \~/.zshrc, reload your shell:

    source ~/.zshrc

------------------------------------------------------------------------

## 12. Philosophy

Projects initialized under this standard should be:

-   AI-native\
-   Measurable\
-   Reproducible\
-   Safe\
-   Iteratively improvable

This standard exists to industrialize development at the personal level.
