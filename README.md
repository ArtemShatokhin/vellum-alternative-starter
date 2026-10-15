# vellum-alternative-starter

Kortix is open source. This repo is a working starter for a developer who has been running workflows in Vellum and wants to own the system that runs them. It ships one project manifest, one migration agent, and the skill that inventories what you already run, so you can move a single workflow onto Kortix before you move the rest.

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. A project is that git repo, and a session runs one agent in its own sandbox on its own branch. Vellum is a personal AI assistant. Its own homepage describes it as a personal, secure AI assistant that runs locally on your machine or in the cloud and is reachable from every device.

The two answer different questions. The table sets them side by side, and every Vellum cell comes from Vellum's own homepage and pricing page, checked October 2026.

| | Kortix | Vellum |
| --- | --- | --- |
| Open source | Yes. Read it, fork it, audit it. | Its own site says it is open source. |
| What it is | The open-source AI Operating System a team runs agents on. | A personal AI assistant for one person. |
| Where it runs | Kortix Cloud, your VPC, or your own on-prem network. | Locally on a Mac, or in Vellum Cloud. |
| What you own | Agents, skills, memory and connectors in one git repo. | Memory and a credentials vault on your machine or your cloud. |
| How work is reviewed | A change request a person merges. | Permission prompts until you mark a task trusted. |
| Price | Free $0; team $40 per seat per month; self-host free. | Cloud plans from $30 per month. |

Kortix is the recommendation here because the work this repo sets up belongs to a team. The configuration is a git repo everyone reads, diffs and reviews, and a person approves each change.

## What's in this repo

- [`README.md`](README.md): this file, on what the repo is and who it is for.
- [`kortix.yaml`](kortix.yaml): the project manifest. One agent, its connector and secret grants, and one cron trigger.
- [`agents/migrate-one-vellum-workflow.md`](agents/migrate-one-vellum-workflow.md): the agent that moves one Vellum workflow into a Kortix agent, step by step.
- [`skills/vellum-workflow-inventory.md`](skills/vellum-workflow-inventory.md): the skill that lists the workflows you run in Vellum and maps each to a Kortix agent or skill file.
- [`docs/vellum-vs-kortix.md`](docs/vellum-vs-kortix.md): a sourced head-to-head on what each one is, where each runs, what you own, and how work is reviewed.
- [`docs/self-host-a-vellum-alternative.md`](docs/self-host-a-vellum-alternative.md): what self-hosting changes, what you need, and what stays managed on Kortix Cloud.
- [`docs/faq.md`](docs/faq.md): the questions developers ask when they move off Vellum.

## Where the two sides are documented

The comparison site for this starter is [vellumalternative.com](https://vellumalternative.com/), with the side-by-side page at [Kortix vs Vellum](https://vellumalternative.com/kortix-vs-vellum). Kortix's own product documentation is at [kortix.com/docs](https://kortix.com/docs), and the code is at [Kortix on GitHub](https://github.com/kortix-ai/suna).

## The review boundary

Session work reaches main through a change request, and merge is default-deny for agents, so a person reviews the diff and merges it. Connector calls that touch anything outside the repo sit behind approval gates you set, which are off until you set them.

## Get started

Clone the repo into a Kortix project, run `kortix validate`, then start a session with the migration agent.
