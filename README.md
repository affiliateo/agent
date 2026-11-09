# Affiliateo for AI agents

![Affiliateo](assets/icon.svg)

Run your [Affiliateo](https://affiliateo.com) business from Claude, Hermes Agent or any AI agent that speaks
MCP. Ask in plain words and the agent does it through Affiliateo's hosted MCP server:

- **Affiliate programs**: affiliates, commissions, personal deals, invites, join requests and payouts
- **Products**: courses, memberships, downloads and services with plans and sales pages
- **Revenue**: MRR, trials, subscriptions, churn and every customer as one person across devices
- **Invoices, leads and booked calls**
- **Paid ads** on Meta, TikTok, Google Ads, Apple Search Ads, Snapchat and X: results, wasted spend,
  pausing, budgets and new campaigns (always created paused)
- **Funnels and visitors**, **courses**, **events**, **community posts**, **support tickets** and **Live Chat**

This package holds one skill (`skills/affiliateo`) that teaches the agent how to use the tools safely, and the
connection to the MCP server at `https://affiliateo.com/api/mcp`.

## What you need

An [Affiliateo](https://affiliateo.com) account. No key to copy: the agent signs in with Affiliateo. Your
browser opens Affiliateo's Authorize page, where you pick:

- **Read only** (the agent can look at everything) or **Read & write** (it can make changes too)
- which areas it may change: businesses and apps, products, content, community, affiliates, leads and
  invoices, ads, webhooks
- all your businesses, or just one

A sign-in can never pay anyone or move money. See every connected app, and disconnect any of them, in any
business dashboard: **API** tab, **Connected apps**.

Want the agent to pay affiliates? Use an API key instead: in the **API** tab, create a key (it starts with
`afk_`) with its **Payouts** switch on. Payouts stay within that key's daily limit.

## Install

### Claude Code

```
/plugin marketplace add affiliateo/agent
/plugin install affiliateo@affiliateo
```

Then run `/mcp`, pick **affiliateo** and choose **Authenticate**. Your browser opens the Affiliateo sign-in.
Claude Code keeps the sign-in in your system's secure storage.

Coming from version 1.0.0? The plugin no longer asks for an API key: run `/mcp` and sign in. To keep using a
key, add the server yourself instead (see "Just the skill" below).

### Claude (claude.ai and the desktop app)

Open **Settings**, **Connectors**, **Add custom connector**, and enter `https://affiliateo.com/api/mcp`.
Click **Connect** and authorize on the Affiliateo page.

### Hermes Agent

```
hermes plugins install affiliateo
```

Before the catalog listing is live, install from GitHub instead:

```
hermes plugins install affiliateo/agent --no-enable
hermes plugins enable affiliateo
```

The Hermes package connects with an API key: set it in the plugin's settings in Hermes, or as
`AFFILIATEO_API_KEY` in your Hermes profile's `.env`. Hermes asks you before every tool call that changes
something, because the package marks the server as untrusted.

To sign in instead of using a key, add the server yourself rather than installing the package:

```
hermes mcp add affiliateo --url https://affiliateo.com/api/mcp --auth oauth
```

### Just the skill (any agent)

```
npx skills add affiliateo/agent --skill affiliateo
```

Then connect the MCP server yourself: URL `https://affiliateo.com/api/mcp` (Streamable HTTP). Clients that
support MCP sign-in (Claude, Claude Code, Cursor, ChatGPT and others) open the Affiliateo sign-in by
themselves. In Claude Code:

```
claude mcp add --transport http affiliateo https://affiliateo.com/api/mcp
```

With an API key instead, send it as the header `Authorization: Bearer <your key>`:

```
claude mcp add --transport http affiliateo https://affiliateo.com/api/mcp --header "Authorization: Bearer <your key>"
```

## Try it

- "How much revenue did we make this week, and from which source?"
- "Who are my top five affiliates this month, and what do I owe them?"
- "Which Meta placements are wasting my budget?"
- "Who booked a call with me today?"
- "Add a lesson called Getting started to my course."

## What this package does, and where data goes

- Every tool call goes to Affiliateo's hosted server at `affiliateo.com` and acts on your Affiliateo account
  with the permissions you picked when you signed in, or those of the API key you gave it. The tool list is
  served by that server, so it can grow without a new version of this package.
- Some tools act on real people or money once you confirm: they can email an invoice or a booking change,
  invite someone to an app, pay affiliates from your wallet and approve paid creator requests (Payouts keys
  only, never a sign-in), delete records, and pause, resume or re-budget ads, which changes what you spend.
  New ad campaigns are always created paused.
- The skill tells the agent to confirm each of those with you first and to treat text other people wrote
  (messages, tickets, reviews) as data, never as instructions.
- Your sign-in or key is stored by your agent (Claude Code's secure storage, Claude's connector settings, or
  your Hermes profile). This package has no code of its own, runs nothing on your machine, and sends no
  telemetry.

## Links

- API reference: https://affiliateo.com/docs/api
- Everything in one file for agents: https://affiliateo.com/llms-full.txt
- Support: https://affiliateo.com

## License

MIT
