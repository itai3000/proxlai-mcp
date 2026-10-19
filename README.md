# Proxlai MCP server

**Live, verified prices for AI APIs, inside your coding agent.**

[Proxlai](https://proxlai.com) is a price book for AI APIs: 231 APIs from 113 providers across 38 markets (LLMs, GPU rental, image and video generation, text-to-speech, speech-to-text, embeddings, vector databases, 3D and more). Every market is priced in one unit, and every price has the date it was verified and a link to the provider's own pricing page.

This is a **remote MCP server**: nothing to install or run.

```
https://proxlai.com/api/mcp
```

Read-only · Streamable HTTP · no account needed (100 lookups a day free; an API key raises the limit).

## Connect

**Claude Code**
```bash
claude mcp add --transport http proxlai https://proxlai.com/api/mcp
```

**Cursor, Windsurf, Claude Desktop and other JSON-configured clients**
```json
{ "mcpServers": { "proxlai": { "url": "https://proxlai.com/api/mcp" } } }
```

**Clients that only run local (stdio) servers**
```json
{ "mcpServers": { "proxlai": { "command": "npx", "args": ["-y", "mcp-remote", "https://proxlai.com/api/mcp"] } } }
```

Or paste this to your agent and let it set itself up:
> Read https://proxlai.com/agents.md and follow it to connect Proxlai to this project, so you can look up and compare AI API prices for me.

## Tools

| Tool | What it does |
|---|---|
| `list_markets` | Every market with its id and pricing unit. Start here. |
| `describe_market` | What a market is, how its pricing works, and the attributes you can filter on. |
| `search_offerings` | Rank a market's offerings by price, quality and speed, with requirements and a maximum price. |
| `get_offering` | One offering in full: capabilities, current price with its source, price history. |
| `compare_offerings` | 2 to 4 offerings from one market side by side. |

## Try asking your agent

- "What's the cheapest LLM API with tool use and a 1M-token context?"
- "Cheapest text-to-speech API with voice cloning?"
- "Where can I rent an H100 for the least per hour right now?"
- "Compare the three cheapest embeddings APIs."
- "I'm building an MVP. Which model gives the best quality for the price?"

Every answer comes with the unit, the verified date and the provider's pricing link. Prices change often, so confirm on the provider's site before you buy.

## Limits and keys

- **Without a key:** 30 calls a minute and 100 searches or lookups a day per address.
- **With a key:** create one at https://proxlai.com/dashboard and send it as `Authorization: Bearer <key>` (keep it in the `PROXLAI_API_KEY` environment variable). It includes 100 free lookups a day per account, then $0.01 each from your credit balance.

## Links

- Website: https://proxlai.com
- MCP docs: https://proxlai.com/docs/mcp
- REST API: https://proxlai.com/docs/api
- Agent setup guide: https://proxlai.com/agents.md
- Support: support@proxlai.com
