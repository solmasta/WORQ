# WORQ

BMO | JLL MTS Work Order Request (WORQ) process documentation.

See [docs/WORQ-PROCESS.md](docs/WORQ-PROCESS.md) for the full process flowchart, the WORQ email template, job classification rules, and the $499 NTE hard-stop policy.

## WORQ Intake app

[`app/index.html`](app/index.html) is a static, no-backend intake form that replaces free-typing the WORQ email. Techs fill in dropdowns and fields in the same order as the template; the page assembles the exact `crewos@bmo.com` email body, flags jobs over the $499 NTE until the FM heads-up is marked, and lets the tech copy the email or open it directly in their mail app.

It's a single static file with no build step or server. To try it locally, open `app/index.html` in a browser.

**Live for techs:** `https://solmasta.github.io/WORQ/` — that's the link to bookmark on a phone. The root page immediately redirects to [`app/`](app/index.html), which is the actual tool. GitHub Pages here is set to "deploy from a branch" (the repo's default, not something this repo's files control), which rebuilds on every push to `main` automatically — no separate deploy step is needed.

**Embedding in Corrigo:** see [docs/CORRIGO-INTEGRATION.md](docs/CORRIGO-INTEGRATION.md) for a handoff summary — what the tool is, what it needs (nothing), and what's left to decide on the Corrigo side.
