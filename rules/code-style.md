# Code Style

Formatting, naming, and language-level conventions.

See [_format.md](_format.md) for the entry format.

---

### Don't suppress TypeScript errors to make them go away
- **Rule:** Don't resolve TypeScript errors with `any`, `@ts-ignore`, `@ts-expect-error`, or `eslint-disable` unless there's a documented technical reason and no safer practical alternative.
- **Why:** Suppressing the type checker hides real bugs instead of fixing them and erodes the value of typing over time.
- **Applies to:** TypeScript projects
