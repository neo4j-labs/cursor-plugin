# Neo4j Cursor plugin

Register the [official Neo4j MCP server](https://github.com/neo4j/mcp) and three [Neo4j Contrib skills](https://github.com/neo4j-contrib/neo4j-skills) inside Cursor.

## What's included

| Component | Source | Purpose |
|-----------|--------|---------|
| MCP server `neo4j` | `neo4j-mcp-server` on PyPI (wraps the official Go binary from `neo4j/mcp`) | `get-schema`, `read-cypher`, `write-cypher`, `list-gds-procedures` against a Neo4j instance |
| Skill `neo4j-cli-tools-skill` | `neo4j-contrib/neo4j-skills` | Use when working with Neo4j CLIs: `neo4j-admin`, `cypher-shell`, `aura-cli`, `neo4j-mcp` |
| Skill `neo4j-cypher-skill` | `neo4j-contrib/neo4j-skills` | Use when upgrading Neo4j 4.x/5.x Cypher queries to 2025.x/2026.x |
| Skill `neo4j-migration-skill` | `neo4j-contrib/neo4j-skills` | Use when upgrading Neo4j drivers (.NET, Go, Java, JavaScript, Python) across major versions |

## Prerequisites

1. **`uv`** — the MCP server is run via `uvx`:
   ```sh
   brew install uv
   # or: curl -LsSf https://astral.sh/uv/install.sh | sh
   ```
2. **A Neo4j instance** running Neo4j 5.26.19+ with the [APOC plugin](https://neo4j.com/docs/apoc/current/) installed. AuraDB, local Docker, or a managed install all work.
3. **Connection credentials** exposed as environment variables (see below).

## Setup

### 1. Set environment variables

The MCP server reads these from your environment (export them in your shell profile, or set them in Cursor's MCP env UI):

| Variable | Required | Example |
|----------|----------|---------|
| `NEO4J_URI` | yes | `neo4j+s://xxxxxxxx.databases.neo4j.io` or `bolt://localhost:7687` |
| `NEO4J_USERNAME` | yes | `neo4j` |
| `NEO4J_PASSWORD` | yes | *your password* |
| `NEO4J_DATABASE` | no | `neo4j` (default) |
| `NEO4J_READ_ONLY` | no | `true` to disable `write-cypher` |

### 2. Enable the plugin in Cursor

Install this plugin from the marketplace, then reload the Cursor window (Cmd+Shift+P → "Developer: Reload Window"). On first invocation, `uvx` downloads `neo4j-mcp-server` (the official Go binary, constrained to `>=1.5,<2`) and caches it. To pick up a newer 1.x release, run `uv cache clean neo4j-mcp-server`.

### 3. Verify

In a Cursor chat, ask: *"Use the neo4j MCP server to show the schema."* Expect `get-schema` to return node labels, relationship types, and properties.

## MCP tools exposed

| Tool | Description |
|------|-------------|
| `get-schema` | Node labels, relationship types, property keys with a sampled inference of types |
| `read-cypher` | Run read-only Cypher |
| `write-cypher` | Run write Cypher (disabled when `NEO4J_READ_ONLY=true`) |
| `list-gds-procedures` | List available Graph Data Science procedures if GDS is installed |

## Skills

All three skills auto-trigger on relevant prompts (e.g. *"help me upgrade this Cypher query from 5.x to 2025"* activates `neo4j-cypher-skill`). They use `WebFetch` (and `Bash` for the CLI tools skill) to pull the latest official Neo4j docs at runtime, so guidance stays current.

## Multiple databases

For additional databases, duplicate the `neo4j` entry in `mcp.json` under a different key (e.g. `neo4j-staging`) with that database's credentials. Cursor will surface both servers.

## Attribution

- **MCP server** — [github.com/neo4j/mcp](https://github.com/neo4j/mcp) (GPL-3.0). Not bundled; `uvx` downloads the PyPI wheel [`neo4j-mcp-server`](https://pypi.org/project/neo4j-mcp-server/) at runtime.
- **Skills** — vendored from [github.com/neo4j-contrib/neo4j-skills](https://github.com/neo4j-contrib/neo4j-skills) (MIT). See [`skills/UPSTREAM_LICENSE.md`](skills/UPSTREAM_LICENSE.md) for the upstream commit SHA and license text.
