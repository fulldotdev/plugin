# Fulldev

Work with your Fulldev organization from your AI assistant: find, create and update tasks and projects in Fulldev Work, check your websites and the findings of Fulldev Scan, read conversations in Fulldev Message and contacts in Fulldev Contacts, and use your own connected business tools, such as Google or Shopify, through Fulldev Connect. Owners and admins also manage their organization's members, invitations and teams.

This plugin holds two things:

- **The Fulldev connector**, the remote MCP server at `https://app.full.dev/mcp`, run by Fulldev. It is the only service the plugin connects to.
- **The `fulldev` skill**, which explains to the assistant how Fulldev works: start with the overview, describe a type or an action before using it, update with the revision it read, confirm actions that send or invite with you first, and retry a write with the same idempotency key. In a terminal without the connector, the skill uses the [Fulldev CLI](https://www.npmjs.com/package/fulldev) instead.

The plugin runs no code on your computer and has no hooks.

## Sign in and access

The first call asks you to sign in with your Fulldev account at app.full.dev. You then choose the organizations, none ticked at first, and how far the assistant may go: Read, Make changes or Administer. Every call is checked against those choices and your current access in Fulldev. Change or revoke the connection under AI connections on your Fulldev profile.

## Data

The connector receives only the calls the assistant makes, not your conversation. What it returns goes to your assistant's provider, which processes it under its own terms. Calls that read or change your organization's data are recorded in its activity log, without their content. See the [privacy statement](https://full.dev/en/privacy/) and the [terms](https://full.dev/en/terms/).

## Install

- **Claude**: add Fulldev from the directory, or in Claude Code run `/plugin marketplace add fulldotdev/plugin` and `/plugin install fulldev@fulldev`.
- **ChatGPT and Codex**: add Fulldev from the Plugins directory, or run `codex plugin marketplace add fulldotdev/plugin` and install Fulldev from that marketplace under `/plugins`.

More, including Cursor: [full.dev/en/ai-assistants](https://full.dev/en/ai-assistants/).

## Support

Email [contact@full.dev](mailto:contact@full.dev).

## License

MIT
