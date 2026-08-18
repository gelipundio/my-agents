# Tooling

Preferred package managers, libraries, CLIs, and stack defaults.

See [_format.md](_format.md) for the entry format.

---

### Keep the codebase indexed with codebase-memory-mcp
- **Rule:** Use the `codebase-memory-mcp` tools (`search_graph`, `trace_path`, `get_code_snippet`, `query_graph`, `get_architecture`, `search_code`) for code exploration instead of raw grep/read where possible. If the project isn't indexed yet, run `index_repository` first; if the MCP server isn't configured for this project, ask the dev to add it.
- **Why:** Graph-augmented search finds the right code with far fewer tokens than manual exploration.
- **Applies to:** any project with the codebase-memory-mcp server available
