# SOP to skill template

Use this to turn a procedure your team already follows into a skill an AI can run in Claude Code, Claude, ChatGPT or Codex.

## Step 1: Write the SOP in plain words first

Answer these in a few lines each:

1. What task is this? (one sentence)
2. What triggers it? (a schedule, a request, an event)
3. What does a person need before starting? (access, files, data)
4. What are the steps, in order, as you do them today?
5. What does "done" look like?
6. What must never happen?
7. Who approves it, and when?

If you cannot answer 4 and 5 clearly, the task is not ready to automate. Fix the process first.

## Step 2: Fill in the skill file

Copy this into `<skill-name>/SKILL.md`. Use lowercase words with hyphens for the folder and `name`.

````markdown
---
name: <skill-name>
description: <What it does, in one sentence. Then "Use when" and 3 to 5 phrases a person would actually say.>
---

# <Task name>

<One line: what this produces and who checks it.>

## You need
- <Access, data or files. Say "the user's own account or token". Never paste a secret here.>

## Inputs
| Input | Example | Default |
|---|---|---|
| <name> | <example> | <value or required> |

## Steps
1. <Verb first. One action per step.>
2. <Name the exact source and the exact output.>
3. <Save results to the database, not to chat.>
4. <Run the checklist.>
5. <Save as draft with status pending_approval.>
6. <Tell the named person what to review.>

## Checklist before saving
- [ ] <A check someone could verify in 30 seconds.>
- [ ] <Another.>

## Never
- Never <send / publish / spend / delete> without approval.
- Never invent data. Write "data not available" instead.
- Never <your own hard rule>.

## Done when
- <A fact you can check, such as "a draft row exists with status pending_approval".>
````

## Step 3: Apply the 8 rules

| Rule | Check |
|---|---|
| One task per skill | If the title has "and" in it, split it |
| Description says when to use it | It has "Use when" and real phrases |
| Steps are numbered and start with a verb | Read them aloud |
| Inputs and outputs are named | No "the data" or "the file" |
| Approval gate exists | Anything client-facing or money-spending stops for a human |
| State goes to a database | No reliance on chat history |
| A "Never" list exists | At least three lines |
| "Done when" is checkable | A person can confirm it without asking the AI |

## Step 4: Test it three times

1. Run it on a real, low-risk case.
2. Read the output. Write down every edit you would make.
3. Turn each edit into a step, a checklist line or a "Never" line.
4. Run it on a second case. Repeat.
5. After three runs with few edits, schedule it.

## Step 5: Use it in your AI tool

| Tool | How |
|---|---|
| Claude Code | Put the folder in your skills directory |
| Claude | Paste into a Project or upload as a skill |
| ChatGPT | Paste into a Custom GPT or Project instructions |
| Codex | Save in the repo and reference it from `AGENTS.md` |

## Step 6: Review monthly

Keep a short changelog at the bottom of each skill: date, what you changed, why. Skills improve when every correction gets written back into the file.
