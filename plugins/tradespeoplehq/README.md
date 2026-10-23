# TradespeopleHQ for Claude, ChatGPT and Codex

Find screened skilled-trades workers on the TradespeopleHQ hotlist and send your open job, from Claude, ChatGPT or Codex.

TradespeopleHQ keeps a live, anonymous hotlist of welders, shipfitters, pipefitters, electricians and other trades
workers who were screened and recently confirmed they want work. With this plugin an employer can:

1. **Search the hotlist** (`search_workers`) by trade, state, years of experience, pay and per diem.
2. **Open a worker card** (`get_worker`) by its reference, e.g. `TP-1A2B3C4D`.
3. **Send an open job** (`submit_open_job`) so TradespeopleHQ can introduce matching workers who say yes. The first
   introduction is free; see https://www.tradespeoplehq.com/employers for pricing.

The `find-tradespeople` skill walks Claude through that flow: ask for trade, location and pay, search, show the cards
as a table, then draft the job and get your explicit OK before sending it.

## Endpoint

Public Streamable HTTP MCP server, no login: `https://www.tradespeoplehq.com/mcp` (configured in `.mcp.json`).

## Boundaries

- Worker cards are anonymous. Names, phone numbers, emails and exact addresses are never returned; they are shared
  only after a worker says yes to a specific job.
- Facts on a card are candidate-stated unless labeled otherwise.
- The plugin never texts, calls or emails a worker. `submit_open_job` only sends your job to TradespeopleHQ, which
  reviews it and replies to you by email.
- Sending a job requires your consent that TradespeopleHQ may show it, under its terms, to matching workers in its
  pool (`consent_to_list`).
- No promises that a worker will accept or be hired, and no ranking by age or other protected traits.

## Install

From a checkout of this repository:

```bash
claude --plugin-dir plugins/tradespeoplehq
```

Or through the repository's plugin marketplace (`.claude-plugin/marketplace.json`, name `talentprism-plugins`):

```bash
claude plugin marketplace add sangyh/talentprism-plugins
claude plugin install tradespeoplehq@talentprism-plugins
```

Inside Claude Code the same works with `/plugin marketplace add sangyh/talentprism-plugins` and `/plugin install tradespeoplehq@talentprism-plugins`.

## ChatGPT and Codex

The same folder is packaged for OpenAI's plugin directory in `.codex-plugin/plugin.json`: it reuses `.mcp.json`, the
`find-tradespeople` skill (also the onboarding skill) and the icon and logo in `assets/` (the TradespeopleHQ brand
mark from the site header). No login or OAuth: the server is public.

## Testing and review

`submit_open_job` takes `dry_run: true` for testing. A dry run applies the same checks (consent, email, worker
references) and returns the exact payload that would be sent, with `"submitted": false, "dry_run": true`; nothing is
sent or saved. Reviewers should use it, so the review writes no real employer request. The skill only uses it when
the user asks to test.

Demo recording steps (for the owner; no `demo_recording_url` is set until a recording exists):

1. In ChatGPT (or Claude) with the plugin connected, ask: "Find welders available in Mississippi." Show the
   anonymous cards and the note that facts are candidate-stated.
2. Ask to open the first worker's card by its `TP-` reference (`get_worker`). Show there is no name or contact.
3. Ask: "Which shipfitters would work for $34 an hour or less?" (`max_hourly_pay_floor`).
4. Ask for the worker's phone number and show the refusal and the approval-step explanation.
5. Ask to send a test open job as a dry run. Show the assistant listing the fields and asking for consent, agree,
   and show the result: `submitted: false`, `dry_run: true`, "nothing was sent".

## Support

support@talentprism.ai · https://www.tradespeoplehq.com/ · Privacy: https://www.tradespeoplehq.com/privacy
