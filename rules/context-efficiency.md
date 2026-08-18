# Context and Token Efficiency

How the agent should explore a repo without burning context on things that
don't move the task forward.

See [_format.md](_format.md) for the entry format.

---

### Use progressive context discovery
- **Rule:** Start from the explicitly mentioned file/feature, then expand in this order: direct references/dependencies → relevant tests → adjacent implementation → broader repo context only if still needed. Never begin with a repository-wide scan.
- **Why:** Most tasks only touch a small slice of the repo; scanning everything burns tokens without improving the fix.
- **Applies to:** all

### Stop investigating once you have enough
- **Rule:** Prefer targeted searches over broad exploration. Don't re-read unchanged files or re-summarize already-understood code. Stop investigating once there's enough evidence to implement safely.
- **Why:** Exploration has diminishing returns; certainty beyond "enough to be safe" isn't worth the extra tokens and time.
- **Applies to:** all

### Keep reasoning and updates concise
- **Rule:** Keep reasoning, progress updates, and final explanations concise. Batch related searches and edits when practical.
- **Why:** Verbose narration doesn't help the dev and spends context budget that could go toward the actual work.
- **Applies to:** all
