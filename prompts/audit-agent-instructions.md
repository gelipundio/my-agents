# Audit and improve agent instructions

Paste this into a fresh session in the target repo when you want an agent to
audit and rewrite that repo's own `CLAUDE.md` / `AGENTS.md` / scoped
instruction files. The atomic rules it enforces are also broken out in
[`../rules/`](../rules/) so you can pull individual ones without running the
whole audit — this file is for when you want the full pass.

---

I want you to audit and improve the AI coding-agent instructions for this repository.

Your goal is to optimize the repository's `CLAUDE.md`, `AGENTS.md`, and any scoped agent instruction files for:

1. Security
2. Reduced token/context usage
3. Faster software development
4. Safer code changes
5. Better code quality
6. Less unnecessary exploration and refactoring
7. More autonomous execution with fewer unnecessary questions
8. Efficient testing and verification

## Step 1 — Inspect the repository

Before modifying anything, inspect the repository enough to understand:

* Project structure
* Languages and frameworks
* Frontend/backend boundaries
* Database and ORM
* Authentication/authorization
* Infrastructure and deployment
* Testing tools
* Linting/type-checking tools
* Package manager
* Existing coding conventions
* Existing `CLAUDE.md`, `AGENTS.md`, or similar instruction files
* Existing repository-specific documentation that should be referenced instead of duplicated

Do NOT perform a repository-wide deep scan unless necessary.

Use progressive context discovery:

1. Inspect root configuration and instruction files.
2. Identify major application directories.
3. Inspect relevant package/config files.
4. Inspect representative implementation files only when necessary.
5. Stop once you have enough information to define appropriate rules.

Avoid wasting context by reading large numbers of unrelated files.

## Step 2 — Design the instruction hierarchy

Prefer a small global instruction file plus scoped instructions where appropriate.

For example:

```text
/
├── AGENTS.md
├── CLAUDE.md
├── frontend/
│   └── AGENTS.md
├── backend/
│   └── AGENTS.md
└── infrastructure/
    └── AGENTS.md
```

Do NOT create scoped files unless they provide meaningful repository-specific value.

Avoid duplicating the same instructions across files.

Keep global instructions concise. Put stack-specific rules close to the code they affect.

If both `CLAUDE.md` and `AGENTS.md` are useful, avoid maintaining two large duplicated rule sets. Prefer a clear source of truth and lightweight references where supported.

## Step 3 — Add core engineering rules

The resulting instructions should enforce the following principles.

### Execution

* Prefer the smallest correct change that solves the requested problem.
* Do not refactor unrelated code.
* Search for existing implementations, utilities, components, services, and patterns before creating new ones.
* Follow existing project conventions before introducing new patterns.
* Prefer modifying existing code over creating unnecessary abstractions or files.
* Do not change public APIs, database schemas, infrastructure, authentication flows, dependencies, or configuration unless required.
* Implement straightforward tasks directly.
* Use short plans only for complex, ambiguous, multi-step, or high-risk tasks.
* Resolve obvious implementation details autonomously instead of asking unnecessary questions.

### Planning

* When asked to help plan something, write the plan to a file under `/plan` automatically — do not wait to be asked to document it.

### Context and token efficiency

* Read only files necessary for the current task.
* Never begin with a repository-wide scan.
* Start from explicitly mentioned files/features and expand context progressively.
* Search for symbols/references before opening large files.
* Prefer targeted searches over broad exploration.
* Prefer relevant code sections and diffs over complete-file inspection when possible.
* Do not repeatedly read unchanged files.
* Do not repeatedly summarize already-understood code.
* Batch related searches and edits when practical.
* Stop investigating once enough evidence exists to implement safely.
* Keep reasoning, progress updates, and final explanations concise.

Use this context discovery order:

1. Requested file or feature
2. Direct references/dependencies
3. Relevant tests
4. Adjacent implementation
5. Broader repository context only if still necessary

### Security

Security takes priority over convenience.

Enforce rules covering:

#### Secrets

* Never hardcode credentials, tokens, API keys, passwords, private keys, or connection strings.
* Never commit `.env` files or secrets.
* Never expose server secrets to client code.
* Never log credentials, tokens, passwords, or sensitive information.

#### Input

* Treat external input as untrusted.
* Validate input at system boundaries.
* Prefer the project's existing schema validation solution.
* Perform security-relevant validation server-side.
* Prefer allowlists when appropriate.

#### Injection

* Use parameterized database queries or the existing ORM/query builder.
* Never concatenate untrusted values into SQL.
* Never pass untrusted values directly into shell commands.
* Avoid `eval`, dynamic code execution, and unsafe deserialization.

#### Authentication and authorization

* Authentication does not imply authorization.
* Authorization must be enforced server-side.
* Resource-level access must be verified.
* Never rely exclusively on client-side authorization or hidden UI elements.

#### Data

* Minimize sensitive-data exposure.
* Do not expose internal database fields unintentionally.
* Avoid unnecessary PII logging.
* Do not expose stack traces, SQL errors, credentials, or infrastructure details to clients.

#### Dependencies

* Prefer existing dependencies.
* Avoid adding packages for trivial functionality.
* New dependencies should be justified, maintained, and compatible with the project.
* Respect the project's lockfile/package-management conventions.

## Step 4 — Add change-safety rules

Include rules such as:

* Preserve backward compatibility unless explicitly changing it.
* Check usages before renaming or removing exported/public functionality.
* Check references before deleting code.
* Never modify generated files manually unless explicitly required.
* Do not modify lockfiles unless dependency changes require it.
* Avoid unrelated formatting changes.
* Avoid large mechanical rewrites.
* Never overwrite or discard user changes.

Before modifying these areas, inspect their usages and impact:

* Public APIs
* Exported functions
* Database schemas
* Authentication
* Authorization
* Environment variables
* Shared utilities
* Infrastructure
* Public/shared components

For bug fixes:

1. Identify the root cause.
2. Fix the root cause rather than masking symptoms.
3. Add/update a regression test when practical.
4. Avoid unrelated behavior changes.

## Step 5 — Add testing rules

Verification should be proportional to the change.

Preferred order:

1. Relevant targeted tests
2. Type checking for affected code
3. Linting for affected code
4. Broader test suites only when justified

Rules:

* Run targeted tests before expensive full suites.
* Do not automatically run every test for small isolated changes.
* Do not fix unrelated failures.
* Report unrelated failures instead.
* Never disable tests simply to make CI pass.
* Never weaken assertions to accommodate incorrect behavior.
* Never hide compiler/linter/type errors without understanding them.

For TypeScript, avoid solving errors using:

* `any`
* `@ts-ignore`
* `@ts-expect-error`
* `eslint-disable`

unless there is a documented technical reason and no safer practical alternative.

## Step 6 — Add simplicity rules

Prefer boring, explicit, maintainable code.

Avoid introducing unnecessary:

* factories
* repositories
* adapters
* wrappers
* managers
* service layers
* generic abstractions
* dependency injection
* state-management systems

unless the repository already follows that architecture or the problem clearly requires it.

Do not prematurely abstract small amounts of duplication.

Optimize for readability and maintainability rather than architectural cleverness.

## Step 7 — Add database/backend rules when applicable

Where relevant:

* Avoid N+1 queries.
* Avoid unbounded database queries.
* Paginate potentially large collections.
* Avoid loading large datasets into memory unnecessarily.
* Use transactions when partial writes could leave invalid state.
* Enforce critical invariants at the database level where appropriate.
* Consider idempotency for operations that may be retried.
* Never edit already-deployed migrations; create new migrations instead.
* Evaluate concurrency/race conditions for critical write operations.
* Preserve API contracts unless explicitly changing them.

Adapt these rules to the actual database/ORM/framework used by this repository.

## Step 8 — Add Git and infrastructure safety

Git:

* Never force push.
* Never use destructive reset operations unless explicitly requested.
* Never discard uncommitted user changes.
* Do not commit automatically unless requested.
* Never commit secrets.
* Verify scope before destructive operations.

Infrastructure:

* Never destroy production resources automatically.
* Treat production changes as high risk.
* Do not modify deployment/infrastructure configuration unless required by the task.
* Clearly identify changes that could affect production, data integrity, authentication, billing, or availability.

## Step 9 — Add a Definition of Done

A task should normally be considered complete when:

* Requested behavior is implemented.
* Existing project conventions are followed.
* Relevant targeted tests pass.
* Applicable type checking passes.
* Applicable linting passes.
* No unnecessary dependencies/files were introduced.
* No secrets or sensitive information were introduced.
* No unrelated code was modified.

Do not continue polishing after these conditions are satisfied unless there is a concrete reason.

## Step 10 — Optimize agent communication

Agents should finish tasks with a concise summary containing only:

* What changed
* Important technical decisions, if any
* Tests/checks performed
* Remaining issues or risks, if any

Do not:

* Repeat the original request
* Explain obvious code
* List every file inspected
* Provide long implementation walkthroughs unless requested
* Generate unnecessary documentation

## Repository-specific rules

After understanding this repository, add useful stack-specific rules.

Examples could include rules for:

* TypeScript
* React
* Next.js
* Node.js
* Python/FastAPI
* PostgreSQL
* Prisma
* AWS
* Terraform
* Vercel
* Docker
* CI/CD

However, DO NOT blindly add these examples.

Only add rules relevant to technologies actually used in this repository.

Prefer repository-specific commands such as:

```text
test command
typecheck command
lint command
build command
development command
migration command
```

when they can be determined reliably from the repository.

## Important constraint

The instruction system itself must remain token-efficient.

Do not create a giant policy document.

Every rule should earn its place by preventing a realistic failure mode or improving agent efficiency.

Remove:

* redundant rules
* obvious statements
* duplicated instructions
* excessive examples
* generic software-engineering advice that does not influence agent behavior

Prefer short, actionable rules using MUST / MUST NOT / SHOULD terminology where useful.

## Final task

Now:

1. Inspect the repository.
2. Review all existing agent instruction files.
3. Determine the best instruction hierarchy.
4. Modify or create the appropriate `CLAUDE.md` / `AGENTS.md` files.
5. Add repository-specific rules based on the actual stack.
6. Remove redundant or counterproductive existing instructions.
7. Keep the final instruction set compact and token-efficient.
8. Do not modify application code as part of this task.

After completing the changes, give me a concise summary of:

* Files created/modified
* Important rules added
* Repository-specific rules detected
* Any existing rules you removed or changed and why
