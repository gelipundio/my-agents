# Rule entry format

Every rule in this directory follows the same shape so it can be skimmed,
diffed, and lifted straight into a target project's `CLAUDE.md` / `AGENTS.md`.

```markdown
### <Short imperative title>
- **Rule:** <the directive, phrased exactly as it should read in the target file>
- **Why:** <the reasoning — an incident, a preference, a tradeoff>
- **Applies to:** <all | a language/framework | a project shape, e.g. "Node.js repos", "anything with CI">
```

Guidelines:

- **Rule** should be copy-pasteable. Write it the way you'd want it to read
  inside someone's `CLAUDE.md`, not as a note to yourself.
- **Why** is what lets future-you (or Claude) judge edge cases and decide
  whether a rule still applies to a new situation, instead of following it
  blindly.
- **Applies to** lets an importing prompt filter — e.g. skip frontend rules
  when bootstrapping a CLI tool.
- Keep one rule per entry. If a rule needs three sub-bullets to explain, it's
  probably two rules.
- New category needed? Add a file to `rules/`, follow this format, and add a
  row to the table in the root [README.md](../README.md).
