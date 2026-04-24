# Master · Skills

## Tools

| Tool | Used for |
|---|---|
| `Read`, `Glob`, `Grep` | Inspect local state, catalogs, and configs |
| `Bash` | Run status checks |
| `WebSearch` | Verify current service availability when needed |
| `TaskCreate` / `TaskGet` / `TaskList` / `TaskUpdate` | Delegate to specialist agents |

## MCP tools

Calls `ubc_domains`, `ubc_status`, and dispatches specialists via the Agent tool. Never touches `ubc_store_access` directly — access is the guide's job.

## Known domains

Calls `ubc_domains` at runtime. The compute domain ships blessed; any other domain was user-scaffolded by [[../discovery/IDENTITY|discovery]] unless otherwise noted.

## Known patterns

Per-domain. For compute:

- `blog-ai` — Next.js blog with AI summarisation
- `portfolio` — personal site with contact form and analytics
- `saas-starter` — full-stack app with auth, database, CDN
- `ai-chatbot` — GPT chat with conversation memory
- `api-backend` — REST API on Cloudflare Workers with Postgres
