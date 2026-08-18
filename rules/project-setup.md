# Project Setup

Folder structure conventions, scaffolding defaults, what a new repo should
have before it's considered "started."

See [_format.md](_format.md) for the entry format.

---

### Structure agent instructions as a small hierarchy, not one big file
- **Rule:** Prefer a concise global `AGENTS.md`/`CLAUDE.md` plus scoped instruction files in subdirectories (e.g. `frontend/AGENTS.md`, `backend/AGENTS.md`) only where they add real repository-specific value. Don't create scoped files that just duplicate the global ones, and don't let either grow into a giant policy document.
- **Why:** A bloated or duplicated instruction set costs context on every single task; scoping keeps stack-specific rules close to the code they affect without repeating them everywhere.
- **Applies to:** any repo maintaining CLAUDE.md/AGENTS.md files
