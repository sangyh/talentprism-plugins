---
name: find-tradespeople
description: Find screened skilled-trades workers on the TradespeopleHQ hotlist and send an open job for introductions. Use when an employer, shipyard, contractor or staffing agency wants welders, shipfitters, pipefitters, electricians, machinists, painters/blasters or other tradespeople, asks who is available, or wants to post or send a trades job.
---

# Find tradespeople with TradespeopleHQ

TradespeopleHQ keeps a live hotlist of skilled-trades workers who were screened and recently confirmed they are
looking for work. The `tradespeoplehq` MCP server has three tools:

- `search_workers`: anonymous cards from the hotlist, freshest availability first. Read-only.
- `get_worker`: one anonymous card by reference (TP-XXXXXXXX). Read-only.
- `submit_open_job`: sends the employer's job to TradespeopleHQ so it can introduce matching, interested workers.
  It contacts no worker by itself.

## Workflow

1. **Get the basics.** If the user has not said them, ask for the trade, the job location (city and state) and the
   pay. One short question covering the missing pieces is enough; don't block on optional details.
2. **Search.** Call `search_workers` with `trade` and `state`, and `max_hourly_pay_floor` when the pay is an hourly
   number. Add `min_years`, `per_diem_not_required` or `max_days_since_confirmed` only when the user asks for them.
   If nothing matches, retry once with fewer filters (drop pay, then state) and say what you relaxed.
3. **Show the cards** as a compact table:

   | Reference | Trade | Region | Years | Min pay | Per diem | Confirmed |
   |---|---|---|---|---|---|---|
   | TP-1A2B3C4D | Welder | Gulf Coast | 12 | $32/hr | Not required | 3 days ago |

   Below the table, say plainly that these facts are what the workers told TradespeopleHQ (candidate-stated), and
   that names and contact details come only after a worker says yes to a specific job. Use `get_worker` if the user
   wants one card in full.
4. **Offer to send the job.** If the user wants any of these workers, or wants TradespeopleHQ to recruit for the
   role, draft the open-job request. Required: company, contact name, work email, role title, location, pay.
   Optional: phone, trade, number of openings, per diem, start date, notes, and the worker references they liked.
5. **Confirm before submitting.** Show the exact fields you will send. Ask the user to confirm them and to agree that
   TradespeopleHQ may show this job, under its terms, to matching workers in its pool (`consent_to_list`). Only after
   an explicit yes, call `submit_open_job` with `consent_to_list: true` and a fresh `idempotency_key` (for example a
   short random string). If you retry after an error, reuse the same key. Leave `dry_run` unset for a real job; set
   `dry_run: true` only when the user asks to test the flow (it checks the fields and sends nothing).
6. **Close the loop.** Relay the `next_steps` from the result: TradespeopleHQ replies by email, workers hear about the
   job only from TradespeopleHQ after review, and nobody's contact details are shared without that worker's yes.

## Boundaries

- Never ask for, guess or reveal a worker's name, phone, email or exact address. The cards are anonymous on purpose.
- Never promise that a specific worker will say yes, show up or be hired. Introductions depend on the worker.
- Never invent workers or fill a table with examples. If the search is empty, say so and offer to send the job
  anyway: TradespeopleHQ also recruits for open roles.
- Do not rank, filter or comment on workers by age, sex, race, religion, national origin, disability or any other
  protected trait, even if asked. Stick to trade, location, experience, pay, per diem and availability.
- Do not quote prices beyond "the first introduction is free". If the user asks about cost, point them to
  https://www.tradespeoplehq.com/employers.
- Never call `submit_open_job` without the user's explicit confirmation of the fields and of `consent_to_list`.
- If a tool says the hotlist is unavailable, tell the user and offer to send the job instead.
