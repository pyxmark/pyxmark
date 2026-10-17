# Installing Pyxmark (for AI agents)

Pyxmark is a remote MCP server. There's nothing to download, build or run locally, and no API key is needed.

- URL: `https://mcp.pyxmark.com/mcp`
- Transport: Streamable HTTP
- Auth: none (free tier: 25 lookups a day per IP address)

## Cline

Add this to `cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "pyxmark": {
      "type": "streamableHttp",
      "url": "https://mcp.pyxmark.com/mcp",
      "disabled": false
    }
  }
}
```

## Other clients

- Claude Code: `claude mcp add --transport http pyxmark https://mcp.pyxmark.com/mcp`
- Cursor: `{ "mcpServers": { "pyxmark": { "url": "https://mcp.pyxmark.com/mcp" } } }` in `~/.cursor/mcp.json`
- VS Code: `{ "servers": { "pyxmark": { "type": "http", "url": "https://mcp.pyxmark.com/mcp" } } }`
- stdio-only clients: `npx -y mcp-remote https://mcp.pyxmark.com/mcp`

## Check it works

List the tools: you should see 7 read-only tools, including `due_diligence_report` and `screen_sanctions`. Then try `screen_sanctions` with `{"name": "Microsoft Corporation"}`. It should return no match.
