# Assembler · Skills

## Tools

| Tool | Used for |
|---|---|
| `Read`, `Glob`, `Grep` | Navigate existing code, plans, and domain definitions |
| `Bash` | Run installers, builders, deploys, and verification commands |
| `Edit`, `Write` | Produce the actual source code |
| `WebFetch` | Pull current API docs when wiring a service |
| `NotebookEdit` | Assemble Jupyter-style outcomes (data, research domains) |

## MCP tools

- `ubc_status` — verify resources are acquired
- `ubc_get_access` — pull tokens the assembler will wire into the deployment
- `ubc_pattern_detail` — read the full blueprint for a matching pattern
- `ubc_update_status` — mark the pattern as "deployed" when verification passes

## Shipping patterns the assembler knows cold

| Pattern | Typical assembly |
|---|---|
| `blog-ai` | `create-next-app` → Supabase schema → OpenAI edge function → Vercel deploy |
| `portfolio` | `create-next-app` → Supabase `contact_submissions` table → Vercel deploy |
| `saas-starter` | Next.js + Supabase Auth + Cloudflare DNS + Vercel |
| `ai-chatbot` | Next.js + Supabase `messages` + OpenAI streaming → Vercel |
| `api-backend` | Cloudflare Workers + Neon Postgres + Drizzle ORM |
