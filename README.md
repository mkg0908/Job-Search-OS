# Job Search OS

[![Stars](https://img.shields.io/github/stars/mukeshbasvekar/Job-Search-OS?style=flat-square)](https://github.com/mukeshbasvekar/Job-Search-OS/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg?style=flat-square)](https://www.python.org/)

**An AI-native operating system for your job search.**

One profile file. One CLI. Every tool you need — company discovery, resume generation, outreach, interview prep, pipeline tracking — all wired together and powered by AI at every step.

This is not a collection of templates. It's a system with a runtime: fill in your profile once, and every tool in here draws from it. Scrape companies that match your background. Generate a tailored resume for any JD in under 10 minutes. Draft outreach. Prep for interviews. Track your pipeline. All from the terminal. All AI-native.

Built from a real job search. Open-sourced so you don't have to build it from scratch.

---

## What You Can Do With It

Pick what you need. Use one module or all of them — they all draw from the same profile, so nothing is siloed.

| Task | How |
|---|---|
| Find companies that fit your background | `jsos scrape` + `jsos score` + `jsos list` |
| Generate a tailored resume for any JD | AI prompt + your profile → production `.tex` in 10 min |
| Write a personalized outreach email | AI prompt + your profile + JD → 3-bullet cold email |
| Prep for an interview end-to-end | AI prompt → 8-phase prep doc, role-specific |
| Track your pipeline | `jsos track` + `jsos stats` |
| Diagnose why your search is stalling | `7-Situations/WHEN_STUCK.md` — 3-question diagnostic |
| Handle interview objections | `7-Situations/OBJECTION_PLAYBOOK.md` |

---

## Quick Start

```bash
git clone https://github.com/mukeshbasvekar/Job-Search-OS.git
cd Job-Search-OS
bash install.sh
```

Scaffold your workspace:

```bash
jsos init ~/my-job-search
cd ~/my-job-search
```

Fill in `1-Profile/YOUR_context.md` — this is the one file everything else reads from. Then run whatever you need.

**New here?** Follow [QUICKSTART.md](QUICKSTART.md) — it gets you from install to your first resume or email in one sitting.

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

## Who This Is For

- You want your job search to run like a system, not feel like guesswork
- You're targeting startups and want structured company discovery
- You're already using AI for work — and want it baked into your search, not bolted on
- You prefer a CLI and a text editor over drag-and-drop dashboards
- You've tried scattered tools (Notion templates, random prompts, spreadsheets) and want something coherent

---

## What's Inside

| Module | What It Does |
|---|---|
| [1-Profile](1-Profile/) | Your single source of truth — fill it in once, every tool draws from it |
| [2-Resume](2-Resume/) | AI prompt + LaTeX template → tailored resume rebuilt from scratch per JD |
| [3-Outreach](3-Outreach/) | Outreach system — AI email prompt, 3-message sequence, strategy guide, tracker |
| [4-Company-Research](4-Company-Research/) | Python scrapers for startups.gallery (Series A/B/Seed/YC) + fit scoring engine |
| [5-Interview-Prep](5-Interview-Prep/) | 8-phase AI prep engine, 32 behavioral questions, 53-question company research |
| [6-Strategy](6-Strategy/) | Full playbook — channel data, daily ops ritual, the Rule of Three |
| [7-Situations](7-Situations/) | Situational guides — when you're stuck at any stage of the funnel |
| [skills/](skills/) | Claude Code slash commands — `/generate-resume`, `/cold-email`, `/interview-prep`, and more |
| [PHILOSOPHY.md](PHILOSOPHY.md) | The 4Ps framework — the mental model that holds the whole system together |

---

## How the AI Works

There's no magic API. The AI layer is prompt-based — you paste context into Claude (or GPT-4o) and get a result. What makes it work is that `1-Profile/YOUR_context.md` is the shared context across every prompt. You fill it in once.

**Resume:** Paste `prompt_compact.md` + your profile + the JD → AI rebuilds the resume for that role from scratch, not a generic tweak.

**Outreach:** Paste `email_prompt.md` + your profile + the company's JD → AI writes a personalized email specific to their stage, team, and problem.

**Interview prep:** Paste `interview_prep_prompt.md` + your profile + your story bank + the JD → AI generates an 8-phase prep doc: role decode, company research, narrative, behavioral prep, questions to ask, objection handling, logistics, thank-you.

The prompts are engineered, not generic. They've been refined through a real search.

---

## The 4Ps — How the System Thinks

Every module maps to one of four principles. When the search isn't moving, one of these four is broken.

| Principle | What It Means | Where It Lives |
|---|---|---|
| **Protect** | Guard your mental state — rejection is structural, not personal | `6-Strategy/DAILY_OPS.md` |
| **Pipeline** | Keep enough in motion that one quiet process never stalls the search | `3-Outreach/` · `4-Company-Research/` |
| **Prove** | Specific proof beats generic claims — on paper and in the room | `2-Resume/` · `5-Interview-Prep/` |
| **Prep** | Segment → Target → Position. Know your material before you need it | `1-Profile/` · `6-Strategy/PLAYBOOK.md` |

Full reasoning: [PHILOSOPHY.md](PHILOSOPHY.md)

---

## Channel Data

The system is channel-agnostic. Use cold outreach, warm intros, job boards, or all three — the tools support any approach. Here's what the data shows about how different channels perform, so you can weight your effort accordingly:

| Channel | Interview Conversion | Decision-Maker Rate |
|---|---|---|
| Direct outreach to founder/HM | **5–8%** | ~67% reach decision-maker |
| Networking / warm intro | varies | ~50% reach decision-maker |
| Cold application (ATS) | **~1%** | ~44% reach decision-maker |
| Job boards (inbound) | varies | ~29% reach decision-maker |

The playbook in `6-Strategy/PLAYBOOK.md` covers the Rule of Three — how to run multiple channels in parallel so no single one becomes a bottleneck.

---

## Setup (30 Minutes)

### Step 1 — Fill in your profile (20 min)
Open [1-Profile/YOUR_context.md](1-Profile/YOUR_context.md). Fill in every section. **This is the most important step** — it's the source of truth for every AI prompt.

Also fill in [1-Profile/YOUR_resume_data_compact.md](1-Profile/YOUR_resume_data_compact.md) for faster AI lookups.

### Step 2 — Set up your resume template (5 min)
Open [2-Resume/template/resume_template.tex](2-Resume/template/resume_template.tex). Replace the header with your name, email, and LinkedIn.

Install [Tectonic](https://tectonic-typesetting.github.io/) (LaTeX compiler):
```bash
brew install tectonic   # macOS
```

### Step 3 — Set up your tracker (2 min)
Copy [3-Outreach/tracker_template.csv](3-Outreach/tracker_template.csv) → rename to `outreach_tracker.csv`.

### Step 4 — Pull your first company list (3 min)
```bash
jsos scrape --stage series-a
jsos score  --stage series-a
jsos list
```

---

## How to Use Each Module

### Generate a Tailored Resume
1. Find a job description
2. Open Claude or GPT-4o
3. Paste: `2-Resume/prompts/prompt_compact.md` + `1-Profile/YOUR_context.md` + the JD
4. AI outputs a `.tex` file rebuilt specifically for that role
5. Compile: `tectonic output/your_resume.tex`

### Write Outreach
1. Find the right person to contact (role-dependent: founder, HM, or recruiter)
2. Open Claude
3. Paste: `3-Outreach/email_prompt.md` + `1-Profile/YOUR_context.md` + the JD or company description
4. AI generates a personalized 3-bullet message
5. Send manually, automate follow-ups 2 and 3

### Prep for an Interview
1. Open Claude
2. Paste: `5-Interview-Prep/prompts/interview_prep_prompt.md` + `1-Profile/YOUR_context.md` + your behavioral stories YAML + the JD
3. AI generates your full 8-phase prep doc

### When You're Stuck
[7-Situations/WHEN_STUCK.md](7-Situations/WHEN_STUCK.md) runs a 3-question diagnostic: Are emails going out? Are interviews coming in? Are calls converting? Each answer maps to a specific situation and protocol.

[7-Situations/OBJECTION_PLAYBOOK.md](7-Situations/OBJECTION_PLAYBOOK.md) covers every common interview objection — experience gaps, short tenures, career pivots, comp conversations — with the same structure: **acknowledge → reframe → redirect to evidence.**

---

## What You'll Need

| Tool | Purpose | Cost |
|---|---|---|
| Claude or GPT-4o | Powers every AI prompt | Free tier works |
| [Tectonic](https://tectonic-typesetting.github.io/) | Compiles LaTeX resumes | Free |
| Python 3.10+ | CLI and scrapers | Free |
| Apollo.io | Contact lookup (optional) | Free tier: 50/month |
| Google Sheets or Excel | Outreach tracker | Free |

---

## Folder Structure

```
Job-Search-OS/
├── PHILOSOPHY.md                           ← Read this first — the 4Ps framework
├── QUICKSTART.md                           ← Zero to first output in one sitting
├── CONTRIBUTING.md                         ← How to contribute
├── LICENSE                                 ← MIT
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
│   ├── email_prompt.md                     ← AI outreach prompt
│   ├── cold_email_sequence.md              ← 3-message sequence
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
