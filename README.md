<p align="center"><img src="assets/icon-256.png" width="96" height="96" alt="Pyxmark logo"></p>

# Pyxmark

Check a company before you pay it. Pyxmark is a hosted MCP server that screens a company or person against the OFAC, UN, EU and UK sanctions lists, looks the company up in SEC EDGAR, checks its web domain's age and email records, and puts it together in a due-diligence report with a clear, review or hold verdict. Every result links to the official record and says when each list was last synced.

- Server: `https://mcp.pyxmark.com/mcp` (Streamable HTTP, no auth)
- Free, no account or key: 25 lookups a day per IP address
- Docs: https://mcp.pyxmark.com/ · Methodology: https://pyxmark.com/methodology
- Made by Trunnel & Co. · hello@pyxmark.com

This repository holds listing and install files only. The server is hosted; its code isn't published here.

## Connect

**Claude Code**

```
claude mcp add --transport http pyxmark https://mcp.pyxmark.com/mcp
```

**Claude (web and desktop):** Settings → Connectors → Add custom connector. Name it Pyxmark and paste the server URL.

**Cursor** (`~/.cursor/mcp.json`, or use the `.mcp.json` in this repo):

```json
{
  "mcpServers": {
    "pyxmark": { "url": "https://mcp.pyxmark.com/mcp" }
  }
}
```

**VS Code, Windsurf and others:**

```json
{ "servers": { "pyxmark": { "type": "http", "url": "https://mcp.pyxmark.com/mcp" } } }
```

**ChatGPT:** Settings → Apps & Connectors → Advanced settings → turn on Developer mode, then Create. Paste the server URL and choose No authentication.

Clients that only speak stdio can use `npx -y mcp-remote https://mcp.pyxmark.com/mcp`.

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
