# TalentPrism for Claude, ChatGPT and Codex

TalentPrism is a recruiter command center for a user's connected TalentPrism workspace.
It uses OAuth and the public Streamable HTTP MCP endpoint at `https://talentprism.ai/mcp`.

The plugin can inspect team-scoped candidates, campaigns, reminders, interviews, activity,
outreach drafts, and integrations. It cannot mutate records, expose raw transcripts, or make hiring decisions.

Sending: by default a connection is read-only and cannot send outreach. The endpoint can send candidate texts and
emails only when all of these hold:

- the client requested `mcp:tools:read mcp:tools:write` and the person ticked the Sending box on the consent screen;
- a TalentPrism admin turned on "MCP connector sending" for the team (off by default);
- the client previews the send (`..._preview` tool), shows the person the exact message, and gets their approval
  before calling the send tool with an `idempotency_key`.

Each send reaches a real person and cannot be undone. Candidates who replied STOP or are marked do-not-contact are
always refused. This plugin's skill still treats the workspace as read-only. If the client asks for every advertised
scope, the consent screen shows the Sending box unticked; leaving it unticked keeps the connection read-only.

## Packaging

One folder serves every client: the MCP config (`.mcp.json`) and the skill (`skills/`) are shared.

- Claude: `.claude-plugin/plugin.json`, listed in the repository marketplace `.claude-plugin/marketplace.json`
  (`talentprism-plugins`). Install from a checkout with `claude --plugin-dir plugins/talentprism`, or:

  ```bash
  claude plugin marketplace add sangyh/talentprism-plugins
  claude plugin install talentprism@talentprism-plugins
  ```

  Claude connects to the same OAuth endpoint and asks you to sign in to TalentPrism on first use.
- ChatGPT and Codex: `.codex-plugin/plugin.json` (published in OpenAI's plugin directory as 0.1.1).

Public links:

- Website: https://talentprism.ai/
- Support: https://talentprism.ai/support/
- Privacy: https://talentprism.ai/privacy/
- Terms: https://talentprism.ai/terms/
- Developer documentation: https://talentprism.ai/developers/
