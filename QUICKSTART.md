# Quickstart — From Zero to First Output

This guide gets you from a fresh install to your first tailored resume or outreach email in one sitting. It skips nothing important and adds nothing extra.

Time: about 45 minutes.

---

## Step 1 — Install (5 min)

```bash
git clone https://github.com/mukeshbasvekar/Job-Search-OS.git
cd Job-Search-OS
bash install.sh
```

Verify it worked:

```bash
jsos --version
```

If you see a version number, you're good.

---

## Step 2 — Create your workspace (2 min)

```bash
jsos init ~/my-job-search
cd ~/my-job-search
```

This scaffolds your folder structure. Everything from here on lives in `~/my-job-search`.

---

## Step 3 — Fill in your profile (20 min)

This is the most important step. Every AI prompt in this system reads from one file:

```
1-Profile/YOUR_context.md
```

Open it and fill in each section. Here's what to actually write:

**Metrics table** — list your real numbers. Think cost savings, users, revenue, team size, speed improvements. Do not round up. If you don't have an exact number, use a range or skip it.

**Professional Identity** — one sentence, lead with what you built or delivered. Not your degree. Not your title. Something like: "I led product at [Company] — [what it does] — shipped [N features] and drove [$X savings] before that, built [side project] to [N users]."

**Experience bullet bank** — for each role, write labeled bullets. The labels matter — they're how the AI selects which bullets fit a given JD. Good labels: `Cost Savings`, `Launch Speed`, `Customer Adoption`, `Team Leadership`. Bad labels: `Bullet 1`, `General`.

**Cold Email Identity** — one paragraph you'd open every cold email with. Write it now, before you need it. Formula: what you built + what it achieved + why it's relevant to the type of company you're targeting.

**Behavioral stories (quick reference)** — add at least 3 one-liners here. Format: Company | What happened in one line | What themes it covers (e.g., conflict, failure, ownership).

Also fill in `1-Profile/YOUR_resume_data_compact.md` — it's a shorter version of the same info, used for faster AI lookups.

---

## Step 4 — Configure your scoring (5 min)

Open `config.yaml`. Three things to set:

**Your name** — top of the file.

**Industry weights** — set the industries you know to 2 or 3. Set industries you want to avoid to 0. If you have no opinion, leave at 1.

**Keywords** — replace the default list with terms that match your background. If you've worked on enterprise SaaS, keep `enterprise`, `saas`, `b2b`. If you're targeting AI roles, keep `agent`, `llm`, `generative`. Delete the ones that don't fit.

**Company size** — set which team sizes you want. If you want Founding PM roles, set `1-10` to 3. If you prefer established startups, set `51-200` higher.

---

## Step 5 — Pull and score companies (5 min)

```bash
jsos scrape --stage series-a
jsos score  --stage series-a
jsos list
```

You'll see a ranked list of companies scored against your config. If your list is too short, lower the threshold in `config.yaml` or run a different stage:

```bash
jsos scrape --stage seed
jsos scrape --stage yc
```

---

## Step 6 — Pick one company and do something with it

You're set up. Now use the system.

### Option A — Generate a tailored resume

1. Pick a company from `jsos list` and find a JD for a role there
2. Open Claude (claude.ai) or GPT-4o
3. Paste these three things in one message:
   - Contents of `2-Resume/prompts/prompt_compact.md`
   - Contents of `1-Profile/YOUR_context.md`
   - The job description
4. The AI outputs a `.tex` file rebuilt for that role
5. Save it to `2-Resume/output/` and compile:

```bash
brew install tectonic   # if you don't have it
tectonic 2-Resume/output/your_resume.tex
```

### Option B — Write a cold outreach email

1. Pick a company from `jsos list` and find the founder or hiring manager's email (Apollo.io free tier works)
2. Open Claude or GPT-4o
3. Paste these three things:
   - Contents of `3-Outreach/email_prompt.md`
   - Contents of `1-Profile/YOUR_context.md`
   - The company's JD or a short description of what they do and the role
4. The AI generates a personalized 3-bullet email
5. Log it when you send:

```bash
jsos track --company "Acme AI" --status sent
```

---

## Step 7 — Activate Claude Code skills (optional, 2 min)

If you're using Claude Code, you can skip the copy-paste step entirely. Skills let you run `/generate-resume` or `/cold-email` directly from the terminal — Claude reads your profile automatically.

```bash
mkdir -p .claude/commands
cp skills/*.md .claude/commands/
```

Then inside Claude Code in your workspace, just run:

```
/generate-resume
/cold-email
/interview-prep
```

---

## What Day Two Looks Like

- Run `jsos list` and pick your top 10 targets for the week
- Send 5–10 outreach emails per day, log each one with `jsos track`
- Check your pipeline with `jsos stats`
- When you get a reply, update the status: `jsos track --company "Acme" --status replied`
- When you land an interview, run `/interview-prep` or use `5-Interview-Prep/prompts/interview_prep_prompt.md`

If something isn't working — reply rate low, no interviews booking, pipeline stalling — open `7-Situations/WHEN_STUCK.md`. It has a three-question diagnostic that tells you exactly where the break is.

---

## Files to Know

| File | What It's For |
|---|---|
| `1-Profile/YOUR_context.md` | Master context — everything reads from here |
| `config.yaml` | Scoring weights and targeting preferences |
| `2-Resume/prompts/prompt_compact.md` | Resume generation prompt |
| `3-Outreach/email_prompt.md` | Cold email generation prompt |
| `5-Interview-Prep/prompts/interview_prep_prompt.md` | 8-phase interview prep prompt |
| `7-Situations/WHEN_STUCK.md` | When the search stalls |
| `skills/` | Claude Code slash commands |
