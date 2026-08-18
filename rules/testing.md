# Testing

TDD expectations, what to mock vs hit for real, coverage philosophy.

See [_format.md](_format.md) for the entry format.

---

### Match verification to the size of the change
- **Rule:** Prefer targeted tests for the affected code first, then type checking, then linting, and only run broader/full suites when the change justifies it. Don't run the entire test suite for a small, isolated change.
- **Why:** Full suites are slow and expensive; targeted checks catch the same regressions for most changes at a fraction of the cost.
- **Applies to:** all

### Don't paper over failures
- **Rule:** Don't fix unrelated test failures — report them instead. Never disable a test or weaken an assertion just to make CI pass, and never suppress a compiler/linter/type error without understanding why it's firing.
- **Why:** Silencing failures hides real bugs and erodes the value of the test suite over time.
- **Applies to:** all

### Add regression tests for bug fixes
- **Rule:** For bug fixes, find the root cause, fix the root cause rather than masking the symptom, and add or update a regression test when practical — without introducing unrelated behavior changes.
- **Why:** A fix without a regression test can silently regress again later.
- **Applies to:** all
