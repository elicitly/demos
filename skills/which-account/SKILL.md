---
name: which-account
description: Elicitly demo (sample data, logs nothing). When a name matches several sample CRM accounts, ask a human to pick the right one on a review page. Use only when the user asks to log call notes for Harbor in the demo or to run the which-account demo.
license: MIT-0
compatibility: Requires Elicitly Pro (elicit_selection, elicit_await, elicit_result).
---

# Which account?

> **Demo.** Uses made-up sample data from `assets/`, connects to no real system, and changes nothing. It's a reference for how to use Elicitly: adapt it to your own data and systems.

"Log this against Harbor" matches three accounts. Rather than guess, the agent
lists the candidates with enough detail to tell them apart and lets a human
choose. The choice is a real radio button on the review page, and only a
valid account id can come back.

## Steps

1. Read `assets/matches.json`. It is a complete `elicit_selection` input.
2. Call `elicit_selection` with that object as-is.
3. Give the user the `reviewUrl` as a link, and say the choice is waiting
   there.
4. Call `elicit_await` with the `elicitationId`. While it returns `pending`,
   call it again. Stop when the status is anything else.
5. If the status is `submitted` or `declined`, call `elicit_result`:
   - `decision: "submitted"`: look up the chosen id in `selectedIds` among
     the options and name the account. This demo logs nothing; say "In a
     real skill, the call notes would be logged to this account here."
   - `decision: "declined"`: none of the accounts was right. Ask the user
     for another detail (city, contact name) to narrow the search.
   For `expired` or `canceled`, say no choice was made and offer to ask
   again.
