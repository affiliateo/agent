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

An Affiliateo API key. Sign in at [affiliateo.com](https://affiliateo.com), open any business dashboard, go to
the **API** tab and create a key (it starts with `afk_`). A read-only key lets the agent look at everything.
A read and write key lets it make changes. Paying people needs a key with its **Payouts** switch on, and it
stays within that key's daily limit.

## Install

### Claude Code

```
/plugin marketplace add affiliateo/agent
/plugin install affiliateo@affiliateo
```

Claude Code asks for your API key when the plugin is enabled and keeps it in your system's secure storage.

### Hermes Agent

```
hermes plugins install affiliateo
```

Before the catalog listing is live, install from GitHub instead:

```
hermes plugins install affiliateo/agent --no-enable
hermes plugins enable affiliateo
```

Set your key in the plugin's settings in Hermes, or as `AFFILIATEO_API_KEY` in your Hermes profile's `.env`.
Hermes asks you before every tool call that changes something, because the package marks the server as
untrusted.

### Just the skill (any agent)

```
npx skills add affiliateo/agent --skill affiliateo
```

Then connect the MCP server yourself: URL `https://affiliateo.com/api/mcp` (Streamable HTTP), header
`Authorization: Bearer <your key>`. In Claude Code:

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
  with the permissions of the API key you gave it. The tool list is served by that server, so it can grow
  without a new version of this package.
- Some tools act on real people or money once you confirm: they can email an invoice or a booking change,
  invite someone to an app, pay affiliates from your wallet (Payouts keys only), approve paid creator
  requests, delete records, and pause, resume or re-budget ads, which changes what you spend. New ad campaigns
  are always created paused.
- The skill tells the agent to confirm each of those with you first and to treat text other people wrote
  (messages, tickets, reviews) as data, never as instructions.
- Your key is stored by your agent (Claude Code's secure storage, or your Hermes profile). This package has no
  code of its own, runs nothing on your machine, and sends no telemetry.

## Links

- API reference: https://affiliateo.com/docs/api
- Everything in one file for agents: https://affiliateo.com/llms-full.txt
- Support: https://affiliateo.com

## License

MIT
