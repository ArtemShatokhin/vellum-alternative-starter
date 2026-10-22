# Self-host a Vellum alternative

Vellum lets you run its assistant on your own machine, a VPS, or a private cloud, and its own [pricing page](https://www.vellum.ai/pricing) says so. If the thing you want to self-host is a system a whole team runs on, Kortix is the open-source option: the [Kortix self-hosting guide](https://kortix.com/docs/host) covers running the full platform on a server you control. This page walks through what self-hosting changes, what you need, and what stays managed when you use Kortix Cloud instead.

## What self-hosting changes

A self-hosted Kortix instance is the full platform on a server you control: one Docker Compose stack that the `kortix self-host` CLI installs, configures and updates. Your database, your files, your repos and your policies sit on disk you own, and the same images the managed cloud runs are the ones your stack pulls. It is open source, so what you are running is code you can read.

Sessions are the part that still runs elsewhere. Every session starts on a cloud sandbox provider rather than on the server itself, so the instance has to be reachable from the internet for the sandbox to call back. The three reachability modes the docs describe make that trade explicit: `domain` is the production setup with public URLs and sessions enabled, `tunnel` publishes only the API for evaluation, and the default loopback setup runs no sessions at all.

## What you need

- A Linux server with a public IP. The bootstrap installs Docker Engine and the Compose plugin when they are missing.
- DNS pointed at the server before the first start: A or AAAA records for `<domain>` and `api.<domain>`, plus a wildcard `*.p.<domain>` for sandbox previews.
- Ports 80 and 443 open inbound, so Caddy can get the TLS certificate.
- A sandbox provider key for Platinum or the legacy Daytona fallback. Without one, sessions do not start.
- A model provider key, added in the web app after the first sign-in.
- Optionally, a wildcard `*.<apps base domain>` such as `*.apps.<domain>` if you want to host Apps.

## The steps

The [Kortix self-hosting guide](https://kortix.com/docs/host) documents the install in this order.

1. Point DNS at the server, with the records above, and open ports 80 and 443.
2. Install the CLI and initialize the stack on the server. The bootstrap path installs Docker and the Compose plugin first; the by-hand path assumes both are present:
   `curl -fsSL https://kortix.com/install | bash`
   `kortix self-host init --domain kortix.example.com --admin-email you@example.com`
3. Answer the setup questions with `kortix self-host configure`: the reachability mode, the admin email, the sandbox provider key, and the preview domain.
4. Apply the answers with `kortix self-host start`, which runs the Compose stack and the database migration.
5. Sign up as the admin at your domain, connect GitHub at `/admin/git`, create the team account and a project, then add a model key.
6. Run `kortix self-host doctor` and fix every failing check before you invite the team.

The docs are explicit that step 5 is urgent. Until you set an email URL or disable sign-ups, anyone who reaches a fresh instance can create a confirmed account, the admin address included.

## What stays managed on Kortix Cloud

On Kortix Cloud the same stack is hosted for you: the control plane, the database, TLS and the daily updater are Kortix's problem, and you start a session without provisioning a server or a sandbox key. Self-hosting is free, so the choice is about where the data and the operations sit, not about a price difference.

Three things behave the same on both. Sandboxes run at a cloud sandbox provider, not on your box. Model access is yours either way: any model provider with your own keys, or the ChatGPT plan you already pay for, or sign in with your OpenCode Console account for OpenCode Zen and Go. And the review boundary does not move: session work reaches main through a change request, and merge is default-deny for agents.
