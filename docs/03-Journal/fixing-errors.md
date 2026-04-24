# Troubleshooting Journal

Weekly notes on what broke, why, and what the fix was. These are the scars that made the protocol load-bearing.

---

## 2026-03-24 · Renaming UBC → Bricolage

**What broke.** The project shipped as "Universal Basic Compute" for its first few weeks. The name implied a commons — infrastructure that anyone was entitled to. In practice almost every "free tier" in the catalog is customer-acquisition spend, not a public good. The name was overstating the claim.

**Why it mattered.** Users were building on `trial`-classified resources (OpenAI's $5 starter credit, various "free for 12 months" tiers) and treating them like they were durable. When the credits ran out, the catalog didn't take the blame — I did, for shipping a name that implied permanence.

**The fix.** Renamed to Bricolage (Lévi-Strauss's word for "making do with what's at hand") on 2026-03-24. Added the `free_tier_type` classification so the planner can explicitly mark what's durable (`cross_subsidy`, `public_good`) versus what's CAC-funded. Kept the `ubc_` prefix on MCP tools for backward compatibility — the prefix is now a stable token, not a claim.

---

## 2026-03-23 · Catalog staleness

**What broke.** A user ran `/build` with a plan that included Heroku's free PostgreSQL tier. The planner happily suggested it. The assembler scaffolded the project against it. Deploy failed — Heroku killed the free tier in late 2022.

**Why it mattered.** The catalog had no concept of time. A resource that was accurate in 2022 looked the same to the planner as one verified yesterday. Free tiers are decaying assets; the catalog was treating them like stone.

**The fix.** Added `verified_at` to every resource. Entries older than **90 days** now carry a `warn` tag; older than **180 days**, `stale`. `ubc_catalog` surfaces both tags in every response. The planner accepts `exclude_stale=true` to filter them out entirely. Re-verified the whole compute catalog on 2026-03-23 and removed Heroku, the old Railway free tier, and three others that were gone.

---

## 2026-03-18 · User-scaffolded domains looked blessed

**What broke.** The discovery agent scaffolded a new `finance` domain for a user. The next day a different user asked the planner for finance advice, got recommendations from the scaffolded catalog, and had no idea the entries had never been verified by a maintainer.

**Why it mattered.** The whole protocol is load-bearing *because* every resource is validated. A domain scaffolded from a web search is meaningfully less trustworthy than one that shipped with the plugin. The agents had no way to say that.

**The fix.** Added `trust_level` to every domain: `blessed` (shipped with plugin, reviewed), `user_scaffolded` (local scaffold, not reviewed), `external` (future: signed registry). Discovery now marks all new domains as `user_scaffolded` by default via `ubc_create_domain`. Master and planner both surface the flag in every summary. User-scaffolded content still works — it just wears its hat.

---

## 2026-03-15 · `config.toml` leak in a screenshot

**What broke.** During the Week 2 workshop I pasted a terminal screenshot into the cohort Slack. It showed `.ubc/access/compute/openai.token.enc` — only the filename, but the filename made it obvious that credentials were on disk. One cohort member opened an issue asking whether the file contained plaintext.

**Why it mattered.** It didn't — tokens are AES-256-GCM encrypted at rest — but the screenshot also happened to include the shell prompt with an Apify token (prefix redacted) visible in the environment export. That was a real leak.

**The fix.** Two changes:

1. Every raw `config.toml` now uses placeholder tokens like `YOUR_APIFY_TOKEN`, substituted at runtime from the encrypted store. The raw file never contains a real credential.
2. Added `.ubc/` to the plugin's own `.gitignore` *and* to the `config.toml` template.
3. Standing pre-push grep against the two common credential-prefix patterns (OpenAI-style bearer tokens and any literal `api` followed by underscore and `key`). Both checks must return empty before any push. Wired into the pre-commit hook.

---

## 2026-03-10 · Assembler shipped a broken blog

**What broke.** Assembler ran the `blog-ai` pattern end-to-end. Site deployed to Vercel. Homepage worked. Every individual post returned 500. User reported it the next day.

**Why it mattered.** The assembler's "verify" step was checking `HTTP 200` on the root URL only. A pattern with five pages needs five verifications, not one.

**The fix.** Assembler now reads `outcome_types` from the domain and the pattern's `verification_routes` list. For `deployed_app` outcomes, it probes every route the pattern declares. The bug manifested because the Supabase connection string in the edge function had a typo — the new verifier caught it on the second deploy.

---

## 2026-03-05 · Protocol schemas rejected valid YAML

**What broke.** A discovery-agent run produced a `resource.yaml` with `verified_at: 2026-03-05` (no quotes). The Zod loader rejected it because the schema was parsing the field as a string. Silent failure — the discovery agent thought it had written the file successfully.

**Why it mattered.** YAML is forgiving about date-string ambiguity. Code must not be.

**The fix.** Schemas in `tools/src/schemas.ts` now explicitly coerce date-like fields with `z.coerce.date().transform(d => d.toISOString().slice(0, 10))`. Invalid entries fail loudly to stderr rather than silently. Added a test to the plugin repo: load every shipped resource YAML, assert each parses.

---

## Ongoing · PicoClaw reliability

PicoClaw on GitHub Actions is the default infra recommendation, but GitHub Actions has a 2,000-minute/month free budget that a chatty agent can exhaust. Tracking whether daily catalog-refresh jobs start brushing the limit at around 25 active users. Will graduate to MiniClaw-on-Cloudflare once the numbers force it.
