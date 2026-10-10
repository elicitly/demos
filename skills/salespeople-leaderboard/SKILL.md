---
name: salespeople-leaderboard
description: Elicitly demo (made-up sample data, not your CRM): show a sample sales leaderboard as a ranked card with photos, sales totals and quota progress. Use only when the user asks for the demo sales leaderboard or to run the salespeople-leaderboard demo.
license: MIT-0
compatibility: Elicitly Free or Pro (elicit_display) in a host that renders MCP Apps. Photos load from https://www.elicitly.ai, which must be an allowed origin.
---

# Salespeople leaderboard

> **Demo.** Uses made-up sample data from `assets/`, connects to no real system, and changes nothing. It's a reference for how to use Elicitly: adapt it to your own data and systems.

Shows a sales leaderboard with `elicit_display` instead of a Markdown table.
The layout lives in a template, so it looks the same every time; you only
supply the data.

## Steps

1. Read the sales figures from `assets/leaders.json`. (In a real skill this
   would be a CRM query.)
2. Call `elicit_display` with:
   - `title`: `Top salespeople — ` followed by the `month` from the data
   - `template`: the contents of `assets/leaderboard.liquid`, verbatim
   - `context`: `{ "people": <the people array> }`
   - `summary`: one sentence naming the leader and their quota percentage
3. If the result says the host can't render MCP Apps, give the ranking as a
   short numbered list in your reply. Otherwise don't repeat the data; add at
   most one sentence of insight (for example, who is closest to quota).

## Notes

- Sofia Ramirez has no photo on purpose: the template falls back to initials.
- Photos come from `https://www.elicitly.ai`. If the result reports it as a
  blocked origin, tell the user how to allow it: Free, set
  `ELICITLY_DISPLAY_RESOURCE_DOMAINS=https://www.elicitly.ai`; Pro, add it to
  the organization's allowed origins.
