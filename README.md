# Re-Pricer for AI agents

Connect your OnBuy account to [Re-Pricer](https://re-pricer.com) from the terminal. Check the Buy Box and reprice listings inside your own min and max prices.

## Install

```
/plugin marketplace add jackculpan/agents
/plugin install re-pricer@re-pricer
/re-pricer:setup
```

Cursor: install Re-Pricer from the Cursor Marketplace, or add it by hand in `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "re-pricer": { "url": "https://mcp.re-pricer.com/mcp" } } }
```

Then open Cursor Settings, MCP, and click "Needs login" next to `re-pricer`.

ChatGPT and Codex: install the Re-Pricer plugin from the plugin directory and click Connect.

Claude Desktop or claude.ai: open Settings, Connectors, Add custom connector, and use `https://mcp.re-pricer.com/mcp`. On Team and Enterprise plans, an owner must add the connector first.

Other AI agents: "Read https://re-pricer.com/setup.md and follow it to set up Re-Pricer for my OnBuy account."

## What it does

- Connects the remote Re-Pricer MCP server at `https://mcp.re-pricer.com/mcp` (OAuth, no keys in chat).
- Lists your listings and shows which ones win the Buy Box.
- Reprices only inside the min and max price of each listing, and only after you confirm.

Your OnBuy API keys go into https://re-pricer.com/api-keys in the browser. They never enter the chat.

## Layout

| Path | Used by |
| --- | --- |
| `.claude-plugin/marketplace.json`, `plugin/.claude-plugin/plugin.json`, `plugin/.mcp.json` | Claude Code |
| `.cursor-plugin/marketplace.json`, `plugin/.cursor-plugin/plugin.json`, `plugin/mcp.json` | Cursor |
| `plugin/plugin.json`, `plugin/mcp.json` | ChatGPT and Codex (Agent Plugins) |
| `plugin/skills/setup/SKILL.md`, `plugin/assets/logo.png` | All |

## License

MIT
