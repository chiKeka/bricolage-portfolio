# Guide · Skills

## Tools

| Tool | Used for |
|---|---|
| `Read`, `Glob`, `Grep` | Load resource guide YAMLs |
| `Bash` | Run test API calls to verify a newly captured token works |
| `WebSearch`, `WebFetch` | Follow current signup flows when the guide YAML is stale |

## MCP tools

- `ubc_resource_guide` — fetch a resource's full setup walkthrough
- `ubc_store_access` — encrypted token storage (see below)
- `ubc_update_status` — mark a resource as acquired

## Access handling

- **Never** display full API keys, tokens, or secrets in conversation output.
- Tokens stored via `ubc_store_access` are encrypted at rest with AES-256-GCM in `.ubc/access/{domain}/`.
- `ubc_store_access` validates each token against a per-resource regex *before* encrypting — bad tokens fail fast.
- `ubc_get_access` masks values unless `reveal=true`; every reveal is audited.
- The `.ubc/` directory is gitignored by default — the guide reminds the user to keep it that way.
