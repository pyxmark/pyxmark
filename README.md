<p align="center"><img src="assets/icon-256.png" width="96" height="96" alt="Pyxmark logo"></p>

# Pyxmark

Check a company before you pay it. Pyxmark is a hosted MCP server that screens a company or person against the OFAC, UN, EU and UK sanctions lists, looks the company up in SEC EDGAR, checks its web domain's age and email records, and puts it together in a due-diligence report with a clear, review or hold verdict. Every result links to the official record and says when each list was last synced.

- Server: `https://mcp.pyxmark.com/mcp` (Streamable HTTP, no sign in or key)
- Free, no account or key: 25 lookups a day per IP address
- Docs: https://mcp.pyxmark.com/ · Methodology: https://pyxmark.com/methodology
- Made by Trunnel & Co. · hello@pyxmark.com

This repository holds listing and install files only. The server is hosted; its code isn't published here.

## Connect

Server URL: `https://mcp.pyxmark.com/mcp` (Streamable HTTP). No sign in and no key.

<p><a href="https://cursor.com/en/install-mcp?name=pyxmark&config=eyJ1cmwiOiJodHRwczovL21jcC5weXhtYXJrLmNvbS9tY3AifQ%3D%3D"><img src="https://img.shields.io/badge/Install_in-Cursor-000000?style=flat-square" alt="Install in Cursor"></a> <a href="https://vscode.dev/redirect?url=vscode%3Amcp%2Finstall%3F%257B%2522name%2522%253A%2522pyxmark%2522%252C%2522type%2522%253A%2522http%2522%252C%2522url%2522%253A%2522https%253A%252F%252Fmcp.pyxmark.com%252Fmcp%2522%257D"><img src="https://img.shields.io/badge/Install_in-VS_Code-0098FF?style=flat-square" alt="Install in VS Code"></a></p>

**Claude (claude.ai and Claude Desktop):** Customize → Connectors → + Add → Add custom connector. Name it Pyxmark, paste the server URL, choose No sign in, then Add. Free plans allow one custom connector. On Team and Enterprise an owner adds it first under Organization settings → Connectors.

**Claude Code**

```
claude mcp add --transport http pyxmark https://mcp.pyxmark.com/mcp
```

**ChatGPT (web):** Plugins → + → Add custom MCP server. Name it Pyxmark, paste the server URL, pick No authentication, tick the risk box, then Create as a plugin. Install it and pick it with @ in a chat. You don't need Developer mode. OpenAI offers this on Business, Enterprise and Edu (admins and owners add it) and on Pro.

**Codex and the ChatGPT desktop app**

```
codex mcp add pyxmark --url https://mcp.pyxmark.com/mcp
```

Or in the desktop app: Settings → MCP servers → Add server, choose Streamable HTTP and paste the URL.

**Cursor:** use the Install in Cursor button, or add this to `~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` (one project):

```json
{ "mcpServers": { "pyxmark": { "url": "https://mcp.pyxmark.com/mcp" } } }
```

**VS Code (GitHub Copilot):** use the Install in VS Code button, or run MCP: Add Server from the Command Palette, choose HTTP and paste the URL. From a terminal:

```
code --add-mcp '{"name":"pyxmark","type":"http","url":"https://mcp.pyxmark.com/mcp"}'
```

**Grok:** at grok.com/connectors choose New Connector, then Custom, and paste the URL. On Grok Business and Enterprise a team admin adds it first. In Grok Build:

```
grok mcp add --transport http pyxmark https://mcp.pyxmark.com/mcp
```

**Grok Bot:** there's no settings form. Tell your bot "Add this MCP server: https://mcp.pyxmark.com/mcp". It confirms, and the tools work from your next message. (This comes from a Grok Bot staff answer; there's no doc page for it yet.)

**Gemini CLI**

```
gemini mcp add --transport http -s user pyxmark https://mcp.pyxmark.com/mcp
```

**Other clients:** most read the standard block below, which is also this repo's `.mcp.json` (Claude Code, VS Code and Grok Build pick it up from a project root). Clients that only run local stdio servers can use `npx -y mcp-remote https://mcp.pyxmark.com/mcp`.

```json
{ "mcpServers": { "pyxmark": { "type": "http", "url": "https://mcp.pyxmark.com/mcp" } } }
```

**Check it works:** ask "List the Pyxmark tools". You should see 7 read-only tools. Then ask "Is Microsoft Corporation on any sanctions list?" It should come back with no match.

AI agents setting this up for a user: follow [llms-install.md](llms-install.md).

## Tools

All seven tools are read-only.

| Tool | What it does |
|---|---|
| `due_diligence_report` | One report on a vendor: sanctions screen, SEC record and risk filings, domain age and email records, ending in a clear, review or hold verdict with reasons |
| `screen_sanctions` | Fuzzy-screens a name against OFAC SDN and Consolidated, UN, EU and UK lists. Optional birth date, nationality and country tell apart people with the same name. Optional address, email, phone, website, IDs and owners are matched against what the lists record, including sanctioned regions and the OFAC 50 percent rule |
| `search_company` | Finds which SEC-registered company a name, ticker or CIK refers to |
| `company_profile` | The SEC EDGAR record for one company: identity, address, three years of key financials and recent filings |
| `domain_age` | Domain registration date and registrar (RDAP, with a WHOIS fallback) and its MX, SPF and DMARC records |
| `state_registry_link` | A link to the US state business registry search for a company |
| `check_exclusions` | SAM.gov federal exclusions. Not synced yet: it returns a link to search SAM.gov yourself |

## Try asking

- "Run a due diligence report on Acme Corp, acme.com, Delaware."
- "Is this supplier on any sanctions list?"
- "Show me Tesla's last three years of revenue and recent 8-Ks."

## Read this

Results are informational, not a compliance determination. Names are matched fuzzily, so check any potential match against the linked official entry before you act. Pyxmark isn't for consumer screening (credit, jobs, housing, insurance or tenancy).

Privacy: https://pyxmark.com/privacy · Terms: https://pyxmark.com/terms

UK Sanctions List data contains public sector information licensed under the Open Government Licence v3.0.
