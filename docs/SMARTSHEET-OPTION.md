# Option: Building This on Smartsheet Instead

A note for the presentation — worth raising as a live option, not a decision. Since the company already runs Smartsheet, it could carry a real chunk of this without new custom software at all. Here's an honest look at what would transfer and what wouldn't.

## What Smartsheet could replace outright

| Piece | Custom app (what's built now) | Smartsheet equivalent |
|---|---|---|
| Tech intake form | `app/index.html` | **Smartsheet Forms** — same guided fields, conditional show/hide (e.g. hide Asset when Third-party), and native file-attachment support, so photo capture works out of the box. |
| FM approve/deny/forward | The visual prototype (`app/fm-review-demo.html`) | **Smartsheet Approval Requests / Automations** — Smartsheet already has a built-in "request an approval" workflow that can trigger on a new row and route by conditions like NTE amount. |
| Monthly/yearly tallies | Dropped earlier for lack of a database | **Smartsheet Reports and Dashboards** — this is what Smartsheet is actually built for. A live tally by technician, by month or year, with no database or backend to stand up. |

## What stays a gap either way

- **One-click Corrigo work order creation** needs the same thing regardless of platform: OAuth API credentials from Corrigo's admin. Smartsheet's automation engine (or its Bridge/Zapier-style connectors) could be the piece that calls Corrigo's API instead of a custom backend — but the credential requirement doesn't go away.
- **The $499 threshold, third-party-vs-internal branching, and the tech-recommends-FM-decides framing** are process rules, not app features — they'd need to be rebuilt as Smartsheet form logic and automation rules. That's real setup work, just no-code instead of code.

## The actual trade-off

- **Smartsheet:** faster to stand up, no code to maintain, dashboards and approvals come free, and staff may already know the interface. Costs: typically a paid seat per person who needs to approve or edit (not just view), less control over the exact experience, and the approval/automation logic lives inside Smartsheet's rules engine rather than something we can freely customize.
- **Custom app (current):** free to run (static site), fully tailored to this exact workflow, but it's bespoke software someone has to maintain, and anything beyond the intake form (real approvals, real tallies) needs the backend work already discussed.

## Bottom line for the deck

The valuable part of this project isn't really the HTML — it's the process itself: the $499 line, techs recommending rather than deciding, photos as evidence, one form instead of a live consultation. That logic is portable. Where it actually lives — a custom page or a Smartsheet form — is a separate, later decision, and doesn't need to be settled to demo the idea.
