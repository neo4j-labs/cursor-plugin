# Neo4j Cursor plugins

A multi-plugin [Cursor](https://cursor.com) repository maintained by Neo4j. Though it only has one plugin today, more may be added in the future. Register it as a **custom marketplace** to install every plugin from the Plugins panel, or install plugins individually.

## Plugins

| Plugin | Description |
|--------|-------------|
| [`neo4j`](plugins/neo4j/) | Official Neo4j MCP server (via `uvx`) plus skills for Cypher upgrades, driver migrations, and CLI tools |

## Install

**All plugins from this repo (recommended for teams)** — in Cursor, open Settings → Plugins → **Add marketplace** and use this repository URL. That registers a **custom** marketplace (separate from Cursor's default plugin gallery); every plugin in the table above becomes installable from the Plugins panel.

**One plugin only** — install from Cursor's public plugin gallery by plugin name, or clone this repo and reference a single plugin directory.

See each plugin's own README (linked in the table above) for prerequisites and setup.

## Development

This repo follows Cursor's multi-plugin layout:

```
.cursor-plugin/marketplace.json    # marketplace manifest
plugins/<plugin-name>/             # one directory per plugin
  .cursor-plugin/plugin.json       # plugin manifest
  mcp.json                         # optional — MCP server config
  skills/, rules/, agents/, ...    # optional components
```

- **Add a plugin**: see [`docs/add-a-plugin.md`](docs/add-a-plugin.md).
- **Validate before commit**: `node scripts/validate-template.mjs`.

## License

This repository is MIT-licensed. Individual plugins vendor or reference upstream components under their own licenses — see each plugin's README and any `UPSTREAM_LICENSE.md` files for attribution.
