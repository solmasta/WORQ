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

## The other end: FM review and one-click Corrigo creation

The next piece being designed (not built yet) is the FM side: when a WORQ email lands in the shared inbox, the FM should be able to approve, deny, or forward it for additional approval, and — for plain internal repairs — create the Corrigo work order in one click instead of retyping it.

**Visual reference:** [`app/fm-review-demo.html`](fm-review-demo.html) (live at `https://solmasta.github.io/WORQ/fm-review-demo.html`) shows the intended flow against sample requests. It's a static mockup — nothing is clickable — built as source material for the slide deck and video, not connected to any real inbox or to Corrigo. Individual state screenshots (pending, approved, denied, escalated) are in [`docs/assets/fm-review-states/`](assets/fm-review-states/), ready to drop into slides.

**What real one-click creation needs before it can be built:**

1. **Corrigo API credentials.** Corrigo publishes a REST API (`developer.corrigo.com`) that can create work orders directly. This requires an OAuth client (client ID/secret) issued by your Corrigo admin — without it, "one click" can only mean "opens Corrigo pre-filled," not "creates it automatically."
2. **Scope of what's automated.** Per direction from this project: only a straightforward Internal MTS repair (no vendor, no capital-vs-operating judgment call) is a candidate for one-click creation. Anything involving a third-party vendor or a capital/operating expense classification stays a manual decision for the FM — the prototype reflects this split.
3. **Where the approve/deny/forward queue lives and how it's populated** — e.g. does it read the shared inbox directly (needs Microsoft 365/Google Workspace API access, depending on how `crewos@bmo.com` is hosted), or does the WORQ Intake app submit to a small backend that both feeds this queue and eventually calls Corrigo. Either way this is real infrastructure (a backend + database), not a static page like the intake tool.

## Closing the loop back to the tech: use Corrigo's own alerts, don't build new ones

Corrigo Enterprise already has a documented **Alerts/Notifications** system, and the CorrigoPro contractor portal has **CruChats** — in-app messaging tied directly to the work order, logged there as part of its audit trail, replacing phone/email tag for job coordination. That changes the plan for how a tech finds out their WORQ was approved, denied, or forwarded:

- **Don't build a separate notification path.** Once a work order exists in Corrigo (created via the one-click flow above, or manually), status changes and messages should go through Corrigo's own alerting — the same way a tech already gets notified about any other job. That's one notification system for the tech to watch, not two.
- **CruChats is confirmed for CorrigoPro** (the third-party/vendor-facing portal) specifically. Whether an equivalent exists for internal MTS techs inside core Corrigo Enterprise — not just contractors bidding jobs — is worth confirming with your Corrigo admin. If it's contractor-only, it's still directly relevant to the "Third-party" / Recommended Vendor path in the WORQ form, even if internal repairs rely on the general Alerts/Notifications feature instead.
- **Same dependency as everything else here:** triggering a Corrigo alert or CruChat message programmatically from an approve/deny/forward action still needs the Corrigo API credentials mentioned above. Nothing about this changes the "what do we need first" list — it changes what we build once we have it: route outcomes into Corrigo's own alerts rather than inventing an email or SMS system alongside it.

## Where the source lives

Repo: `solmasta/WORQ`. Tech intake tool at `app/index.html`, FM review prototype at `app/fm-review-demo.html`. GitHub Pages here rebuilds automatically on every push to `main` (repo default "deploy from branch" setting) — the URLs above never change across updates.
