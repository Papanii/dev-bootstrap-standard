## Instructions for the Claude Agent

- Use `bd` for task tracking.
- Use beadsync to upload beads to GitHub as GitHub Issues.

### Task Tracking Rules                                                                                                                                      

This project uses `bd` (Beads CLI) for task tracking and `beadsync` to sync beads to GitHub Issues. The `bd` database has been initialized in this repo.

 **Do not work on any code unless it is tied to an open bead or GitHub Issue.**

 Before starting any work:

1. Run `bd list` or `beadsync status` to find the relevant bead.
2. If no bead exists for the requested work, stop and ask the user to create one before proceeding.
3. Reference the bead ID in all discussion about the work (e.g. `bd-abc123`).

###  Commits and Pull Requests

 Before creating any commit or PR:

1. Run `bd show <id>` to get the bead title and details.
2. Run `beadsync status` to check if a corresponding GitHub Issue exists.

 **Commit message format:**

 [bd-abc123] Short description of change

 Bead: bd-abc123 — "Title of the bead"

 GitHub Issue: #42 (omit this line if no issue exists yet)

 **PR format:**

1. Title must include the bead ID: `[bd-abc123] Short description`
2. Body must include:
   1. A link to the bead: `Bead: bd-abc123 — "Title of the bead"`
   2. A link to the GitHub Issue if one exists: `Closes #42`
   3. Summary of changes and test plan as normal

