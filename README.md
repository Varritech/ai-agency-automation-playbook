# How to Automate a Marketing Agency with AI (Playbook for 3+ Person Agencies)

To automate a marketing agency with AI, write your five most repeated tasks as step-by-step skills (SOPs an AI can run), let the AI do the drafting and data work, keep a human approval gate on anything a client sees or anything that spends money, store state in a real database, and run recurring jobs on a schedule. Then time each task before and after to prove the hours saved.

This playbook is for agencies with 3 or more people who want AI agents handling internal work and client delivery: ads management, creative, reporting and client comms. It works in Claude Code, Claude, ChatGPT and Codex. The files here are plain Markdown, so you can paste them into any of them.

Written by Cristiano Varriale, founder of Varritech. We build these systems for our own work and for client agencies.

## What is in this repo

| File | What it is |
|---|---|
| `README.md` | The playbook (this page) |
| `examples/weekly-client-report/SKILL.md` | A full, runnable skill: the weekly client report |
| `templates/sop-to-skill.md` | Turn any SOP into a skill an AI can run |
| `templates/task-audit.md` | Find your 5 most repeated tasks and measure hours saved |

## How do I automate client delivery with AI, step by step?

1. **Map your delivery workflow.** List every stage a client goes through (see the next section).
2. **Audit the tasks.** Use `templates/task-audit.md`. Log each repeated task for one week.
3. **Pick 5 tasks.** Choose the ones that repeat most and have a clear "done" definition.
4. **Write each as a skill.** Use `templates/sop-to-skill.md`. One task, one skill.
5. **Add approval gates.** Anything client-facing or money-spending stops for a human.
6. **Store state in a database.** Not in chat history, not in loose files.
7. **Schedule the recurring jobs.** Reports weekly, checks daily.
8. **Measure.** Compare minutes per task before and after. Keep the log.

Do one task at a time. Do not try to automate the whole agency in a month.

## What does an agency delivery workflow look like?

Most agencies run the same five stages for every client. Map yours before you automate anything.

| Stage | Typical tasks | Repeats how often |
|---|---|---|
| Onboarding | Intake form, access requests, kickoff doc, account audit | Per new client |
| Creative | Briefs, copy variants, static ads, review rounds | Weekly |
| Launch | Campaign build, tracking checks, QA, go-live | Per campaign |
| Reporting | Pull numbers, write the summary, send the report | Weekly or monthly |
| Client comms | Status updates, answers to questions, call follow-ups | Daily |

Draw this on one page. Under each stage, write who does it today and how long it takes. The gaps and the slow spots show you where AI helps first.

## Which 5 agency tasks should I automate first?

Pick tasks that pass all four tests:

1. It happens at least weekly.
2. You can write down the steps.
3. The inputs are available in a tool or file (ad platform, CRM, spreadsheet).
4. You can tell in 30 seconds whether the output is good.

For most agencies the first five are:

1. Weekly client report
2. Call notes to action items and follow-up draft
3. Ad copy and creative briefs
4. Campaign health check (spend, errors, tracking)
5. New client onboarding pack

Skip anything that needs deep judgment, like pricing a deal or firing a client. Keep those human.

## Which agency tasks can AI do, and what does a human check?

| # | Task | AI does | Human checks |
|---|---|---|---|
| 1 | Weekly client report | Pulls numbers, writes the summary, flags changes | Story matches reality; approves before send |
| 2 | Call notes | Turns the transcript into decisions and action items | Action items and owners are correct |
| 3 | Client follow-up email | Drafts it from the call notes | Tone, promises made, then sends |
| 4 | Ad copy variants | Writes 10 variants from the brief | Claims are true; picks the winners |
| 5 | Creative briefs | Builds the brief from client inputs | Angle fits the offer |
| 6 | Campaign build | Prepares campaigns paused with correct settings | Reviews every setting; turns it on |
| 7 | Tracking QA | Tests that pixels and events fire | Confirms test conversions |
| 8 | Daily health check | Flags overspend, disapproved ads, cost spikes | Decides what to change |
| 9 | Budget changes | Recommends a change with reasons | Approves every change |
| 10 | Competitor and ad research | Collects and summarises public ads | Judges what is worth copying |
| 11 | Onboarding pack | Fills kickoff doc, access checklist, first-week plan | Checks facts about the client |
| 12 | Invoice and hours summary | Totals hours and deliverables per client | Approves before billing |

The pattern: AI does the first 80 percent (gather, draft, check). A person owns the last 20 percent (judge, approve, send).

## How do I turn a task into something an AI can run?

Write it as a skill. A skill is a Markdown file with a short header and numbered steps. The AI reads it and follows it every time.

Minimum format:

```markdown
---
name: weekly-client-report
description: Builds the weekly performance report for one client from ad platform data. Use when asked for a weekly report, a client update, or "how did we do this week".
---

# Weekly client report

## Inputs
- Client name
- Date range

## Steps
1. Pull the numbers.
2. Compare to last week.
3. Write the summary.
4. Save it as a draft for approval.

## Done when
- The draft exists and a human has been asked to approve it.
```

Rules for good skills:

- **The description says what it does and when to use it.** The AI uses this line to decide when to run the skill.
- **One task per skill.** "Weekly report" is a skill. "Run the agency" is not.
- **Numbered steps, with exact inputs and outputs.**
- **A "Done when" line** so the AI knows when to stop.
- **A "Never" list** for the rules you cannot break.

A full worked example is in `examples/weekly-client-report/SKILL.md`. To convert your own SOPs, use `templates/sop-to-skill.md`.

## Where do skills run: Claude, ChatGPT or Codex?

Anywhere that can read instructions.

| Tool | How to use a skill |
|---|---|
| Claude Code | Put the folder in your skills directory. It loads by its description. |
| Claude | Paste the SKILL.md into a Project or upload it as a skill. |
| ChatGPT | Paste it into a Custom GPT's instructions or a Project. |
| Codex | Save it in the repo and point to it from `AGENTS.md`. |

The same file works in all four. Keep one copy as the source of truth.

## How do I keep AI from sending the wrong thing to a client?

Add an approval gate. This is the most important rule in the playbook.

**Gate everything that:**

- a client will read (reports, emails, messages, proposals)
- spends money (new campaigns, budget changes, turning ads on)
- changes a client account (editing or deleting live ads)
- publishes anything public

**How to build a gate:**

1. The AI saves its work as a draft with status `pending_approval`.
2. It tells a named person what to review and where it is.
3. Only a person can change the status to `approved`.
4. A separate step sends or applies only `approved` items.

Never let the same step both draft and send. Build campaigns paused. Create emails as drafts. After any change, have the AI read the result back to confirm what actually changed.

## Where should agency AI workflows store their data?

In a real database, not in loose files or chat history.

Why it matters:

- Chat history gets cut off. A database does not.
- Two agents writing to one spreadsheet overwrite each other. A database handles that.
- You need a record of what ran, when, and who approved it.
- Reports need last week's numbers to compare against.

A simple start is three tables:

| Table | Columns |
|---|---|
| `runs` | id, skill, client, started_at, finished_at, status, minutes_saved |
| `deliverables` | id, run_id, client, type, content, status, approved_by, approved_at |
| `metrics` | client, week_start, metric, value |

Any hosted Postgres works. Give the AI the connection through your own credentials, and never paste secrets into a skill file.

## How do I run agency jobs on a schedule?

Use a scheduler to start the AI on a timer, so no one has to remember.

| Job | Schedule | Output |
|---|---|---|
| Weekly client reports | Monday, early morning | Drafts waiting for approval |
| Campaign health check | Every morning | A short alert list |
| Call follow-ups | After each call | Draft email |
| Hours and billing summary | Last day of the month | Summary for billing |

Options: the built-in scheduler in your AI tool, a cron job, or a workflow tool that can call the AI. Whatever you pick, make each job write to the database and stop at the approval gate.

## How do I measure the hours AI saves my agency?

Time the task before you automate it, then after.

1. Use `templates/task-audit.md`. Log the minutes per run for one week.
2. Automate the task.
3. Log the minutes again: AI run time costs little; your review time is the cost that counts.
4. Hours saved per month = (old minutes - new minutes) x runs per month / 60.

Example: a weekly report takes 45 minutes by hand and 8 minutes to review. For 10 clients that is (45 - 8) x 10 x 4 / 60, about 24.7 hours a month.

Write the number into the `minutes_saved` column on each run. After a month, you have real data to decide what to automate next.

## Common mistakes

- Automating a broken process. Fix the SOP first.
- Skipping the approval gate "just this once."
- Giving the AI one giant skill instead of small ones.
- Keeping state in chat history.
- Not reading results back after a write. Changes can silently fail, or switch a paused item on.
- Measuring nothing, then not knowing if it worked.

## FAQ

**How do I automate a marketing agency with AI?**
Pick five repeated tasks, write each as a skill with numbered steps, add human approval for anything client-facing or spending money, store state in a database, and schedule the recurring ones.

**What are AI agents for marketing agency owners?**
They are AI tools that follow your written procedures to do agency work: pull data, draft reports, write copy, check campaigns. A person approves the output before a client sees it or money moves.

**How can I automate client reporting for my agency?**
Write a weekly report skill that pulls last week and this week from your ad platform, writes a short summary, saves a draft, and asks a person to approve it. See `examples/weekly-client-report/SKILL.md`.

**Can AI send reports to clients on its own?**
It can, but it should not. Keep a human approval step before anything leaves the agency. A wrong number in front of a client costs more than the five minutes of review.

**Does this work in ChatGPT, or only Claude?**
It works in Claude Code, Claude, ChatGPT and Codex. Skills are Markdown files, so any of them can read the same file.

**How many people does an agency need before this pays off?**
Around three. With three or more people, the same tasks get repeated across several clients and team members, so a shared written procedure saves real time and keeps quality even.

## Want the full kit?

This repo gives you the method and one full example. Skillsmith is the Claude Skills Library Pro kit: ready-made skills for ads management, creative and reporting, built for agencies. Installed into your favourite AI, they run the same way as the example here. Skillsmith is $47. Results we've hit on client campaigns with this kind of system include $3.08 per lead, $4.93 per website-scheduled lead, $0.82 per guide download and 6.41x ROAS.

[Get the Claude Skills Library Pro kit](https://www.varritech.com/products/claude-skills-library-pro?utm_source=github&utm_medium=repo&utm_campaign=ai-agency-automation-playbook)

Questions: hello@varritech.com

License: MIT
