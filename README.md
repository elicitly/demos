# Elicitly demos

Agent Skills that demonstrate [Elicitly](https://www.elicitly.ai): rich
displays inline in chat, and human decisions an agent can't fake. Each skill
uses fixed sample data, so it behaves the same every time you run it. Copy
them, change them, and make them yours.

> [!IMPORTANT]
> These are demos, not integrations. Every skill reads made-up sample data
> from its `assets/` folder, connects to no real system, and changes
> nothing: "approving" the renewal sends no quote, and "shipping" the
> release deploys nothing. They're a reference for using Elicitly. To use one
> for real, replace the sample data with a query against your own system and
> the "In a real skill…" step with the real action.

## The demos

Free demos run on the open-source [Free Edition](https://github.com/elicitly/elicitly)
(`npx -y elicitly`) or on Pro. Pro demos need the hosted
[Pro Edition](https://www.elicitly.ai/docs/pro/install/).

| Demo | Tools | Edition | Try saying |
| --- | --- | --- | --- |
| [salespeople-leaderboard](skills/salespeople-leaderboard/) | `elicit_display` | Free | "Show the demo sales leaderboard." |
| [jupiter-moons](skills/jupiter-moons/) | `elicit_display` | Free | "Show me the Jupiter moons demo." |
| [release-go-no-go](skills/release-go-no-go/) | `elicit_display`, `elicit_confirm` | Free | "Ship the Brightwater Portal demo release." |
| [rollout-settings](skills/rollout-settings/) | `elicit_form` | Free | "Set up the Brightwater Portal demo rollout." |
| [renewal-approval](skills/renewal-approval/) | `elicit_approval` | Pro | "Send the Harbor & Pine demo renewal for approval." |
| [account-enrichment](skills/account-enrichment/) | `elicit_proposal` | Pro | "Enrich the Larkspur Robotics demo account." |
| [which-account](skills/which-account/) | `elicit_selection` | Pro | "Log call notes for Harbor in the demo." |

One more needs no skill at all. Ask your agent: "Run elicit_doctor with
probeElicitation true and tell me what this host supports." It reports
whether your host can show Elicitly's dialogs and displays.

## Set up

1. **Connect Elicitly to your host.**
   - Free: `claude mcp add elicitly -- npx -y elicitly`, or see the
     [Free Edition README](https://github.com/elicitly/elicitly#quick-start)
     for other hosts and the one-click Claude Desktop extension.
   - Pro: add `https://mcp.elicitly.ai/mcp` as a remote MCP server; see
     [Install Pro](https://www.elicitly.ai/docs/pro/install/).
2. **Install the skills.** Copy the folders under `skills/` into your host's
   skills directory (for Claude Code, `~/.claude/skills/` or your project's
   `.claude/skills/`), or upload a skill folder as a ZIP in hosts that take
   uploads.
3. **Allow image origins** for the two display demos with photos:
   `https://www.elicitly.ai` (salespeople) and `https://upload.wikimedia.org`
   (Jupiter). On Free, set
   `ELICITLY_DISPLAY_RESOURCE_DOMAINS=https://www.elicitly.ai,https://upload.wikimedia.org`
   in the server's environment (in the Claude Desktop extension, that's the
   **elicit_display: extra allowed origins** setting). On Pro, add them to
   your organization's allowed origins in the dashboard.

## Which host?

Displays need a host that renders [MCP Apps](https://modelcontextprotocol.io/extensions/apps/overview);
dialogs (`elicit_confirm`, `elicit_form`) need one that renders form
elicitation. Support varies by host, version and even transport. The
[Elicitation Support Matrix](https://www.elicitly.ai/docs/elicitation/support-matrix/)
tracks what works where. Pro review pages work everywhere: the agent gives you
a link.

## How the skills are built

Each skill is a folder with a `SKILL.md` and an `assets/` folder:

- the template (`*.liquid`), passed to Elicitly verbatim, so the layout never
  depends on what the model improvises;
- the sample data (`*.json`), standing in for a CRM, CI system or ERP.

Each skill's description is scoped to its demo ("Use only when the user asks
for the demo…"), so an installed demo shouldn't pick up a real question and
answer it with sample data. To adapt one, swap the JSON for a real query, keep the
template, and rewrite the description for your real use case. See the
[template rules](https://www.elicitly.ai/docs/templates/) and the
[tool reference](https://www.elicitly.ai/docs/tools/).

All companies, people and figures in the sample data are made up. The
salespeople photos are hosted on elicitly.ai for these demos and aren't part
of this repository; the Jupiter images are credited on each card.

## License

[MIT-0](LICENSE): use, copy and modify these demos without attribution.
Elicitly is a product of Preneur LLC. The license covers the demo content
only; it grants no rights to the Elicitly name or logo.
