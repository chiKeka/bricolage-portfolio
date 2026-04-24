# Infra · Skills

## Tools

| Tool | Used for |
|---|---|
| `Read`, `Glob`, `Grep` | Inspect runtime source and existing deployments |
| `Bash` | Run `railway up`, `flyctl deploy`, `wrangler publish`, `gh workflow run` |
| `Edit`, `Write` | Author workflow YAML, Dockerfiles, `wrangler.toml`, etc. |
| `WebSearch`, `WebFetch` | Check platform docs for current free-tier limits |
| `CronCreate`, `CronDelete`, `CronList` | Manage scheduled tasks |

## Decision matrix

| User says | Recommended runtime |
|---|---|
| "I just want periodic catalog updates" | **PicoClaw** on GitHub Actions |
| "I need always-on agents responding to webhooks" | **OpenClaw** on Fly.io free machine |
| "I already built with Vercel / Cloudflare" | **MiniClaw** on the platform they're using |

## Platform caveats

- **Railway free tier** — gone (deprecated 2023). Do not recommend.
- **Heroku free tier** — gone (deprecated 2022). Do not recommend.
- **Fly.io free machines** — still available but capped; read the current limits at deploy time.
- **Vercel Hobby** — generous but subject to commercial-use restrictions. Warn the user.
- **Cloudflare Workers free** — 100k requests/day; excellent for MiniClaw.
- **GitHub Actions** — 2,000 public-repo minutes/month free; best fit for PicoClaw.
