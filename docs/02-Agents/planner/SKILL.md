# Planner · Skills

## Tools

| Tool | Used for |
|---|---|
| `Read`, `Glob`, `Grep` | Inspect domain YAMLs, pattern files, catalog |
| `WebSearch` | Sanity-check a resource's current free-tier status |

## MCP tools

`ubc_domains`, `ubc_patterns`, `ubc_catalog`, `ubc_pattern_detail`. Read-only access — the planner never writes.

## Resource preference order

The planner prefers resources in this order:

1. `cross_subsidy` (Cloudflare-style — durable)
2. `public_good` (GitHub Education-style — gated but durable)
3. `cac_funded` (most SaaS free tiers — fine for now, may decay)
4. `community` (availability tracks donations)
5. `trial` (time-limited — flagged, not relied on)
6. `unknown` (treated as `cac_funded`)

Within the same tier, `has_guide: true` wins.

## Staleness

Resources with `verified_at` older than 90 days get a `warn` tag; 180 days becomes `stale`. The planner can be invoked with `exclude_stale=true` to skip stale entries entirely.
