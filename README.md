# Job Search OS

[![Stars](https://img.shields.io/github/stars/mukeshbasvekar/Job-Search-OS?style=flat-square)](https://github.com/mukeshbasvekar/Job-Search-OS/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg?style=flat-square)](https://www.python.org/)

**Everyone said to apply online. I cold emailed founders instead. Here's the system.**

Cold emails to founders convert to interviews at 5–8× the rate of job board applications. They skip the recruiter bottleneck and land directly with the person who can say yes. Most people never figure this out — and spend months refreshing their inbox waiting for ATS systems to respond.

This is the complete system for running a job search that actually converts: a CLI (`jsos`), AI prompts, company scrapers, LaTeX resume templates, a cold email engine, 8-phase interview prep, and a playbook for when things break. Built from a real search. Open-sourced so you don't have to build it from scratch.

---

## Who This Is For

- You've been applying online and getting silence — and you're ready to try a different channel
- You're targeting startups (Series A/B, Seed, YC) and want a direct line to founders
- You want your job search to run like a pipeline, not feel like a slot machine
- You're comfortable with a CLI and a text editor

This is not for passive applicants. It's for people who want to run an active, deliberate search.

---

## Quick Start

```bash
git clone https://github.com/mukeshbasvekar/Job-Search-OS.git
cd Job-Search-OS
bash install.sh
```

Then scaffold your workspace and run your first search:

```bash
jsos init ~/my-job-search
cd ~/my-job-search
jsos scrape --stage series-a
jsos score  --stage series-a
jsos list
```

That's it. You're now working a scored shortlist of Series A companies filtered to your background.

---

## What It Looks Like

```
$ jsos list --min-score 8

   #  Company                       Score  Priority      Role                  Size      Location
──────────────────────────────────────────────────────────────────────────────────────────────────────
   1  Acme AI                        10/12  Top Target    Product Manager       51-200    San Francisco
   2  BuildCo                         9/12  Top Target    Operations Lead       11-50     New York
   3  DataLayer                       8/12  High          Product Manager       51-200    Remote
   4  Foundry Inc                     8/12  High          Operations Lead       11-50     Austin

  Showing 4 companies  (score ≥ 8)
  →  Next:  jsos track --company "<name>" --status sent


$ jsos stats

  Outreach Pipeline — 47 companies tracked

  Status               Count  Bar
  ────────────────────────────────────────────────
  Sent                    31  ███████████████████████████████
  Replied                  9  █████████
  Meeting Booked           4  ████
  No Response              3  ███

  Reply rate  42%  (13/31)
  HM+ rate    31%  (4/13)
```

---

## Why Cold Email Beats Everything Else

| Channel | Interview Conversion Rate | Of those: Decision-Maker Rate |
|---|---|---|
| Cold Email → Founder/HM | **5–8%** | **~67%** reach decision-maker directly |
| Cold Application (ATS) | **~1%** | ~44% eventually reach decision-maker |
| Networking (warm intro) | varies | ~50% reach decision-maker |
| Job Boards | varies | ~29% reach decision-maker |

Cold email wins twice: it converts to interviews at a higher rate, and those interviews land directly with founders — skipping the recruiter layer entirely.

The scrapers in `4-Company-Research/` are the engine. They pull fresh companies from startups.gallery, score them against your background, and give you a prioritized shortlist to work through. The AI prompts handle the personalization at scale.

---

## What's Inside

| Module | What It Does |
|---|---|
| [1-Profile](1-Profile/) | Your master context file — fill it in once, every AI prompt reads from it |
| [2-Resume](2-Resume/) | AI prompt + LaTeX template → tailored resume rebuilt from scratch in under 10 minutes |
| [3-Outreach](3-Outreach/) | Cold email system — 3-email sequence, AI prompt, full strategy guide, tracker |
| [4-Company-Research](4-Company-Research/) | Python scrapers for startups.gallery (Series A/B/Seed/YC) + fit scoring engine |
| [5-Interview-Prep](5-Interview-Prep/) | 8-phase prep engine, 32 behavioral questions, 53-question company research template |
| [6-Strategy](6-Strategy/) | The full playbook — channel data, Rule of Three, daily ops ritual |
| [7-Situations](7-Situations/) | When you're stuck — diagnostic guides for every funnel breakdown |
| [PHILOSOPHY.md](PHILOSOPHY.md) | The 4Ps framework — the mental model behind every tool in here |

---

## The 4Ps — One Framework to Run the Whole Search

Every tool in this repo maps to one of four principles. When something breaks, one of these four is the culprit.

| Principle | What It Means | Where It Lives |
|---|---|---|
| **Protect** | Guard your mental state — rejection is structural, not personal | `6-Strategy/DAILY_OPS.md` |
| **Pipeline** | Keep enough in motion that one quiet process never stalls the search | `3-Outreach/` · `4-Company-Research/` |
| **Prove** | Specific proof beats generic claims — on paper and in the room | `2-Resume/` · `5-Interview-Prep/` |
| **Prep** | Segment → Target → Position. Know your material before you need it | `1-Profile/` · `6-Strategy/PLAYBOOK.md` |

Full reasoning: [PHILOSOPHY.md](PHILOSOPHY.md) — worth reading before you start.

---

## Setup (30 Minutes)

### Step 1 — Fill in your profile (20 min)
Open [1-Profile/YOUR_context.md](1-Profile/YOUR_context.md) and fill in every section. **This is the most important step.** Every AI prompt reads from this file.

Also fill in [1-Profile/YOUR_resume_data_compact.md](1-Profile/YOUR_resume_data_compact.md) — the compact version for faster AI lookups.

### Step 2 — Set up your resume template (5 min)
Open [2-Resume/template/resume_template.tex](2-Resume/template/resume_template.tex). Replace the header with your name, email, and LinkedIn.

Install [Tectonic](https://tectonic-typesetting.github.io/) (LaTeX compiler):
```bash
brew install tectonic   # macOS
```

### Step 3 — Set up your outreach tracker (2 min)
Copy [3-Outreach/tracker_template.csv](3-Outreach/tracker_template.csv) → rename to `outreach_tracker.csv`. Every company you contact gets logged here.

### Step 4 — Run your first scrape (3 min)
```bash
jsos scrape --stage series-a
jsos score  --stage series-a
jsos list
```

---

## How to Use Each Module

### Generate a Tailored Resume
1. Find a job description
2. Open Claude (or GPT-4o)
3. Paste: `2-Resume/prompts/prompt_compact.md` + `1-Profile/YOUR_context.md` + the JD
4. AI outputs a production-ready `.tex` file rebuilt for that specific role
5. Compile: `tectonic output/your_resume.tex`

### Write a Cold Email
1. Find a founder's email (Apollo.io free tier: 50 lookups/month)
2. Open Claude
3. Paste: `3-Outreach/email_prompt.md` + `1-Profile/YOUR_context.md` + the JD
4. AI generates a personalized 3-bullet cold email in their voice and context
5. Send Email 1 manually, automate follow-ups 2 and 3

### Source Companies to Email
1. Run `jsos scrape --stage series-a` (or seed, series-b, yc)
2. Run `jsos score --stage series-a` to rank by fit
3. Run `jsos list --min-score 8` to see your shortlist
4. Work it top-down

### Prep for an Interview
1. Open Claude
2. Paste: `5-Interview-Prep/prompts/interview_prep_prompt.md` + `1-Profile/YOUR_context.md` + your behavioral stories YAML + the JD
3. AI generates 8-phase prep: role decode → company research → narrative → behavioral → questions to ask → objections → logistics → thank-you email

### When You're Stuck
Answer three questions: Are emails going out? Are interviews coming in? Are calls being booked? [7-Situations/WHEN_STUCK.md](7-Situations/WHEN_STUCK.md) has a decision tree that maps your exact situation to a specific protocol.

Getting pushback in interviews? [7-Situations/OBJECTION_PLAYBOOK.md](7-Situations/OBJECTION_PLAYBOOK.md) covers every common objection — experience gaps, short tenures, career pivots, comp conversations — with the same structure every time: **acknowledge → reframe → redirect to evidence.**

---

## The Philosophy

The full version is in [PHILOSOPHY.md](PHILOSOPHY.md). The short version:

Most searches fail not from lack of effort but from effort pointed at the wrong thing. People spend 80% of their time on job boards — the lowest-leverage channel — and 20% on everything else. They send generic emails. They write generic resumes. They stop sending when one process looks promising, then have nothing when it goes quiet.

This system inverts that:

- **Cold email to founders** is the engine. The scrapers keep it fed. The AI keeps it personalized.
- **Every resume is rebuilt for the JD** in under 10 minutes with AI — not tweaked, rebuilt.
- **Interview prep predicts questions** based on the JD, company stage, and role type before you're in the room.
- **The pipeline keeps running** even while interviews are active — so a quiet process never stalls the whole search.
- **When something breaks**, `7-Situations/` tells you exactly where and what to fix.

---

## What You'll Need

| Tool | Why | Cost |
|---|---|---|
| Claude or GPT-4o | AI prompts for resume, email, interview prep | Free tier works |
| [Tectonic](https://tectonic-typesetting.github.io/) | LaTeX compiler for resumes | Free |
| Python 3.10+ | CLI and scrapers | Free |
| Apollo.io | Founder email lookup | Free tier: 50/month |
| Google Sheets or Excel | Outreach tracker | Free |

---

## Folder Structure

```
Job-Search-OS/
├── PHILOSOPHY.md                           ← Read this first — the 4Ps framework
├── README.md                               ← You are here
├── config.yaml                             ← Scoring weights + targeting preferences
├── install.sh                              ← One-command install
├── 1-Profile/
│   ├── YOUR_context.md                     ← Fill this in first (master AI context)
│   └── YOUR_resume_data_compact.md         ← Compact AI lookup version
├── 2-Resume/
│   ├── template/resume_template.tex        ← LaTeX template (replace header)
│   └── prompts/prompt_compact.md           ← AI resume generation prompt
├── 3-Outreach/
│   ├── email_prompt.md                     ← AI cold email prompt
│   ├── cold_email_sequence.md              ← 3-email sequence
│   └── OUTREACH_STRATEGY.md                ← Full strategy guide
├── 4-Company-Research/
│   ├── scrape_series_a/b/seed/yc.py        ← Startup scrapers
│   └── enrich_and_score.py                 ← Fit scoring engine
├── 5-Interview-Prep/
│   ├── prompts/interview_prep_prompt.md    ← 8-phase prep generator
│   ├── stories/behavioral_questions.md     ← 32 master behavioral questions
│   └── prep/research_template.md          ← 53-question company research template
├── 6-Strategy/
│   ├── PLAYBOOK.md                         ← Rule of Three + channel data
│   └── DAILY_OPS.md                        ← Morning ritual + daily workflow
└── 7-Situations/
    ├── WHEN_STUCK.md                       ← Funnel diagnostic + situation protocols
    └── OBJECTION_PLAYBOOK.md               ← Interview objection handling
```

---

If this saves you time or helps you land something — drop a star. It helps other job seekers find it.

Built by [Mukesh Basvekar](https://www.linkedin.com/in/mukeshbasvekar/)
