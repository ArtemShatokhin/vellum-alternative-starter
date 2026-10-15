# Kortix vs Vellum

Kortix is the open-source AI Operating System a team runs agents on. Vellum is a personal AI assistant for one person. Both are open source and both can run on your own hardware, and they answer different ownership questions. This page sets out what each one is, where each runs, what you own, and how work is reviewed. Every Vellum cell comes from Vellum's own pages, linked inline and checked October 2026.

## What each one is

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. The [Kortix docs](https://kortix.com/docs) describe a project as a git repo with `kortix.yaml` at its root, where agents, skills, memory, tools, triggers and connectors are files. A session runs one agent in its own sandbox on its own branch, and the agent opens a change request when the work is ready.

Vellum is a personal AI assistant. Its [homepage](https://www.vellum.ai/) calls it a personal, secure AI assistant that you fully own and customize to your needs, that runs locally on your machine or in the cloud, is available around the clock from any device, and remembers you over time. Vellum frames the assistant as one you name and shape, and its [docs](https://www.vellum.ai/docs) describe an assistant that lives in Vellum Cloud, has its own identity, and does things in the world.

The difference is scope. Vellum keeps one person's assistant, its memory, and its credentials. Kortix keeps a company's configuration, which a whole team reads, diffs and reviews.

## Where each one runs

Kortix runs on Kortix Cloud, in your VPC, or on your own on-prem network, and self-host is free. The [Kortix self-hosting guide](https://kortix.com/docs/host) describes a self-hosted instance as one Docker Compose stack the `kortix self-host` CLI installs, configures and updates. Sessions are the one part that runs elsewhere: they start on a cloud sandbox provider (Daytona, Platinum or E2B), and the instance must be reachable so those sandboxes can call back.

Vellum runs its assistant locally on your machine or in Vellum Cloud, according to its [homepage](https://www.vellum.ai/). Its [pricing page](https://www.vellum.ai/pricing) says you can deploy the assistant on your own hardware, a VPS, or a private cloud. The homepage lists Mac as native, with iOS, Android, web, voice, email, Telegram, Slack and terminal as ways to reach the same assistant.

Both can sit on machines you control or rent. Kortix self-hosting runs the same images the managed cloud runs, so the two deployments stay in step.

## What you own

Kortix keeps the company's configuration in a git repo you own. Agents are markdown files, memory is files that accumulate, and `kortix.yaml` declares the connectors and triggers, so every part of the setup is versioned, diffable and shared by the team. [Kortix on GitHub](https://github.com/kortix-ai/suna) is the same open-source code you can read, fork and audit.

Vellum keeps a different set of things on your side. Its [homepage](https://www.vellum.ai/) says the assistant's memory and credentials vault live locally on your machine or in the cloud, with none of your data accessible by Vellum unless you have opted in. Its [docs](https://www.vellum.ai/docs) say the assistant can access your files, your tools and your services, which is what makes it useful and what makes it worth understanding.

## How work is reviewed

Kortix puts a review between an agent and the place work lands. Session work reaches main through a change request, and merge is default-deny for agents, so a person reviews the diff and merges it. Approval gates are off until you set them, and connector calls use Allow, Ask or Block, down to the arguments of each call. The [Kortix docs](https://kortix.com/docs) put the merge in the hands of a person with the `project.gitops.merge` permission.

Vellum handles review at the task level. Its [homepage](https://www.vellum.ai/) says the assistant asks for permission on tasks with security risks until you mark them as trusted, and that high-stakes actions such as sending email to new contacts, modifying important files, or spending credits require explicit approval until you mark them trusted. The control is a permission prompt on one person's assistant, where Kortix's control is a diff a team reviews.

## The two, side by side

| | Kortix | Vellum |
| --- | --- | --- |
| What it is | The open-source AI Operating System a team runs agents on. | A personal AI assistant for one person. |
| Where it runs | Kortix Cloud, your VPC, or your own on-prem network. | Locally on a machine, or in Vellum Cloud. |
| What you own | Agents, skills, memory and connectors in one git repo. | Memory and a credentials vault on your machine or your cloud. |
| How work is reviewed | A change request a person merges. | Permission prompts until you mark a task trusted. |
| Open source | Yes. Read it, fork it, audit it. | Its own site says it is open source. |

## When Vellum is the right pick

Vellum fits when the job belongs to one person. It learns your preferences, holds memory about you, runs on a Mac or in Vellum Cloud, and reaches you across the devices you already use. The payment shape follows the same model: its [pricing page](https://www.vellum.ai/pricing) builds cloud tiers around one assistant's capacity, from $30 per month at the first tier.

## When Kortix is the right pick

Kortix fits when the job belongs to a team. The configuration is one git repo the company owns, so the agents, skills, memory and connectors that run the business are versioned and reviewable instead of held on one device. Sessions run on real cloud computers, and thousands of agents run in parallel on one config, each on its own cloud computer. Every change reaches main through a change request a person approves. [Kortix pricing](https://kortix.com/pricing) starts free and self-host is free: Free is $0 with 200 credits per month and 1 project. The team plan is $40 per seat per month with 2,500 credits per month per seat, pooled.
