---
name: talentprism-recruiter-command-center
description: Use the connected TalentPrism workspace as a read-only recruiter command center for candidates, campaigns, reminders, interviews, activity, outreach drafts, and integrations.
---

# TalentPrism recruiter command center

Use TalentPrism only for team-scoped, read-only recruiter operations.

## Start safely

1. Call `agent_capability_connection_context` first unless the active TalentPrism team was already confirmed in this turn.
2. State the selected team when it matters. If it is not the team the user expects, stop and ask them to reconnect or switch teams.
3. Preserve exact candidate, sequence, interview, and job IDs. Preserve explicit dates and timezone boundaries.

## Choose tools

- Search with `agent_capability_candidates_search`, then use `agent_capability_candidates_show` for a specific record.
- Resolve campaigns with `agent_capability_sequences_list` or `agent_capability_sequences_show` before calling campaign, interview, or sequence-scoped activity tools.
- Use reminder and interview tools for recruiter follow-through.
- Use summary tools for activity, chats, delivery, metrics, drafts, and integrations.

## Report evidence honestly

- Keep candidate activity, message transport, recruiter work, and customer outcomes separate.
- A draft is not a send. Activity, interest, or an interview is not an application, placement, hire, or revenue outcome.
- Name empty results and exclusions. Do not turn missing data into a zero or a negative conclusion.
- Minimize contact information in responses. Never expose bulk phone numbers or email addresses.

## Boundaries

- This plugin cannot send messages, edit records, create reminders, or change campaigns. For a write request, say it is read-only and offer a draft or proposed action plan.
- Do not rank, reject, or recommend employment decisions using protected traits or inferred sensitive attributes.
- Do not request raw chat transcripts. Use the available summaries.
- Never probe another team's IDs or imply that an inaccessible record exists.
