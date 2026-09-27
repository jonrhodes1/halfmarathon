# Lisbon Half Marathon Coach

A calm, precise training dashboard for a sub-2-hour Lisbon Half Marathon (Sunday 7 March 2027). Built as a single self-contained web app — no build step, no account, nothing to install to try it.

## Files

- `index.html` — the whole app (UI, logic, seeded plan). This is the one you open.
- `manifest.json`, `sw.js`, `icon-*.png` — PWA install support.

## Opening it

Double-click `index.html`, or drag it into any browser tab. Everything works immediately — the full 23-week programme is pre-loaded for both Katie and Jon, and all logged data is saved to that browser's local storage (nothing leaves your device).

## The dashboard

The whole app is one scrollable page, topped with the official EDP Maratona de Lisboa banner. Katie and Jon follow the exact same 23-week programme (same sessions, same dates, same targets), tracked independently since you won't always complete a session on the same day. The page shows:

- **Hero stats** — days to Lisbon, combined miles this week, combined sessions done, longest run so far, and average readiness across both of you.
- **A head-to-head comparison** — a bar chart of this week's completion, and a two-line mileage-trend chart, Katie vs. Jon.
- **Katie's column and Jon's column, side by side** — each headed by their own photo, with a race-readiness score, this week's ring, mini stats, and an "up next" card for their next session. Tap the circle on a row to mark it done in one tap (it banks the planned distance/duration automatically); tap the row to open full detail and log actual pace, HR, RPE, or how it felt.

Everything else — the full 23-week plan, progress charts, readiness/benchmarks/log, and profile/settings — opens as an overlay from the "View full plan" button or the settings icon in the top bar, with a Katie/Jon switcher inside, so it never interrupts the single scrolling page.

## Installing as an app (PWA)

Browsers only allow "install as app" / offline caching for pages served over `http(s)`, not for files opened directly (`file://`). To get the installable version on your phone:

1. Put this whole folder somewhere it can be served over https — the easiest free options are [Netlify Drop](https://app.netlify.com/drop) (drag the folder in) or GitHub Pages.
2. Open the hosted link on your iPhone/iPad in Safari, or Android in Chrome.
3. Use "Add to Home Screen" (iOS Safari) or the install prompt (Android Chrome).

Once installed it opens full-screen, works offline for the plan and logging, and behaves like a native app.

If you just want to use it in a browser tab, none of this is necessary — skip straight to opening `index.html`.

## Data & backup

- All data lives in your browser's local storage, scoped per athlete (Katie / Jon).
- **Profile → Export backup** downloads a full JSON snapshot (plan, logs, benchmarks). Keep this somewhere safe — clearing browser data or switching devices will otherwise lose your history.
- **Profile → Restore from backup** re-imports that JSON on any device/browser.
- Nothing is sent to a server. There is no backend.

## What's real vs. what's scaffolded

Built and working: the full seeded plan for both athletes, the single-scroll dual-athlete dashboard with real photo avatars and one-tap complete, drag-free "tap to move" scheduling with recovery-conflict warnings, workout + strength logging, progress rings, mileage/long-run/pace/RPE charts, a consistency heatmap, race readiness, 5K benchmark recalibration, weekly reviews, race day pacing + checklist, multi-athlete profiles, JSON export/import, and a print-friendly race week view.

Deliberately not built yet (and clearly marked "Coming soon" in Profile rather than faked): Garmin, Strava and Apple Health file import. All logging here is manual by design — everything is entered and ticked off inside the app itself. The storage layer is written as a small repository abstraction (`AthleteRepository`, `WorkoutRepository`, …) specifically so a real backend or a future import path could replace or extend local storage later without touching the UI.
