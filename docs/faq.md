# FAQ: moving off Vellum

Seven questions developers ask when they move a workflow from Vellum to Kortix, the open-source AI Operating System, each answered from the two vendors' own pages.

## Is Vellum open source too?

Yes. Vellum's own [homepage](https://www.vellum.ai/) says it is open source and that you can inspect the code yourself. Kortix is open source too, and the code is at [Kortix on GitHub](https://github.com/kortix-ai/suna), where you can read it, fork it and audit it. The difference is scope: Vellum is a personal assistant for one person, and Kortix is the open-source AI Operating System a team runs on.

## Can I self-host a Vellum alternative?

Yes. Kortix runs on Kortix Cloud, in your VPC, or on your own on-prem network, and self-host is free. The [Kortix self-hosting guide](https://kortix.com/docs/host) installs the full platform as one Docker Compose stack on a server you control. Vellum's [pricing page](https://www.vellum.ai/pricing) says you can deploy its assistant on your own hardware, a VPS, or a private cloud.

## What does it cost?

Kortix is free to start, and self-host is free. On [Kortix pricing](https://kortix.com/pricing): Free is $0 with 200 credits per month and 1 project. The team plan is $40 per seat per month with 2,500 credits per month per seat, pooled. Vellum is free to download, and its [pricing page](https://www.vellum.ai/pricing) starts cloud plans at $30 per month.

## How do I migrate one Vellum workflow?

Use the agent in this repo, `agents/migrate-one-vellum-workflow.md`. It names one workflow, writes the behavior file under `agents/`, declares the grants in `kortix.yaml`, and adds the trigger that runs it. The full step list is in the agent file, and [`skills/vellum-workflow-inventory.md`](../skills/vellum-workflow-inventory.md) maps each Vellum job to a Kortix agent or skill file.

## What happens to the work an agent produces?

The agent works on its session branch and opens a change request. Session work reaches main through a change request, and merge is default-deny for agents, so a person reviews the diff and merges it. Calls that reach outside the repo sit behind approval gates you set, which are off until you set them.

## Where does my data live?

In Kortix, connector credentials are brokered server-side and never enter the machine, and secrets are encrypted at rest with a key per project. Your configuration lives in one git repo you own. Vellum's [homepage](https://www.vellum.ai/) says its memory and credentials vault live locally on your machine or in the cloud, with none of your data accessible by Vellum unless you have opted in.

## Can I keep using my own model keys?

Yes. Kortix takes any model provider with your own keys, or the ChatGPT plan you already pay for, or sign in with your OpenCode Console account for OpenCode Zen and Go. Vellum's [homepage](https://www.vellum.ai/) says you can switch between models including OpenAI, Anthropic, Gemini, or open weights via Ollama at any time.
