# Showcase

Bricolage agents in action — real sessions, edited for brevity.

---

## 1. Master → Planner → Guide → Assembler: a blog in one session

**User:** *I want to build a blog with AI summarisation. Free only.*

**Master:**
> Good goal. Let me check what we've got.
> Compute domain is `blessed` and verified 2026-03-23. I'll hand you to the planner.

**Planner output:**

```yaml
domain: compute
goal: AI-summarising blog
pattern: blog-ai
resources:
  - name: GitHub
    role: source repo + Actions CI
    has_guide: true
  - name: Vercel
    role: hosting + edge functions
    has_guide: true
  - name: Supabase
    role: posts + summaries table
    has_guide: true
  - name: OpenAI
    role: gpt-4o-mini for summarisation
    has_guide: true
steps:
  - create public GitHub repo
  - scaffold Next.js with Supabase + OpenAI SDK
  - wire Vercel deploy
  - write the /api/summarise edge function
  - verify end-to-end with a seed post
warnings:
  - OpenAI free credit is classified `trial` — will decay once the $5 starter is used
  - Supabase free tier: 500 MB, pauses after 7 days inactive
estimated_effort: 45 min
```

**Guide:** Walked through GitHub signup → Vercel OAuth → Supabase project → OpenAI API key. Stored four tokens via `ubc_store_access` with regex validation. None of the four were ever printed in the chat.

**Assembler:** Scaffolded `create-next-app`, wrote `lib/supabase.ts` and `app/api/summarise/route.ts`, ran `vercel --prod`, verified `/`, `/posts`, and `/posts/seed-post` all returned 200.

**Total time:** 38 minutes from "I want a blog" to `https://brunos-ai-blog.vercel.app/` being live.

---

## 2. Discovery: scaffolding a domain on demand

**User:** *I want to learn data science for free but I don't know where to start.*

**Master:** No matching domain. Delegating to discovery.

**Discovery:**
1. Called `ubc_create_domain` with `id: education`, `trust_level: user_scaffolded`.
2. Ran 14 web searches. Verified free tiers on: fast.ai, MIT OCW, Kaggle Learn, freeCodeCamp, Coursera audit track, StatQuest, 3Blue1Brown, The Odin Project, Full Stack Open, Harvard CS50, DeepLearning.AI (audit), Google ML Crash Course.
3. Wrote 12 resource YAMLs under `domains/education/resources/` and a bulk entry for 34 adjacent resources in `catalog.yaml`.
4. Authored the starter pattern `ds-foundations.yaml`: Khan Academy math → StatQuest stats → Kaggle Learn Python → fast.ai → Kaggle competition.
5. Reported back: **"Domain `education` scaffolded. `trust_level: user_scaffolded` — the catalog is my best research, not a maintainer's review."**

That honesty flag is the feature.

---

## 3. Infra: PicoClaw on GitHub Actions

**User:** *I want the catalog to re-verify itself weekly.*

**Infra:** Recommended PicoClaw on GitHub Actions because the task is periodic and the user's whole project is a public repo.

Wrote `.github/workflows/catalog-refresh.yaml`:

```yaml
name: Catalog Refresh
on:
  schedule:
    - cron: "0 14 * * 1"  # Mondays 14:00 UTC
jobs:
  refresh:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npx tsx tools/scripts/verify-catalog.ts --write
      - uses: peter-evans/create-pull-request@v6
        with:
          commit-message: "chore: refresh catalog staleness tags"
          branch: auto/catalog-refresh
          title: "Weekly catalog refresh"
```

First run took 4 minutes of the monthly 2,000-minute budget. PR arrived with 11 `verified_at` bumps and two newly-stale entries auto-flagged.

---

## Screenshots

The deployed site, the encrypted-access directory listing, and the pre-push grep check all live in `/04-Showcase/images/` in the repo. (Placeholder — add screenshots before submitting to the cohort.)

---

## What this is proof of

- Six agents, one protocol.
- 411 resources, every one verified and dated.
- A credential store that encrypts everything and never prints a secret.
- A domain model that lets the system grow on demand without pretending the new parts are blessed.

This is the fortress. The site you're reading is the window into it.
