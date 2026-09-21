# WORQ: Closing the Gap — NotebookLM Briefing

This is the single source to upload to NotebookLM first (or paste as one document) for generating the slide deck / video. It carries the whole story in order — problem, solution, proof, what's next — so the generated narration doesn't default to a generic explainer tone. Add the other repo docs (`WORQ-PROCESS.md`, `CORRIGO-INTEGRATION.md`, `SMARTSHEET-OPTION.md`) as supporting sources after this one.

**Audience:** corporate presentation, likely presented live on a Teams call. **Tone:** plain language — avoid technical terms (API, backend, database) unless directly explaining a limitation. **Goal:** show that a real communication gap between technicians and facility managers has been identified and closed, with working proof, not just a proposal.

**There's already a live, animated deck built for exactly this call:** [`docs/presentation.html`](presentation.html) (open in a browser, live at `https://solmasta.github.io/WORQ/docs/presentation.html`). Eight slides, click or arrow keys to advance, built to be screen-shared directly — no need to export to PowerPoint first. It covers the same eight sections below in the same order. Use NotebookLM for a narrated video version if you want one; use this deck directly if you're presenting live.

---

## 1. Executive summary

BMO and JLL MTS technicians request work through a shared system (WORQ, emailed to `crewos@bmo.com`). The original process required a live consultation with the Facility Manager before *any* request — no matter how small — could proceed. This project replaces that bottleneck with a structured intake process that gets small jobs moving instantly, gives FMs everything they need to decide quickly on the rest, and proposes a clear path to close the loop with Corrigo, the work order system of record. Nothing about FM authority or financial accountability changes — what disappears is the waiting.

## 2. The problem: what the client started with

The original procedure (v2, see `docs/assets/worq-process-flowchart-v2-original.png`) was a strict four-step gate:

1. JLL MTS issues a WORQ — area of concern identified.
2. FM Consultation — determine if it may qualify as Unplanned Capital.
3. Cost Validation — FM reviews and validates labor & material costs.
4. **"DO NOT PROCEED"** — await FM validation, OPEX funding review, and capital tracking determination.

Its own executive guidance stated: *"All WORQ requests must be reviewed with the Facility Manager prior to authorization or execution."* No exceptions for size or urgency. Every job — a $40 part or a major system failure — went through the same live-consultation gate.

**Why that's a real gap, not just red tape:** it slows down obviously routine work, pulls FMs into a conversation for every single request, and relies entirely on a verbal or written description — no photos, no consistent structure, easy for details to get lost between tech and FM.

## 3. What changed

- **A clear dollar line: $499.** Routine jobs at or under that amount go straight through. Only requests that actually need a decision reach the FM for review.
- **One structured form instead of a live consultation.** The tech fills in location, cost, condition, and what's needed once, in order — matching the same fields FMS already uses to create a work order.
- **Photos, captioned by the tech.** The FM sees the actual problem instead of just reading about it. Each photo can be downloaded with its caption burned directly into the image, so it stays self-explanatory even once attached to an email or work order.
- **Techs recommend, FMs decide — made explicit.** Vendor choice, repair-vs-replace, and capital classification are labeled in the form and the resulting email as the tech's recommendation. The FM still confirms all of it. This preserves the original process's accountability goal; it just records it clearly instead of requiring a live check-in to establish it.
- **A proposed one-click path for the easy cases.** For a plain internal repair with no vendor and no capital-vs-operating judgment call, approving it could also create the Corrigo work order directly — no re-typing. Anything involving a vendor or a capital decision still comes to the FM as a manual call, matching how much judgment that case actually needs.

## 4. What exists today (with screenshots)

Two real, working pieces and one visual concept:

### A. WORQ Intake (technicians) — a real, live tool
A guided web form technicians use instead of composing the WORQ email from memory. Screenshot: `docs/assets/presentation/slide-tech-tool.png`. Live at `https://solmasta.github.io/WORQ/`.
- Dropdown fields in the same order as the WORQ template (location, FM, priority, description, cost, asset, condition, capital type).
- Hides irrelevant fields automatically (e.g. no asset field needed for a third-party vendor call).
- Photo capture and captioning, described above.
- Produces the exact, correctly formatted email body — the tech copies it or opens it directly in their mail app. Nothing is sent automatically.

### B. FM Review Queue — a visual concept, not yet built
Shows what the FM's side could look like: a queue of incoming requests with Approve / Deny / Forward-to-leadership options, and one-click Corrigo creation for the simple cases. Screenshot: `docs/assets/presentation/slide-fm-queue.png`. This is a static mockup (nothing is clickable) — built specifically as source material for this presentation, not a working system yet.

### C. Before/After comparison
The clearest single visual for explaining "why this is better." Screenshot: `docs/assets/presentation/slide-before-after.png`.

## 5. What stays exactly the same

Say this clearly and early when presenting — it's the reassurance that makes the change land as safe rather than risky:

- The FM still has final say on funding, vendor choice, and capital-vs-operating classification.
- Nothing gets spent past the approved amount without the FM's OK — that hard stop is exactly as strict as it was.
- Every job is still tracked and classified before it's closed out.

## 6. What's next (be honest about this — it's not finished)

- **Embedding the tech tool's link inside Corrigo** — a decision for whoever administers Corrigo; documented in `docs/CORRIGO-INTEGRATION.md`.
- **Real one-click work order creation** needs OAuth API credentials from the Corrigo admin. Until then, the one-click concept is a proposal, not a built feature.
- **Notifying the tech of a decision (approved/denied/forwarded) should go through Corrigo's own Alerts/Notifications system** (and CruChats for the contractor/vendor side) rather than building a separate notification system — one place for a tech to check, not two.
- **Smartsheet is a live alternative worth naming**, since the company already uses it — its Forms, Approval Automations, and Dashboards could cover much of the intake, approval, and tally-reporting pieces natively. Documented with honest trade-offs in `docs/SMARTSHEET-OPTION.md`.

## 7. Suggested narrative order for the deck/video

1. Open on the original process's own words — "DO NOT PROCEED." Let it feel real before explaining anything.
2. State the goal in one sentence: close the communication gap between techs and FMs.
3. Show what changed (Section 3 above), leaning on the before/after visual.
4. Show the actual tool — this is proof, not a pitch. Walk through the tech filling out a request, including a photo.
5. Show the FM side concept — how a request gets decided, and the one-click idea for easy cases.
6. Reassure: what doesn't change (Section 5).
7. Close honestly on what's next (Section 6) — Corrigo access needed, Smartsheet as an option worth a conversation.

## 8. Slide index

The live deck (`docs/presentation.html`) has 8 slides, animated and click-through. Flat PNG exports of each — for dropping into NotebookLM, a Word doc, or an email — are in `docs/assets/presentation/`:

| File | Shows |
|---|---|
| `slide-1-title.png` | Title card for the opener |
| `slide-2-problem.png` | The original process's "DO NOT PROCEED," in its own words |
| `slide-3-what-changed.png` | Three before/after contrasts, plus the $499 line |
| `slide-4-tech-tool.png` | The WORQ Intake form, phone-framed, with callouts |
| `slide-5-photos.png` | The photo + caption feature, phone-framed, with callouts |
| `slide-6-fm-review.png` | Pending request → approved-and-created-in-Corrigo, side by side |
| `slide-7-whats-next.png` | Three honest next steps: Corrigo API access, Corrigo's own alerts, Smartsheet option |
| `slide-8-closing.png` | The reassurance close: what stays the same |

Higher-resolution / more detailed screenshots (individual form fields, individual FM queue states) are in `docs/assets/fm-review-states/` and `docs/assets/` if more detail is needed for a follow-up document rather than the live presentation.
