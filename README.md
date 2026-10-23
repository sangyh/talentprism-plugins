# TalentPrism plugins

Claude and ChatGPT/Codex plugins published by TalentPrism.

| Plugin | For | Server |
|---|---|---|
| [`tradespeoplehq`](plugins/tradespeoplehq) | Employers looking for skilled-trades workers: search the anonymous TradespeopleHQ hotlist and send an open job. No account needed. | `https://www.tradespeoplehq.com/mcp` |
| [`talentprism`](plugins/talentprism) | Recruiters using TalentPrism: read-only command center for your team's candidates, campaigns, reminders and interviews. Sign in with your TalentPrism account. | `https://talentprism.ai/mcp/` |

## Install in Claude Code

```bash
claude plugin marketplace add sangyh/talentprism-plugins
claude plugin install tradespeoplehq@talentprism-plugins
claude plugin install talentprism@talentprism-plugins
```

## Use in Claude (web or desktop) without a plugin

Settings → Connectors → Add custom connector, then paste the server URL from the table above.

## Each plugin folder

- `.claude-plugin/plugin.json`: Claude plugin manifest
- `.codex-plugin/plugin.json`: ChatGPT / Codex plugin manifest
- `.mcp.json`: the remote MCP server
- `skills/`: instructions that tell the assistant how to use the tools and what not to do
- `assets/`: icon and logo

Support: support@talentprism.ai
