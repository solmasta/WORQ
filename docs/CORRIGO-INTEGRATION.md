# Corrigo Integration Handoff

For whoever configures the Corrigo-side link. This describes what the WORQ Intake tool is and how it behaves — everything needed to decide where and how to surface it in Corrigo, without needing to read the code.

## What it is

A single web page technicians fill out instead of composing the WORQ email from memory. It walks through the same fields FMS uses to create a work order, then produces the exact `crewos@bmo.com` email body, ready to copy and paste into the work order system.

**Live URL:** `https://solmasta.github.io/WORQ/`

## What it needs from Corrigo

Nothing. It's a static page — no login, no API calls, no data sent anywhere. It reads nothing from Corrigo and writes nothing back. That also means:

- It's safe to link to from anywhere in Corrigo without any data-sharing or security review tied to the page itself.
- It can be opened in a new tab/window, or embedded in an iframe/in-app browser — nothing on the page blocks framing.
- No credentials, API keys, or accounts are involved on our side.

## What it produces

A tech fills the form and taps **Copy email** (or **Open in mail app**). Either way, the result is plain text formatted like:

```
WORQ

Location: ...
FM: ...
Priority (Rush, Normal): ...
WO Description: ...
NTE: $...
...
```

That's it — the tech still sends it themselves (paste into an email, or into wherever Corrigo wants it). The tool does not send anything on its own.

## Decisions for the Corrigo team

1. **Where does the link live?** Corrigo Enterprise has a "Customer Portal – Custom Links" admin feature; unclear whether that surface is technician-facing or customer-facing only. If it's customer-facing only, the equivalent for the technician mobile app (a "Quick Action," favorite, or custom button) would need to be found separately.
2. **New tab or embedded?** Either works technically — pick whichever fits Corrigo's UI pattern for other external links.
3. **Longer term:** Corrigo publishes a REST API (`developer.corrigo.com`) that could let this tool create work orders directly instead of producing text to paste. That's a separate, bigger project requiring OAuth credentials from Corrigo admin — worth considering once the email-based version is proven out with techs, not a blocker for linking it in now.

## Where the source lives

Repo: `solmasta/WORQ`, page source at `app/index.html`. Deploys automatically to GitHub Pages on every push to `main` via `.github/workflows/deploy-pages.yml` — the URL above never changes across updates.
