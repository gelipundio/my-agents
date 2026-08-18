# Dev Environment

Process management — dev servers, ports, and what the agent may run itself
versus what belongs to the dev.

See [_format.md](_format.md) for the entry format.

---

### Don't start or stop dev processes yourself
- **Rule:** Assume the project's dev server/process is already running. Don't start, stop, or restart it as part of implementing a change — ask the dev to do that manually. If you need a specific port, ask the dev which one to use instead of picking one.
- **Why:** Avoids clobbering a process the dev already has running (with its own state, logs, or port bindings) and prevents port conflicts from guessed values.
- **Applies to:** all
