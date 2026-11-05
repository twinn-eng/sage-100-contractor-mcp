# Getting Started

This guide connects an MCP client to the Twinn demo server for Sage 100 Contractor.

## Demo server

| | |
|---|---|
| Server URL | `https://demo-mcp.twinn.engineering/mcp` |
| Transport | Streamable HTTP |
| Authentication | OAuth 2.1 (see [Authentication](authentication.md)) |
| Access | Read-only |

The demo is connected to **Ridgeline Mechanical & Plumbing**, a sample mechanical and plumbing contractor built in Sage 100 Contractor. The data is rebuilt every night, so anything you see today will be reset tomorrow. The server cannot post, edit, or delete records.

## Connect a client

### Claude (web and desktop)

1. Open **Settings > Connectors** and choose **Add custom connector**.
2. Enter `https://demo-mcp.twinn.engineering/mcp` as the URL.
3. Select **Connect** and sign in when the browser window opens.

If your version of Claude Desktop only supports local servers, use the config in [`examples/claude-desktop.json`](../examples/claude-desktop.json). It runs `mcp-remote` as a local bridge and needs Node.js 18 or later.

### Cursor

Add the entry from [`examples/cursor.json`](../examples/cursor.json) to `~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` (one project). Cursor shows a **Login** button next to the server the first time it connects.

### Other clients

Any MCP client that supports remote servers over Streamable HTTP with OAuth will work. Point it at the server URL above.

## Try it

Once connected, ask a question about Ridgeline's data. [`examples/sample-prompts.md`](../examples/sample-prompts.md) has some to start with.

## Next steps

- [Authentication](authentication.md)
- [FAQ](faq.md)
