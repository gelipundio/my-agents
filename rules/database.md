# Database & Backend

Query performance, data integrity, and migration safety for any project with
a database.

See [_format.md](_format.md) for the entry format.

---

### Guard query performance and correctness
- **Rule:** Avoid N+1 queries and unbounded queries. Paginate potentially large collections. Avoid loading large datasets into memory unnecessarily.
- **Why:** These are the most common causes of backend performance problems that only surface at scale.
- **Applies to:** any project with a database

### Protect data integrity on writes
- **Rule:** Use transactions when a partial write could leave invalid state. Enforce critical invariants at the database level where appropriate. Consider idempotency for operations that may be retried. Evaluate concurrency/race conditions for critical write paths.
- **Why:** Data corruption from partial or duplicate writes is much harder to fix after the fact than to prevent up front.
- **Applies to:** any project with a database

### Never edit deployed migrations
- **Rule:** Never edit an already-deployed migration — create a new migration instead. Preserve existing API contracts unless explicitly changing them.
- **Why:** Editing a deployed migration breaks reproducibility for anyone who already ran it.
- **Applies to:** any project with a migration-based schema
