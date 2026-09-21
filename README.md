# WORQ

BMO | JLL MTS Work Order Request (WORQ) process documentation.

See [docs/WORQ-PROCESS.md](docs/WORQ-PROCESS.md) for the full process flowchart, the WORQ email template, job classification rules, and the $499 NTE hard-stop policy.

**New here? Start with [docs/WHY-THIS-WORKS-BETTER.md](docs/WHY-THIS-WORKS-BETTER.md)** — a plain-language comparison of the original process (the client's v2 starting point) against what's here now, and why. No jargon.

## WORQ Intake app

[`app/index.html`](app/index.html) is a static, no-backend intake form that replaces free-typing the WORQ email. Techs fill in dropdowns and fields in the same order as the template, attach and caption photos of the issue, and the page assembles the exact `crewos@bmo.com` email body — flagging jobs over the $499 NTE for FM review — ready to copy or open directly in their mail app.

It's a single static file with no build step or server. To try it locally, open `app/index.html` in a browser.

**Live for techs:** `https://solmasta.github.io/WORQ/` — that's the link to bookmark on a phone. The root page immediately redirects to [`app/`](app/index.html), which is the actual tool. GitHub Pages here is set to "deploy from a branch" (the repo's default, not something this repo's files control), which rebuilds on every push to `main` automatically — no separate deploy step is needed.

**Embedding in Corrigo:** see [docs/CORRIGO-INTEGRATION.md](docs/CORRIGO-INTEGRATION.md) for a handoff summary — what the tool is, what it needs (nothing), and what's left to decide on the Corrigo side.

## FM Review Queue (visual reference)

[`app/fm-review-demo.html`](app/fm-review-demo.html) — live at `https://solmasta.github.io/WORQ/fm-review-demo.html` — is a static mockup of the FM side: approve, deny, or forward a WORQ request for additional approval, with one-click Corrigo creation proposed for plain internal repairs (anything involving a vendor or a capital/operating call stays manual). Nothing on the page is interactive — it's built as source material for the slide deck and video, not a working tool. Individual state screenshots live in [`docs/assets/fm-review-states/`](docs/assets/fm-review-states/). See [docs/CORRIGO-INTEGRATION.md](docs/CORRIGO-INTEGRATION.md#the-other-end-fm-review-and-one-click-corrigo-creation) for what real API access this would need to become a working tool.

## Platform option: Smartsheet

Since the company already runs Smartsheet, it's worth raising as an alternative delivery platform — not a decision, just an option for the presentation. See [docs/SMARTSHEET-OPTION.md](docs/SMARTSHEET-OPTION.md) for what it could replace (forms, approvals, tallies come largely free) versus what stays a gap either way (Corrigo API access, and rebuilding the process rules as form logic).
