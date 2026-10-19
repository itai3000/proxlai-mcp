# Installing the Proxlai MCP server (for AI agents)

Proxlai is a **remote** MCP server. There is nothing to download, build or run, and no API key is needed to start.

- Endpoint: `https://proxlai.com/api/mcp`
- Transport: Streamable HTTP
- Auth: none required (100 lookups a day per address). An optional API key raises the limit (see below).

## Cline

Add this entry to `cline_mcp_settings.json` under `mcpServers`, then save. Cline connects on its own:

```json
{
  "mcpServers": {
    "proxlai": {
      "type": "streamableHttp",
      "url": "https://proxlai.com/api/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

If this Cline version only supports local (stdio) servers, use the `mcp-remote` bridge instead (needs Node.js):

```json
{
  "mcpServers": {
    "proxlai": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://proxlai.com/api/mcp"],
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

## Other clients

- Claude Code: `claude mcp add --transport http proxlai https://proxlai.com/api/mcp`
- Cursor, Windsurf, Claude Desktop: `{ "mcpServers": { "proxlai": { "url": "https://proxlai.com/api/mcp" } } }`

## Check it works

Call `list_markets`. It should return 38 markets, each with an id (such as `llm`, `text-to-speech` or `gpu-on-demand`) and its pricing unit. Then try `search_offerings` with `{ "market": "llm", "limit": 3 }`.

## Optional: API key

For more than 100 lookups a day, the user creates a key at https://proxlai.com/dashboard. Keep it in the `PROXLAI_API_KEY` environment variable, never in code or chat, and send it as a header:

```json
"headers": { "Authorization": "Bearer ${PROXLAI_API_KEY}" }
```

## When quoting prices

Give the price with its unit and `verified_at` date, link the `source_url`, say when a price is marked unverified, and remind the user that prices change, so they should confirm on the provider's site before buying.
