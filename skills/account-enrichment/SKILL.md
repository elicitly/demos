---
name: account-enrichment
description: Elicitly demo (sample data, writes nothing). Propose updates to a sample CRM account from two enrichment sources and let a human review, edit and pick fields in a diff grid. Use only when the user asks to enrich the Larkspur Robotics demo account or to run the account-enrichment demo.
license: MIT-0
compatibility: Requires Elicitly Pro (elicit_proposal, elicit_await, elicit_result).
---

# Account enrichment

> **Demo.** Uses made-up sample data from `assets/`, connects to no real system, and changes nothing. It's a reference for how to use Elicitly: adapt it to your own data and systems.

Enrichment tools disagree, and the CRM already holds values someone typed in.
Instead of overwriting, the agent proposes changes in a grid: two Source
columns (Apollo, Crunchbase), the Current CRM value, and an editable Proposed
column. The reviewer chooses field by field, and only included fields come
back.

## Steps

1. Read `assets/proposal.json`. It is a complete `elicit_proposal` input:
   the agent's proposed values are each property's `default`.
2. Call `elicit_proposal` with that object as-is.
3. Give the user the `reviewUrl` as a link, and say the proposed changes are
   waiting for review there.
4. Call `elicit_await` with the `elicitationId`. While it returns `pending`,
   call it again. Stop when the status is anything else.
5. If the status is `submitted` or `declined`, call `elicit_result`:
   - `decision: "submitted"`: list each field in `formSubmission` with its
     new value, marking any value that differs from the proposed `default`
     as "edited by reviewer". Fields not in `formSubmission` were left
     unchanged; name them in one line. This demo writes nothing; say "In a
     real skill, these fields would be written to the CRM here."
   - `decision: "declined"`: say no changes will be made.
   For `expired` or `canceled`, say no decision was made and offer to send it
   again.
