---
name: vellum-workflow-inventory
description: List the workflows a person runs in Vellum and map each one to a Kortix agent or skill file.
---

# Vellum workflow inventory

Use this skill when you move a workflow off Vellum onto Kortix, the open-source AI Operating System. It lists the jobs a personal assistant does there and gives each one a home in a Kortix project, so a team can run the same work from one repo.

## How to fill the inventory

1. List every recurring job you run in Vellum, including the ones you start by asking.
2. For each job, write its trigger: a time, an event, or a person asking.
3. Write what it reads and what it produces, so a reviewer can tell whether the new agent did the job.
4. Give it a home in the repo: an `agents/<name>.md` for the work, a `skills/<name>/SKILL.md` for how your company does it, and an `agents.<name>` block in `kortix.yaml` for what it may reach.
5. Delete the row once the workflow runs on Kortix and the change request has merged.

## The map

| Vellum workflow | Trigger | Kortix home |
| --- | --- | --- |
| Morning briefing | cron | `agents/morning-briefing.md` + a cron trigger in `kortix.yaml` |
| Inbox triage and reply drafts | cron | `agents/inbox-triage.md` + `skills/inbox-tone/SKILL.md` |
| Calendar scheduling | webhook | `agents/calendar-scheduler.md` |
| Deep research and a summary | person asks | `agents/research-brief.md` + `skills/source-standards/SKILL.md` |
| Slides and documents | person asks | `agents/deck-builder.md` + `skills/deck-format/SKILL.md` |
| Code changes | person asks | `agents/patch-writer.md` + a change request for review |
| Website monitoring | cron | `agents/site-watch.md` |
| Slack messages and replies | webhook | `agents/slack-replier.md` |
| Ticket updates | webhook | `agents/ticket-updater.md` |
| Social posting | cron | `agents/social-drafter.md` + a human send gate |
| Blog drafting | cron | `agents/content-drafter.md` + `skills/house-style/SKILL.md` |
| Remembered preferences | person asks | `memory/` as plain files, read by every agent |

## What changes when the job moves

A personal assistant runs for one account and keeps its state on that one machine. A Kortix project runs for a team: the agent files, the skills, the memory and the connectors are all files in one git repo, so the whole team reads the same instructions and reviews the same change. Each session runs one agent in its own sandbox on its own branch, and a person merges what the agent proposes.

## What each row needs before it runs

- The connector for every outside app the workflow calls, declared in `kortix.yaml`.
- The secret names it needs, listed under `env`, with values set outside the repo.
- The tools it may call, set to Allow, Ask or Block. A call that reaches outside the repo should start at Ask.
- A first run you watch, so you can confirm the output before the trigger runs it unattended.
