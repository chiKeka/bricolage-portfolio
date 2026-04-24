# Welcome to Bricolage Lab

Built on the ZeroClaw framework · Super Individual Workshop, Week 4 · Proof of Work

---

## Why I built this

Free-tier services from GitHub, Vercel, Supabase, OpenAI, Cloudflare, and hundreds of others collectively provide enough capacity to build, deploy, and run real applications without paying for infrastructure. The problem is not that the parts don't exist — it's that nobody knows which parts exist, which ones still work, and how to combine them.

**Bricolage** is an agent system — six specialists that know which resources exist, how to claim them, and how to combine them into something that runs. It's designed to be deployed on **OpenClaw** (with MiniClaw and PicoClaw as lighter-weight options); a Claude Code plugin is also available as an interactive client.

The name is from Lévi-Strauss: *bricolage* is the craft of making do with what's at hand. Scan the available parts, pick the ones that fit the goal, assemble. That is what these agents do.

In the AI era, I want to own assets, not just use tools. This lab documents my agent architecture, the protocol that holds it together, and everything that broke along the way.

---

## What Bricolage is

A domain-agnostic protocol for assembling free resources into outcomes. The system ships with a **compute domain** (411 unique cloud services, verified 2026-03-23). Other domains — education, health, finance, research — are scaffolded on the fly by the discovery agent when a user brings a goal the existing domains don't cover.

- **6 agents** — master, planner, guide, assembler, discovery, infra
- **411 free resources** — 10 detailed guides + 408 bulk catalog entries
- **5 assembly patterns** — blog-ai, portfolio, saas-starter, ai-chatbot, api-backend
- **10 MCP tools** — catalog browsing, status tracking, encrypted token storage
- **Free-tier durability classification** — every resource tagged `cross_subsidy`, `public_good`, `cac_funded`, `community`, `trial`, or `unknown` so the planner can prefer tiers likely to outlast the project
- **Staleness tracking** — every resource carries a `verified_at` date; entries get a `warn` tag at 90 days, `stale` at 180 days

The source repo lives at **[github.com/chiKeka/bricolage](https://github.com/chiKeka/bricolage)**. A ZeroClaw deployment is on the roadmap — today the system is runnable via its Claude Code plugin and via the platform-agnostic MCP server. This site is the portfolio: the methodology, the agent architecture, and the journal of what broke along the way.

---

## Lead agents

The master agent is the entry point. It routes goals to five specialists:

- [**master**](02-Agents/master/IDENTITY.md) — entry point; reads the goal, picks the domain, delegates
- [**planner**](02-Agents/planner/IDENTITY.md) — reads the catalog, picks the minimal set of resources
- [**guide**](02-Agents/guide/IDENTITY.md) — walks the user through account creation and token capture
- [**assembler**](02-Agents/assembler/IDENTITY.md) — takes the plan + acquired access and builds the outcome
- [**discovery**](02-Agents/discovery/IDENTITY.md) — scaffolds a new domain when a goal fits nowhere
- [**infra**](02-Agents/infra/IDENTITY.md) — deploys the runtime onto user-provisioned free compute

---

## Navigation

- [Troubleshooting journal](03-Journal/fixing-errors.md) — what broke along the way
- [Showcase of best outputs](04-Showcase/best-results.md) — Bricolage agents in action
- [Source code on GitHub](https://github.com/chiKeka/bricolage)

---

## The honest pitch

Free tiers are decaying assets. Heroku-in-2022 is the canonical case: a generous free tier that vanished when the unit economics changed. Bricolage treats them as such — every resource carries a verification date, every free tier gets a durability classification, and the planner can exclude stale entries. The protocol is load-bearing, not decorative.
