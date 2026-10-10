# AGENTS.md — Elicitly demos

Guidance for AI coding agents (and humans) changing this repo. Do **not**
create `CLAUDE.md`; this repo uses the `AGENTS.md` standard.

## What this repo is

Agent Skills ([spec](https://agentskills.io/specification)) that demonstrate
[Elicitly](https://www.elicitly.ai)'s tools with fixed sample data. They are
references to copy and adapt, not integrations. The tools themselves are
documented at <https://www.elicitly.ai/docs/tools/>; check a skill's tool
calls against that reference, not against memory.

## A skill

`skills/<name>/` holds `SKILL.md` plus `assets/`:

- **Frontmatter:** `name` (matches the folder), `description`,
  `license: MIT-0`, and `compatibility` naming the edition and tools
  ("Elicitly Free or Pro (elicit_display) …" or "Requires Elicitly Pro
  (elicit_approval, …)") plus any origin to allow.
- **Templates** (`*.liquid`) and **sample data** (`*.json`) live in
  `assets/`, and `SKILL.md` tells the agent to pass them verbatim. Keep
  layout out of the model's hands.
- **Pro review tools** follow one loop: create → give the user `reviewUrl`
  → `elicit_await` until not `pending` → `elicit_result` → act on
  `decision`. Never act on a chat claim of approval.
- **Dialogs** (`elicit_confirm`, `elicit_form`) handle all three outcomes:
  yes, an explicit no, and no answer (`null` / `error`). No answer never
  means yes.

## Rules

- **Demos only.** Every description starts "Elicitly demo". A demo with
  made-up business data says so ("Elicitly demo (sample data, …)") and ends
  "Use only when the user asks for … the <name> demo", naming its sample
  entity (Brightwater, Harbor, Larkspur): it must never trigger on a
  real-world request and answer it with sample data. (Jupiter, with real
  public facts, may trigger more broadly.) Each `SKILL.md` keeps
  the **Demo** note under its heading, and the step that would act says
  "In a real skill, … would happen here."
- **Made-up business data.** Invent companies, people and figures; never
  use real customers or real people's names. Images committed here must be
  openly licensed and credited on the card. The salespeople photos are
  licensed stock that stays hosted on www.elicitly.ai, not committed here.
- **Keep the README in sync.** A new or renamed skill updates the demos
  table (Demo, Tools, Edition, Try saying). Free demos first, and the "Try
  saying" prompt must match the description's trigger.
- **Accessibility (rendered output).** WCAG 2.2 AA: text ≥ 4.5:1 contrast,
  images with `alt`, keyboard-reachable scrolling regions, and
  `motion-reduce:` variants for any animation.
- **Review-page templates** (`displayTemplate`, `rowTemplate`, …) use plain
  HTML and a `<style>` block; give links `target="_blank"`. Display
  templates may load DaisyUI and Tailwind from jsDelivr.
- **Conventional Commits** (`feat:`, `fix:`, `docs:`, …).
- **Never commit or push without explicit user approval.** Show the diff
  first.

## Checking a change

- Every `assets/*.json` parses.
- Every template renders with [LiquidJS](https://liquidjs.com/) against its
  sample data, with `jsTruthy: true` and `outputEscape: "escape"`, which
  Elicitly uses.
- Run the skill once in a host: a display in one that renders MCP Apps, a
  dialog in one that renders form elicitation (see the
  [Support Matrix](https://www.elicitly.ai/docs/elicitation/support-matrix/)),
  and Pro skills against the hosted server.
