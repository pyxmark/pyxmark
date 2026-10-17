# Installing Pyxmark (for AI agents)

Pyxmark is a hosted, remote MCP server. There's nothing to download, build or run, and the user needs no account or API key.

- URL: `https://mcp.pyxmark.com/mcp`
- Transport: Streamable HTTP
- Auth: none. Pick "no authentication" or "no sign in" wherever a client asks.
- Free tier: 25 tool calls a day per IP address
- Server card: `https://mcp.pyxmark.com/.well-known/mcp/server-card.json`

Use the steps for the client you are running in. If yours isn't listed, give it the URL above as a remote Streamable HTTP server.

## Clients with a command

- Claude Code: `claude mcp add --transport http pyxmark https://mcp.pyxmark.com/mcp`
- Codex (also the ChatGPT desktop app): `codex mcp add pyxmark --url https://mcp.pyxmark.com/mcp`
- Grok Build: `grok mcp add --transport http pyxmark https://mcp.pyxmark.com/mcp`
- Gemini CLI: `gemini mcp add --transport http -s user pyxmark https://mcp.pyxmark.com/mcp`
- VS Code: `code --add-mcp '{"name":"pyxmark","type":"http","url":"https://mcp.pyxmark.com/mcp"}'`
- Grok Bot: add `https://mcp.pyxmark.com/mcp` as a custom MCP server when the user asks you to.

## Clients with a config file

Cursor: `~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` (one project):

```json
{ "mcpServers": { "pyxmark": { "url": "https://mcp.pyxmark.com/mcp" } } }
```

Cline: `cline_mcp_settings.json`. Keep the type, or Cline falls back to the older SSE transport:

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

Most other clients (and a project `.mcp.json`, which Claude Code, VS Code and Grok Build read):

```json
{ "mcpServers": { "pyxmark": { "type": "http", "url": "https://mcp.pyxmark.com/mcp" } } }
```

Clients that only run local stdio servers: `npx -y mcp-remote https://mcp.pyxmark.com/mcp`

## Clients the user sets up in a browser

Tell the user these steps; you can't do them yourself.

- Claude (claude.ai, Claude Desktop): Customize → Connectors → + Add → Add custom connector. Name Pyxmark, paste the URL, choose No sign in, Add. Team and Enterprise: an owner adds it under Organization settings → Connectors first.
- ChatGPT (web): Plugins → + → Add custom MCP server. Name Pyxmark, paste the URL, No authentication, tick the risk box, Create as a plugin, then install it. No Developer mode needed. Business, Enterprise, Edu and Pro plans.
- Grok: grok.com/connectors → New Connector → Custom, paste the URL.

## Check it works

List the tools: you should see 7 read-only tools, including `due_diligence_report` and `screen_sanctions`. Then call `screen_sanctions` with `{"name": "Microsoft Corporation"}`. It should return no match.

## When to use it

Use Pyxmark when the user wants to vet a vendor, supplier, contractor or counterparty before paying or onboarding them: sanctions screening, SEC company records, domain age and email records, or one combined report with a clear, review or hold verdict. Results are informational, not a compliance determination. Tell the user to check any potential match against the linked official entry.
