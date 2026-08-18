# General

Cross-cutting principles that don't fit a narrower category — scope
discipline, abstraction level, error handling philosophy, comment policy.

See [_format.md](_format.md) for the entry format.

---

### Don't add defensive code for impossible cases
- **Rule:** Don't add error handling, fallbacks, or validation for scenarios that can't happen. Only validate at system boundaries (user input, external APIs).
- **Why:** Defensive code for impossible cases hides real bugs and adds noise reviewers have to read past.
- **Applies to:** all

### Prefer the smallest correct change
- **Rule:** Prefer the smallest correct change that solves the requested problem. Don't refactor unrelated code. Don't change public APIs, database schemas, infrastructure, authentication flows, dependencies, or configuration unless required.
- **Why:** Scope creep turns a small task into a larger, riskier diff that's harder to review and revert.
- **Applies to:** all

### Reuse before you build
- **Rule:** Search for existing implementations, utilities, components, services, and patterns before creating new ones, and follow existing project conventions before introducing new ones.
- **Why:** Duplicated or inconsistent patterns are a common source of long-term maintenance cost.
- **Applies to:** all

### Act autonomously on straightforward tasks
- **Rule:** Implement straightforward tasks directly. Use a short plan only for complex, ambiguous, multi-step, or high-risk tasks. Resolve obvious implementation details on your own instead of asking unnecessary questions.
- **Why:** Asking about details that have an obvious answer just slows the dev down.
- **Applies to:** all

### Check impact before touching sensitive surfaces
- **Rule:** Before modifying public APIs, exported functions, database schemas, auth, env vars, shared utilities, infrastructure, or shared components, check their usages and impact first. Check references before deleting code or renaming/removing exported functionality.
- **Why:** Changes to widely-used surfaces can silently break callers that aren't visible from the change site alone.
- **Applies to:** all

### Don't touch what the task didn't ask for
- **Rule:** Never modify generated files manually unless explicitly required. Don't modify lockfiles unless a dependency change requires it. Avoid unrelated formatting changes and large mechanical rewrites. Never overwrite or discard user changes.
- **Why:** Unrelated diffs make review harder and increase the chance of an accidental regression.
- **Applies to:** all

### Avoid unnecessary abstraction
- **Rule:** Avoid introducing factories, repositories, adapters, wrappers, managers, service layers, generic abstractions, dependency injection, or state-management systems unless the repo already follows that architecture or the problem clearly requires it. Don't prematurely abstract small amounts of duplication.
- **Why:** Premature abstraction adds indirection future readers have to unwind, often for a generality the code never uses.
- **Applies to:** all

### Definition of done
- **Rule:** Consider a task complete when the requested behavior is implemented, existing conventions are followed, relevant targeted tests/typecheck/lint pass, no unnecessary dependencies or files were introduced, no secrets were introduced, and no unrelated code was touched — then stop polishing.
- **Why:** Without a concrete stopping point, "just one more improvement" turns small tasks into open-ended ones.
- **Applies to:** all
