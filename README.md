# my-agents

A personal library of rules and preferences for how AI coding agents
(Claude Code, or any other model reading `CLAUDE.md` / `AGENTS.md` files)
should work in *other* projects.

This repo has no `CLAUDE.md` of its own — it isn't a project to work in,
it's the source material you point an agent at when setting up or updating
one. Store a rule here once, and reuse it every time you start something new
instead of re-explaining the same preference project after project.

## Layout

Rules live in [`rules/`](rules/), split by topic instead of one giant file.
That way an importing prompt can pull just what's relevant to a given
project (a CLI tool doesn't need frontend rules) instead of ingesting
everything every time.

| File | Covers |
|---|---|
| [`rules/general.md`](rules/general.md) | Cross-cutting principles — scope discipline, abstraction level, error handling, comments, definition of done |
| [`rules/context-efficiency.md`](rules/context-efficiency.md) | Progressive context discovery, when to stop exploring, keeping updates concise |
| [`rules/code-style.md`](rules/code-style.md) | Formatting, naming, language-level conventions |
| [`rules/git-workflow.md`](rules/git-workflow.md) | Commit practices, branching, PR conventions, what's destructive enough to confirm first |
| [`rules/testing.md`](rules/testing.md) | TDD expectations, what to mock vs. hit for real, coverage philosophy |
| [`rules/security.md`](rules/security.md) | Secrets, input validation, injection, authZ, data exposure, dependency trust |
| [`rules/database.md`](rules/database.md) | Query performance, data integrity, migration safety |
| [`rules/infrastructure.md`](rules/infrastructure.md) | Production and deployment-config safety |
| [`rules/tooling.md`](rules/tooling.md) | Preferred package managers, libraries, CLIs, stack defaults |
| [`rules/dev-environment.md`](rules/dev-environment.md) | Process management — dev servers, ports, what the agent may run itself vs. leave to the dev |
| [`rules/planning.md`](rules/planning.md) | How planning requests get handled and documented |
| [`rules/communication.md`](rules/communication.md) | Verbosity, tone, when the model should ask vs. just act |
| [`rules/project-setup.md`](rules/project-setup.md) | Scaffolding defaults, how agent instruction files themselves should be structured |

Add a new file to `rules/` for a new topic and add a row here — the table
is the index, so keep it in sync.

Every rule follows one entry format, documented in
[`rules/_format.md`](rules/_format.md):

```markdown
### <Short imperative title>
- **Rule:** <the directive, phrased exactly as it should read in the target file>
- **Why:** <the reasoning>
- **Applies to:** <all | a language/framework | a project shape>
```

That format is deliberately richer than what should land in a target
project's `CLAUDE.md`. [`rules/_import-strategy.md`](rules/_import-strategy.md)
defines how importing compresses it down and keeps multiple imported (and
pre-existing) rules from contradicting each other — every prompt below
follows it rather than restating it.

## Adding a rule

Capture a rule here the moment it's established, not later from memory:

- You corrected an agent's approach in some other project and want it to
  stick everywhere, not just there.
- You confirmed an unusual approach worked and want to keep doing it.
- You noticed yourself giving the same instruction in a second project.

Put it in the matching category file using the format above. If you're
mid-session in another project, just ask the agent: *"add this as a rule
to my-agents: \<what you want it to remember>"* — it can fetch the current
file from the GitHub URL (see below) and either commit the addition
directly if it has push access, or hand you the text to add yourself.

Keep rules **global**. If something only makes sense for one specific repo,
it belongs in that repo's own `CLAUDE.md`, not here.

## Prompts

[`rules/`](rules/) holds atomic, injectable statements. [`prompts/`](prompts/)
holds full reusable task templates you paste wholesale into a session, rather
than merge into a `CLAUDE.md`.

| File | Use it when |
|---|---|
| [`prompts/audit-agent-instructions.md`](prompts/audit-agent-instructions.md) | You want an agent to inspect a repo and rewrite its `CLAUDE.md`/`AGENTS.md`/scoped instruction files for security, token efficiency, and safety |

Add a prompt here the same way you add a rule: when you catch yourself
retyping (or re-explaining) the same multi-step instruction in a second
project, save it as a file under `prompts/` and add a row above.

## Using it in a new project

This repo is on GitHub at `github.com/gelipundio/my-agents`. No need to
clone it — point an agent at the raw file URLs directly. Copy-paste one of
these (base URL: `https://raw.githubusercontent.com/gelipundio/my-agents/main/`):

**Bootstrapping a brand-new project's `CLAUDE.md` / `AGENTS.md`:**

> Fetch `https://raw.githubusercontent.com/gelipundio/my-agents/main/README.md`
> to see the available rule categories, then fetch the ones relevant to this
> project's stack from
> `https://raw.githubusercontent.com/gelipundio/my-agents/main/rules/<file>.md`.
> Follow
> `https://raw.githubusercontent.com/gelipundio/my-agents/main/rules/_import-strategy.md`
> for how to merge them into this project's `CLAUDE.md`/`AGENTS.md` — it
> covers filtering by stack, deduping, resolving contradictions, and
> keeping the result short.

**Pulling in just a couple of categories:**

> Fetch
> `https://raw.githubusercontent.com/gelipundio/my-agents/main/rules/git-workflow.md`
> and
> `https://raw.githubusercontent.com/gelipundio/my-agents/main/rules/testing.md`,
> and merge them into this project's `CLAUDE.md`, following
> `https://raw.githubusercontent.com/gelipundio/my-agents/main/rules/_import-strategy.md`.

**Ad hoc, without writing anything down:**

> Before you answer, fetch
> `https://raw.githubusercontent.com/gelipundio/my-agents/main/rules/testing.md`
> for how I like tests structured.
