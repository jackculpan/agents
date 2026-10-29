# Re-Pricer for Claude Code

Connect your OnBuy account to [Re-Pricer](https://re-pricer.com) from the terminal. Check the Buy Box and reprice listings inside your own min and max prices.

## Install

```
/plugin marketplace add jackculpan/agents
/plugin install re-pricer@re-pricer
/re-pricer:setup
```

Other AI agents: "Read https://re-pricer.com/setup.md and follow it to set up Re-Pricer for my OnBuy account."

## What it does

- Connects the remote Re-Pricer MCP server at `https://re-pricer.com/mcp` (OAuth, no keys in chat).
- Lists your listings and shows which ones win the Buy Box.
- Reprices only inside the min and max price of each listing, and only after you confirm.

Your OnBuy API keys go into https://re-pricer.com/api-keys in the browser. They never enter the chat.

## License

MIT
