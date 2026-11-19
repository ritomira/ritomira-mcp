# Ritomira MCP

[日本語](README.ja.md)

Connect your AI app to [Ritomira](https://ritomira.com/en) over MCP. Ask Claude, ChatGPT or another MCP-compatible app to review how your X (Twitter) posts performed, then turn the next ideas into drafts and scheduled posts — without leaving the chat.

This repository contains **setup instructions and configuration examples only**. The MCP server is hosted by Ritomira; there is nothing to install or run.

| | |
|---|---|
| Connection URL | `https://mcp.ritomira.com/mcp` |
| Transport | Streamable HTTP |
| Authentication | OAuth (sign in to Ritomira in your browser; no API keys) |
| Official MCP Registry | [`com.ritomira/ritomira`](https://registry.modelcontextprotocol.io/) |
| Supported network | X. Instagram, Threads and Facebook Pages are planned. |
| Plans | Standard or higher. Some analysis (content themes) requires Pro or higher. See [pricing](https://ritomira.com/en/pricing). |

## What you can ask

- "How did my posts do last week compared with the week before?"
- "Show my top posts this month and what they have in common."
- "When do my posts get the most engagement?"
- "Draft three posts based on what worked, and schedule the best one for Thursday at 9:00."

## Permissions and safety

- **Read-only by default.** A new connection can only read your posts and analytics.
- **You turn on more yourself.** Drafts, scheduled posts and other actions are enabled per connection in Ritomira's settings. After changing them, reconnect from your AI app.
- **A person approves actions that cannot be undone.** Replies and follows on X, comment replies, and publishing X Articles are approved by you on a confirmation screen in the AI app, not by the AI. Apps that cannot show that screen cannot perform these actions.
- **Disconnect at any time** from Ritomira's settings. The app stops working from its next request.

Details: [Security and data handling](https://ritomira.com/en/security).

## Setup

### Claude (desktop and web)

1. In Claude, open **Customize → Connectors** and add a custom connector.
2. Name it `Ritomira` and enter `https://mcp.ritomira.com/mcp`. Connect with OAuth, sign in to Ritomira, and review the account and allowed actions.
3. Enable Ritomira in Claude, then try the [first request](#first-request).

Your organization may require an administrator to allow custom connectors. [Claude's instructions](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp)

### Claude Code

```bash
claude mcp add --transport http --scope user ritomira https://mcp.ritomira.com/mcp
```

Then open `/mcp` in Claude Code, select `ritomira` and authenticate in the browser. [Claude Code's instructions](https://code.claude.com/docs/en/mcp)

### ChatGPT (web)

1. In ChatGPT, add a custom MCP server.
2. Name it `Ritomira`, enter `https://mcp.ritomira.com/mcp`, and choose OAuth.
3. Sign in to Ritomira, review the account and allowed actions, and enable it.

Available options depend on your ChatGPT plan and workspace settings. [OpenAI's instructions](https://developers.openai.com/api/docs/guides/custom-mcp-server)

### Codex CLI

```bash
codex mcp add ritomira --url https://mcp.ritomira.com/mcp
codex mcp login ritomira
```

Open `/mcp` in Codex to check the connection. Remove it with `codex mcp remove ritomira`. [Codex's instructions](https://developers.openai.com/codex/mcp)

### Other apps

Add `https://mcp.ritomira.com/mcp` as a remote HTTP (Streamable HTTP) MCP server and start OAuth. A JSON example is in [`examples/mcp.json`](examples/mcp.json). The app must support Streamable HTTP and OAuth; not every app has been tested.

## First request

Start with a read-only request to check the connection:

> List the social accounts connected to Ritomira, showing their names and platforms. If there is more than one, ask me to choose an account. Only perform read operations.

## Troubleshooting

- **"A higher plan is required"**: MCP requires Standard or higher. Reconnect after changing plans.
- **Drafts or scheduling are unavailable**: turn them on in Ritomira's settings, then reconnect.
- **Asked to authenticate again**: reconnect from your app's MCP settings and sign in to Ritomira.

## Links

- [MCP integration guide](https://ritomira.com/en/features/mcp) — full tool list and permissions
- [Ritomira](https://ritomira.com/en)
- [Contact](https://ritomira.com/en/contact)

Operated by NeXus AI LLC.
