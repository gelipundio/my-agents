# Import strategy

The process to follow whenever rules from this repo get merged into a
target project's `CLAUDE.md` / `AGENTS.md`, so the result stays short and
internally consistent. Every "using it in a new project" prompt in the root
[README.md](../README.md) points here instead of restating this.

## 1. Read before you write

Read the target file(s) in full before adding anything. You can't dedupe or
detect conflicts against content you haven't read.

## 2. Filter before you merge

- Only pull rules whose **Applies to** matches this project's actual stack
  — check `package.json`/`pyproject.toml`/etc., don't guess from the
  category filename alone.
- Skip anything the project's file already covers, even if worded
  differently.

## 3. Resolve contradictions, don't stack them

- Imported rule conflicts with something already in the target file? Keep
  the existing project-specific rule, drop the import — project-specific
  knowledge beats a general default.
- Two imported rules conflict with each other (e.g. a stricter personal git
  rule vs. a looser stack default)? Keep the stricter/safer one.
- Never write both sides of a contradiction into the same file "to be
  safe." Pick one and state it once.
- If a conflict is genuinely ambiguous and consequential, flag it in your
  summary instead of guessing.

## 4. Compress on the way in

The library format (`Rule` + `Why` + `Applies to`) is for maintaining
*this* repo, not for pasting verbatim into a target file:

- Import only the **Rule**, phrased as a short imperative (MUST / MUST NOT
  / SHOULD).
- Drop **Why** unless a single clause prevents a real misreading.
- Drop **Applies to** — it already did its job as a filter before import.
- Merge related entries into one bullet instead of one bullet per source
  rule.

## 5. Cap the size

- A project's root `CLAUDE.md`/`AGENTS.md` should be skimmable in under a
  minute. If the merged result runs long, move stack-specific bulk into
  scoped files instead (see [`project-setup.md`](project-setup.md)).
- Every line must earn its place: if removing it wouldn't change agent
  behavior on this specific project, don't add it.

## 6. Self-check before finishing

Re-read the merged file once, end to end, specifically looking for two
lines that instruct opposite things. Fix or remove one before calling the
import done.
