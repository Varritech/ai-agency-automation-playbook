---
name: weekly-client-report
description: Builds the weekly performance report for one agency client from ad platform data, compares it to the prior week, writes a plain-English summary, and saves it as a draft for human approval. Use when asked for a weekly report, a client update, "how did we do this week", or when the Monday report job runs. Never sends anything to the client.
---

# Weekly client report

Produces one report per client per week. It drafts. A person approves and sends.

## You need

- Access to the client's ad platform data through the user's own account or API token (read-only is enough).
- A database with the tables `metrics`, `deliverables` and `runs` (columns in the repo README).
- The client's profile: name, goal (leads, sales or bookings), the one number they care about most (the "north star"), and the contact who approves.

If any of these is missing, stop and ask. Do not guess.

## Inputs

| Input | Example | Default |
|---|---|---|
| client | the client's name or id | required |
| week_start | Monday of the week to report | last full week (Monday to Sunday) |

## Steps

1. **Start a run.** Insert a row in `runs` with skill `weekly-client-report`, the client, the start time and status `running`. Note the time you started for the `minutes_saved` calculation later.
2. **Pull this week's numbers.** From the ad platform, for `week_start` to `week_start + 6 days`, get per campaign: spend, impressions, clicks, leads (or purchases), cost per result.
3. **Pull last week's numbers.** Read them from `metrics` first. If missing, pull from the platform and store them.
4. **Store this week.** Insert this week's totals into `metrics` (client, week_start, metric, value) so next week can compare. Overwrite if the same week already exists.
5. **Calculate changes.** For each metric: this week, last week, change in percent. Mark any change over 20 percent as notable.
6. **Find the story.** Answer three questions from the data only:
   - What got better, and which campaign or ad caused it?
   - What got worse, and which campaign or ad caused it?
   - What is the one action we recommend next week?
7. **Write the report** using the format below. Use plain words, short sentences, no jargon, no hype.
8. **Check the report** against the checklist below. Fix anything that fails.
9. **Save the draft.** Insert into `deliverables`: type `weekly_report`, the report text, status `pending_approval`.
10. **Ask for approval.** Tell the account manager the draft is ready, where it is, and the three numbers to double-check (the north star, spend, and the biggest change).
11. **Close the run.** Set `runs.status` to `awaiting_approval`, record the finish time, and record `minutes_saved` (the usual manual time minus the minutes this run took).

## Report format

```
Subject: [Client] weekly update: [one-line headline with the north star number]

Hi [contact first name],

Here is how the week of [dates] went.

Headline
[One sentence. The north star number and how it moved.]

The numbers
| Metric | This week | Last week | Change |
|---|---|---|---|
| Spend | | | |
| [Results: leads / sales / bookings] | | | |
| Cost per result | | | |
| Clicks | | | |

What worked
- [1 to 2 bullets, each names the campaign or ad and the number]

What did not
- [1 to 2 bullets, same rule]

What we are doing next week
- [1 to 3 actions, each with a reason]

Anything you need from us or we need from you?
- [Only if true. Otherwise leave out.]

[Account manager name]
```

## Checklist before saving

- [ ] Every number in the text matches the table.
- [ ] Spend and results are from the same date range.
- [ ] Percent changes are calculated, not estimated.
- [ ] Nothing is claimed that the data does not show (no "because of the new creative" unless the ad-level data shows it).
- [ ] If results are low or spend is zero, the report says so plainly.
- [ ] No promises about future results.
- [ ] Under 250 words outside the table.
- [ ] No internal notes, tool names or other clients' data.

## Never

- Never email, message or share the report with the client. Draft only.
- Never change a campaign, budget or ad. This skill is read-only on the ad platform.
- Never invent a number. If data is missing, write "data not available" and tell the account manager.
- Never put credentials in the report or in this file. Read them from the environment.
- Never mix two clients' data in one run.

## Done when

- A `deliverables` row exists with status `pending_approval`.
- This week's totals are in `metrics`.
- The account manager has been told it is ready.
- The `runs` row is closed with `minutes_saved` filled in.

## Scheduling

Run every Monday early morning, one run per active client. Each run is independent: if one client fails, log the error in `runs.status` as `failed` and carry on with the others.

## Making it yours

- Change the report format to match what your clients already expect.
- Add or remove metrics to match each client's goal.
- Add a per-client rule block (for example: "always show cost per booked call first").
- After a month, read the approved reports against the drafts. Every edit a human made is a rule to add to this file.
