# CipherOutreach — GI Prep Demo

A polished, **single-file HTML** sales-demo tool that simulates a **longitudinal 14-day pre-colonoscopy SMS prep program** as a patient would experience it on their phone.

Built for a live demo with the **CommonSpirit / Virginia Mason Franciscan Health** GI service line. Everything runs in the browser — no build step, no backend, no install.

---

## What it is

The tool renders a single, continuous **iPhone Messages thread** made of dated **touchpoints** spread across ~14 days leading up to a screening colonoscopy — escalating to hourly on procedure day, then post-procedure follow-up. The demo leader navigates between touchpoints live while presenting.

It models the real workflow a GI clinic runs over a split-dose bowel prep:

- **Day -14** — Welcome, procedure confirmation, and medication review (GLP-1s, blood thinners, iron)
- **Day -7** — Prep-kit pickup, medication holds, and confirming a ride/escort for anesthesia
- **Day -3** — Low-fiber / low-residue diet begins
- **Day -2** — Stock up on clear liquids (avoid red/purple dyes)
- **Day -1** — Clear liquids only + first (evening) prep dose
- **Day 0** — Hour-by-hour: second split dose (3 AM), NPO cutoff (5:30 AM), the **clear-liquid stool check** (6:30 AM), and arrival instructions (7:15 AM)
- **Post-procedure** — Same-day recovery check-in and a next-day feedback prompt

The **6:30 AM clear-liquid stool check** is the marquee moment: a patient replying that their prep is *"still a little cloudy"* prompts a nurse callback — the kind of automated triage that prevents same-day turn-aways.

> **Patient-side only, natural free-text replies.** The patient responds by *typing* a natural-language message (conversational AI style) — there are no multiple-choice buttons. The automated messages never give clinical advice. When a concern truly needs a human, the reply says so ("A nurse from our care team will follow up with you shortly"); routine responses simply get a normal reply. There is no "care team notified" banner and no separate care-team dashboard — this is exactly what the *patient* sees.

---

## How to run

**Option A — just open it.** Double-click `index.html` (or drag it into any modern browser). It works fully offline once the CDN assets (Tailwind, Font Awesome, Inter, XLSX) have loaded once.

**Option B — GitHub Pages (shareable link).** In the repo: **Settings → Pages → Build and deployment → Source: `Deploy from a branch` → Branch: `main` / root**. After it publishes, the demo is available at `https://<org>.github.io/<repo>/`.

---

## How to present it

The left panel has three tabs plus a persistent presenter control bar at the bottom.

### 1. Journey tab (the main driver)
A vertical **Care Journey** navigator listing every touchpoint (e.g. *Day -14 · Welcome*, *Day 0 · 6:30 AM · Clear-liquid check*). Touchpoints that trigger a nurse callback are flagged with a ⚠︎.

- **Click any touchpoint** to jump the thread straight there (it reveals everything up to and including that point). Great for hopping to the highlight moments.
- **Advance** (bottom bar, or the pulsing **camera icon** in the phone's message bar) drives everything: tap it to reveal a touchpoint's hospital messages, tap again to have the patient *type out* their scripted reply, then again to move to the next touchpoint.

### 2. Scripted patient replies (typed live)
The conversation path is fully pre-scripted, so nothing is left to chance in the room. When a touchpoint expects a patient response, the camera icon pulses; tap it and the patient's reply **types out** in the message bar and sends — just like a real person texting back. Touchpoints that trigger a nurse callback are flagged with a ⚠︎ in the navigator (a presenter cue only; the patient never sees it).

### 3. Present mode
Click the **expand** button (or the panel's chevron) to hide the sidebar and show the phone full, clean, and centered for the room. A small "Show Panel" button brings the controls back.

### 4. Settings tab
Configure the demo without touching code:
- **Patient first name** (default *Margaret*)
- **Hospital / health system** (default *Virginia Mason Franciscan Health*) — drives the header logo/initials
- **Facility / location**
- **Procedure date** (date picker) — every message's date divider is computed automatically from this
- **Procedure time**

These are inserted anywhere a message uses the tokens `{patient}`, `{hospital}`, `{location}`, `{procdate}`, `{proctime}`.

### 5. Editor tab (secondary)
A lightweight editor to tweak message copy, reply choices, escalation flags, and acknowledgments. You can also:
- **Import** a script from CSV/XLSX
- **Download** a template pre-filled with the current script

**Template columns:** `Touchpoint ID, Day Offset, Time, Label, Bot Message, Choice Text, Choice Next, Escalate, Ack`

---

## Suggested live demo flow (~3 minutes)

1. Open on **Day -14** — show the warm welcome + the medication-review question, then Advance so the patient types *"Yes, I take Ozempic once a week."* The reply promises a nurse follow-up — the GLP-1 catch that prevents day-of turn-aways.
2. Jump through **Day -7 → Day -1** — show the escalating cadence (prep kit + ride, low-fiber diet, clear liquids, first prep dose), including the tappable education links pushed at each stage.
3. Jump to **Day 0 · 6:30 AM · Clear-liquid check** — the headline. Advance so the patient types *"Not quite, it's still a little cloudy with some bits."* The message holds them from coming in and promises an immediate nurse call — the same-day save.
4. Continue to **Arrival → Recovery → Next-day feedback** — show the up-to-the-hour hand-holding and post-procedure follow-up.
5. Hit **Present mode** at any point to show the clean phone to the room.

---

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The GI Prep demo tool (the thing to present). |
| `legacy-demo.html` | The original generic Demo Builder, preserved for reference. |
| `README.md` | This file. |

---

## Tech notes

- Plain HTML + [Tailwind (CDN)](https://cdn.tailwindcss.com), Font Awesome (CDN), Google Fonts (Inter), and the XLSX CDN for the optional import feature. No build step.
- State (script + settings) is saved to `localStorage`, so edits persist across reloads. Use **Reset** (Editor tab) to restore the default CommonSpirit GI script.
- Degrades gracefully offline after the CDNs have loaded once; no console errors in normal use.
