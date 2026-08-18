# Git Workflow

Commit practices, branching, PR conventions, what counts as a destructive
action worth confirming first.

See [_format.md](_format.md) for the entry format.

---

### Let the dev drive git actions
- **Rule:** Never run git commands that change repository state (commit, push, branch, merge, rebase, tag, etc.) yourself — tell the dev what to run and let them execute it. Read-only commands (status, diff, log, show) are fine for gathering context.
- **Why:** Git history and pushes should stay under the dev's deliberate control, not get assumed or auto-executed by the model.
- **Applies to:** all

### Hard limits even where git writes are allowed
- **Rule:** Never force push, run a destructive reset (`--hard`, etc.), or discard uncommitted changes unless explicitly requested. Never commit secrets. Verify scope before any destructive operation.
- **Why:** These operations can permanently destroy work that isn't recoverable from local state alone — a backstop for any project where the stricter "dev drives git" rule above isn't in force.
- **Applies to:** all
