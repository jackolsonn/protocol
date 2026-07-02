# Protocol — Daily Health Schedule & Calorie Tracker

A progressive web app (PWA) built from `master_schedule_and_products.pdf`. Runs 100% on-device —
all data lives in the phone's local storage and never leaves it.

## Features
- **Today** — your full daily schedule (per weekday, seeded from the PDF) with tap-to-check items,
  plus live rings for calories, protein, fiber, and water (4L target).
- **Food** — calorie tracker vs. 2,100 cal / 180g protein / 35g fiber. One-tap quick-adds for
  Meal 1, Pre-WO Snack, and Meal 2, custom entries, and a 7-day history.
- **Train** — all workout routines (Push/Pull/Legs/Upper, Swimming, Rugby+Run…). Add, edit, and
  delete routines freely.
- **Plan** — the full weekly schedule editor. Add/edit/delete any item on any day; toggle 🔔 to
  include it in reminder exports.
- **More** — reminder export, editable daily targets, JSON backup, full reset.

## Install on iPhone (one-time)

The app needs to be served over HTTPS once so iOS caches it for offline use. Easiest options:

**Option A — free static host (recommended, ~2 minutes)**
1. Go to https://app.netlify.com/drop (or GitHub Pages, Vercel, etc.).
2. Drag this whole folder onto the page. You get a URL like `https://something.netlify.app`.
3. On the iPhone, open that URL **in Safari**.
4. Tap the Share button → **Add to Home Screen** → Add.
5. Done. Launch it from the home screen icon — it now runs fully offline, on-device.
   The host only delivers the files; your logged data never goes anywhere.

**Option B — same Wi-Fi from this Mac (quick test, not offline)**
```bash
cd "/Users/jackolson/Calorie Tracker" && python3 -m http.server 8741
```
Then visit `http://<this-mac's-IP>:8741` in iPhone Safari. Works for trying it out, but iOS
won't cache it for offline use over plain HTTP — use Option A for the real install.

## iPhone reminders / push notifications

iOS does not let a web app fire scheduled local notifications on its own, and true web push
requires a always-on server. So the app uses the reliable, serverless route:

1. Open **More → "Export reminders to Calendar (.ics)"** on the iPhone.
2. Tap the downloaded file → **Add All** to Calendar.
3. Every 🔔-marked schedule item (wake, meals, caffeine cutoff, workouts, 75 Hard walks,
   eating-window close, sleep…) becomes a repeating weekly Calendar event with a native alert —
   real push notifications, even when the app is closed.

To change what alerts you: toggle 🔔 on items in the **Plan** tab, delete the old "Protocol"
events from Calendar, and re-export.

There are also in-app alerts (More → Enable in-app notifications) that fire while the app is open.

## Files
- `index.html` — the entire app (UI + logic, no dependencies)
- `sw.js` — service worker (offline caching)
- `manifest.webmanifest`, `icon-*.png` — home-screen install metadata
