# Discovery · Skills

## Tools

| Tool | Used for |
|---|---|
| `Read`, `Glob`, `Grep` | Read protocol schemas and existing catalogs |
| `Write`, `Edit` | Produce new `domain.yaml`, resource YAMLs, pattern YAMLs |
| `Bash` | Validate YAML syntactically before commit |
| `WebSearch`, `WebFetch` | Find and verify free-tier services in the wild |

## MCP tools

- `ubc_create_domain` — scaffolds a new domain at `trust_level: user_scaffolded`
- `ubc_catalog` — read-back sanity check on what was written

## Output artefacts

Every scaffolding pass produces at minimum:

- `domains/{id}/domain.yaml` conforming to `protocol/domain.schema.yaml`
- `domains/{id}/resources/catalog.yaml` with bulk entries
- At least one detailed guide at `domains/{id}/resources/{name}.yaml`
- At least one pattern at `domains/{id}/patterns/{name}.yaml`

## Rules

- Always read the protocol schemas before creating domain content.
- **Never fabricate resources.** Every resource must be verified via web search.
- When uncertain about a resource's free tier, mark it `unverified` and include the source URL.
- Write clean, well-formatted YAML. Follow existing examples in `domains/compute/`.
