# Contributing to Job Search OS

This is a V1 open-source project built from a real job search. PRs, issues, and ideas are welcome.

---

## What's Most Useful to Contribute

**New scrapers** — `4-Company-Research/` currently covers startups.gallery (Series A/B/Seed/YC). Scrapers for other sources (Crunchbase, LinkedIn, Wellfound, etc.) would meaningfully expand coverage. Match the output CSV format of the existing scrapers so `jsos score` picks them up automatically.

**Improved prompts** — if you used a prompt and it produced something better than the default, share it. Prompts live in `2-Resume/prompts/`, `3-Outreach/email_prompt.md`, and `5-Interview-Prep/prompts/`. Improvements should be grounded in what actually worked, not theoretical rewrites.

**New situations** — `7-Situations/` only has two files. Real stuck points that aren't covered: ghosted after a final round, counter-offer decisions, recruiter-only access to a company, re-applying after a rejection. If you've been through it and have a protocol, that belongs here.

**New skills** — Claude Code slash commands in `skills/`. If you built a skill that isn't in the repo (e.g., `/research-company`, `/negotiate-offer`, `/follow-up`), add it.

**Bug fixes in the CLI** — `jsos/cli.py`, `jsos/scorer.py`, `jsos/tracker.py`. If something breaks or the output is wrong, fix it and include a clear description of what was wrong.

---

## How the Repo Is Structured

```
skills/         Claude Code slash commands
jsos/           The CLI package (Python)
  cli.py        All commands: scrape, score, list, track, stats, init
  scorer.py     Scoring logic — reads config.yaml
  tracker.py    Outreach tracker read/write
  templates/    Files copied by jsos init into a new workspace
1-Profile/      Master context template
2-Resume/       Resume prompt and LaTeX template
3-Outreach/     Outreach system
4-Company-Research/   Scrapers and scoring scripts
5-Interview-Prep/     Interview prep system
6-Strategy/     Playbook and daily ops
7-Situations/   Diagnostic and objection guides
```

The `jsos/templates/` folder mirrors the top-level module folders. When someone runs `jsos init`, everything in `templates/` gets copied into their workspace. If you add a new template file, add it there too.

---

## Before You Open a PR

- Test your change with a real `jsos init` workspace if it touches the CLI or templates
- If you're improving a prompt, note what the old output was and what the new one produced — even a rough before/after
- Keep PRs focused. One thing per PR is easier to review than five things bundled together
- Open an issue first for large changes so there's alignment before you build

---

## Opening Issues

Issues are the right place for:
- Scrapers that break (startups.gallery changes structure periodically)
- CLI commands that error unexpectedly
- Situations or objection types not covered in `7-Situations/`
- Ideas for new modules or commands

Be specific about what you expected vs. what happened. Include the command you ran and the error output if relevant.
