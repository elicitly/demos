---
name: release-go-no-go
description: Elicitly demo (sample data, deploys nothing). Present a sample release readiness card, then ask the user to confirm before shipping. Use only when the user asks to ship the Brightwater Portal demo release or to run the release-go-no-go demo.
license: MIT-0
compatibility: Elicitly Free or Pro (elicit_display, elicit_confirm). The confirm dialog needs a host that renders form elicitation; see https://www.elicitly.ai/docs/elicitation/support-matrix/
---

# Release go/no-go

> **Demo.** Uses made-up sample data from `assets/`, connects to no real system, and changes nothing. It's a reference for how to use Elicitly: adapt it to your own data and systems.

The agent shows what is about to ship, then stops and asks. The question is a
real dialog answered by a human, not a "should I continue?" line in chat that
the model might answer for itself.

## Steps

1. Read `assets/release.json`.
2. Call `elicit_display` with:
   - `title`: `Release ` followed by `product` and `version`
   - `template`: the contents of `assets/readiness.liquid`, verbatim
   - `context`: the whole object from `assets/release.json`
   - `summary`: one sentence with the version, the passing/total checks, and
     the risk level
   If the host can't render MCP Apps, summarize the checks and changes in a
   few lines instead.
3. Call `elicit_confirm` with:
   - `message`: `Ship <product> <version> to production?`
   - `labels`: `{ "ok": "Ship it", "cancel": "Hold" }`
4. Act on the answer, which has three states:
   - `confirmed: true`: say the release is shipping. (This demo ships
     nothing; say "In a real skill, the deploy would start here.")
   - `confirmed: false`: the user chose Hold. Acknowledge it and stop.
   - `confirmed: null`: no answer (dismissed, timed out, or the host can't
     show dialogs). Do not ship. Say no decision was recorded and offer to
     ask again.

Never treat a chat reply as the decision in step 4; only the dialog result
counts.
