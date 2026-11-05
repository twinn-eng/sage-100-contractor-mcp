# Authentication

The server uses OAuth 2.1, following the [MCP authorization specification](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization). You do not need to create or paste an API key. Your MCP client handles the sign-in flow.

## How it works

1. The client calls the server without a token and receives `401 Unauthorized`.
2. The `WWW-Authenticate` header points to the server's protected resource metadata:
   `https://demo-mcp.twinn.engineering/.well-known/oauth-protected-resource/mcp`
3. The metadata names the authorization server, and the client opens a browser window to sign in.
4. After sign-in, the client receives an access token and sends it as a `Bearer` token on every request.

## Scopes

| Scope | Grants |
|---|---|
| `mcp:read` | Read access to the demo company's data |

The demo does not offer write scopes.

## Troubleshooting

**The browser window never opens.** Your client may not support OAuth for remote servers. Use the `mcp-remote` bridge shown in [`examples/claude-desktop.json`](../examples/claude-desktop.json).

**`401 API key missing or invalid` after signing in.** The token has expired or was not saved. Disconnect the server in your client and connect again.

**Signed in to the wrong account.** Clear the saved credentials in your client. For `mcp-remote`, delete the `~/.mcp-auth` folder.
