# Erun — Errands, Handled.

A vetted, professional errand-running marketplace. This repo contains a working,
tap-through preview of the Customer and Runner apps — one static, installable web
app (no build step) that mirrors the real product flows described in the product
spec: category selection, live tracking, the single-use Erun wallet card, runner
feed/calendar/earnings, and more.

## View it

Once GitHub Pages is switched on for this repo (see below), the app is live at:

```
https://lucascpcnblt.github.io/APPERRUND/
```

- **On desktop** it shows inside a phone-frame mockup with a Customer/Runner
  switch, for demos and investor walkthroughs.
- **On an actual phone** the frame disappears and it fills the screen like a
  real installed app.

## Using it offline on your phone

This is a PWA (Progressive Web App) — install it once and it keeps working
without a connection:

1. Open the link above in **Safari** (iPhone) or **Chrome** (Android).
2. **iPhone:** tap the Share icon → **Add to Home Screen**.
   **Android:** tap the menu (⋮) → **Install app** (or use the "Add to home
   screen" prompt that appears in the app itself).
3. Open it from your home screen icon from now on — after the first load it
   works with no signal, on a plane, in a basement car park, anywhere.

## How the live link is published

Every push to `main` runs `.github/workflows/pages.yml`, which publishes the
repo to GitHub Pages. The workflow calls `actions/configure-pages` with
`enablement: true`, so it switches Pages on by itself the first time it runs —
there is no manual **Settings → Pages** step. After that, every push to `main`
redeploys the live link within about a minute; nothing is uploaded by hand.

The repo must be **public** for Pages to serve on a free GitHub plan.

If a deploy ever fails at the "Deploy to GitHub Pages" step, check
**Settings → Pages → Build and deployment → Source** reads **GitHub Actions**.

## Project structure

```
index.html       — the entire app (markup, styles, and interaction logic)
manifest.webmanifest — PWA metadata (name, icons, colors, install behaviour)
sw.js             — service worker: caches the app shell so it works offline
icons/            — the Erun logo (erun-logo.png) + generated app/home-screen icons
.github/workflows/pages.yml — auto-deploy to GitHub Pages on push to main
```

## Design notes

- **Typefaces:** Sora (headings/brand), Inter (body), IBM Plex Mono
  (data — prices, receipts, card numbers) — chosen for a trustworthy,
  fintech-grade feel rather than a casual gig-app look.
- **Palette:** deep navy as the primary trust colour, muted gold reserved for
  Tier 2 / premium signals, green for success/verification states.
- **Logo:** the real Erun mark is the only logo used anywhere in the app. On the
  splash screen it pops in, a single light sweep travels across it (masked
  exactly to the glyph's own pixels), and its accent dot pulses like a live
  runner ping — then it settles into a calm, static mark in-app so day-to-day
  use stays composed rather than flashy.
- Screens follow the customer and runner flows in the product spec: booking →
  finding a runner → live tracking with an in-app purchase-approval step →
  itemised receipt with the spend-cap/actual/swept-back breakdown → rating;
  and on the runner side: job feed with effective $/hr → job detail with a
  stage-by-stage duration breakdown → the single-use virtual card checkout →
  calendar with travel-buffer warnings → earnings with the launch-bonus
  tracker.
