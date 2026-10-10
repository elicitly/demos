---
name: jupiter-moons
description: Elicitly demo: show Jupiter and its four Galilean moons as a swipeable card carousel with images, facts and Wikipedia links. Use when the user asks for the Jupiter moons demo or a visual tour of Jupiter's moons.
license: MIT-0
compatibility: Elicitly Free or Pro (elicit_display) in a host that renders MCP Apps. Images load from https://upload.wikimedia.org, which must be an allowed origin.
---

# Jupiter's moons

> **Demo.** Shows sample data from `assets/`. Adapt the template and data to your own use case.

A light, visual `elicit_display` demo: a planet header and a carousel of
moon cards, each with an image, a fact, and a link to read more.

## Steps

1. Read `assets/moons.json`.
2. Call `elicit_display` with:
   - `template`: the contents of `assets/carousel.liquid`, verbatim
   - `context`: the whole object from `assets/moons.json`
   - `summary`: "Jupiter and its four Galilean moons — Io, Europa, Ganymede
     and Callisto — with size, orbit and a link to each on Wikipedia."
   - no `title`: the template has its own heading
3. If the result says the host can't render MCP Apps, list the four moons
   with one fact each. Otherwise, invite the user to swipe through the cards
   and stop there.

## Notes

- Images come from `https://upload.wikimedia.org`. If the result reports it
  as a blocked origin, tell the user how to allow it: Free, set
  `ELICITLY_DISPLAY_RESOURCE_DOMAINS=https://upload.wikimedia.org`; Pro, add
  it to the organization's allowed origins.
- Each card shows its image credit; keep `credit` with any image you swap in.
