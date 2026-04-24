# Bricolage Portfolio

Week-4 Proof-of-Work submission for the Super Individual Workshop. A public portfolio that documents [Bricolage](https://github.com/chiKeka/bricolage) — an agentic system that turns free-tier resources into working outcomes. Deployable on OpenClaw, ZeroClaw, or any compatible agent runtime running on free-tier compute.

**Live site:** https://chikeka.github.io/bricolage-portfolio/
**Source repo:** https://github.com/chiKeka/bricolage

## What's here

```
bricolage-portfolio/
├── docs/                      <- All site content (MkDocs)
│   ├── index.md               <- Manifesto
│   ├── 02-Agents/
│   │   ├── USER.md            <- Operator profile
│   │   ├── STYLE.md           <- Shared agent voice/style
│   │   ├── master/            <- IDENTITY + SOUL + SKILL per agent
│   │   ├── planner/
│   │   ├── guide/
│   │   ├── assembler/
│   │   ├── discovery/
│   │   └── infra/
│   ├── 03-Journal/            <- What broke and why
│   └── 04-Showcase/           <- Bricolage in action
├── 01-Configuration/          <- Sanitised config.toml template
├── mkdocs.yml                 <- Material theme config
└── .gitignore
```

## Local preview

```bash
python3 -m venv .venv
.venv/bin/pip install mkdocs-material
.venv/bin/mkdocs serve
# open http://127.0.0.1:8000/bricolage-portfolio/
```

## Publish

```bash
.venv/bin/mkdocs gh-deploy
```

MkDocs builds the site, pushes it to the `gh-pages` branch, GitHub Pages serves it. No CI/CD config required.

## Security

- Every credential field is a placeholder (`YOUR_*`). The raw `config.toml` with real tokens is gitignored.
- Pre-push check: grep for common credential-prefix patterns must return empty.
- Real Bricolage tokens are AES-256-GCM encrypted at rest under `.ubc/access/` on the operator's machine — never committed.
