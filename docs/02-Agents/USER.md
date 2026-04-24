# Operator · Profile

**Name:** Bruno (GitHub: [@chiKeka](https://github.com/chiKeka))
**Cohort:** Super Individual Workshop · Founding Member track
**Primary project:** [Bricolage](https://github.com/chiKeka/bricolage)

## What I want Bricolage to do for me

- Keep a complete, verified map of the free-tier services I could plausibly build with.
- Make credentialing painless — walk through signup once, store tokens encrypted, never display secrets in the chat buffer.
- Ship the outcome in the same session the goal was described. No "come back tomorrow."
- Be honest about decay. If a free tier is known dead (Heroku, Railway), the planner must refuse to recommend it — not silently fail at deploy time.

## What I don't want

- Agents that pretend their scaffolded output is blessed when it isn't (`trust_level` must be surfaced).
- Recommendations based on stale catalog data (staleness tags exist so the planner can exclude them).
- Any credential shown in plaintext in a conversation log.

## How I build

- I prefer one bundled PR over many small ones for refactors in the same area.
- I like terse responses with no trailing summaries — I can read the diff.
- YAML configs over JSON when humans will edit them. Zod schemas for machine validation.
