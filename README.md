# WORQ

BMO | JLL MTS Work Order Request (WORQ) process documentation.

See [docs/WORQ-PROCESS.md](docs/WORQ-PROCESS.md) for the full process flowchart, the WORQ email template, job classification rules, and the $499 NTE hard-stop policy.

## WORQ Intake app

[`app/index.html`](app/index.html) is a static, no-backend intake form that replaces free-typing the WORQ email. Techs fill in dropdowns and fields in the same order as the template; the page assembles the exact `crewos@bmo.com` email body, flags jobs over the $499 NTE until the FM heads-up is marked, and lets the tech copy the email or open it directly in their mail app.

It's a single static file with no build step or server. To try it locally, open `app/index.html` in a browser. To host it for the team, enable GitHub Pages on this repo (Settings → Pages → deploy from a branch → `/app` or root) and share the resulting link — or drop the file into any static host.
