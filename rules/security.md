# Security

Secret handling, dependency trust, review expectations for
security-sensitive changes.

See [_format.md](_format.md) for the entry format.

---

### Never expose secrets
- **Rule:** Never hardcode credentials, tokens, API keys, passwords, private keys, or connection strings. Never commit `.env` files or secrets. Never expose server secrets to client code. Never log credentials, tokens, passwords, or other sensitive data.
- **Why:** Leaked secrets are one of the most common and costly incident classes, and entirely preventable by habit.
- **Applies to:** all

### Treat external input as untrusted
- **Rule:** Validate input at system boundaries using the project's existing schema-validation solution. Perform security-relevant validation server-side, not just client-side. Prefer allowlists over denylists where appropriate.
- **Why:** Client-side checks can always be bypassed; the server is the only trust boundary that matters.
- **Applies to:** all

### Prevent injection
- **Rule:** Use parameterized queries or the existing ORM/query builder — never concatenate untrusted values into SQL, pass them directly into shell commands, or run them through `eval`/dynamic code execution/unsafe deserialization.
- **Why:** Injection remains one of the most exploitable and most avoidable vulnerability classes.
- **Applies to:** all

### Enforce authorization server-side
- **Rule:** Authentication does not imply authorization — verify resource-level access server-side on every request. Never rely on client-side checks or hidden UI elements to gate access.
- **Why:** Anything enforced only in the client can be bypassed by calling the API directly.
- **Applies to:** all

### Minimize sensitive-data exposure
- **Rule:** Don't expose internal database fields, stack traces, SQL errors, credentials, or infrastructure details to clients. Avoid unnecessary PII logging.
- **Why:** Verbose errors and over-broad responses are a common source of accidental data leaks.
- **Applies to:** all

### Justify new dependencies
- **Rule:** Prefer existing dependencies over adding new ones for trivial functionality. Any new dependency should be justified, actively maintained, and compatible with the project. Respect the project's lockfile conventions.
- **Why:** Every dependency is a supply-chain liability and maintenance cost, not just a convenience.
- **Applies to:** all
