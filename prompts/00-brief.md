# 00 · The brief

## The ask (the grower, 2026-09-24)

> Something like the Pesticide app's Degree Days tab, but standalone: multiple
> weather sources plus the SprayCast/BlightCast scorecard; preloaded nursery
> pests, all editable, users add their own pests and thresholds; an "active
> now / coming soon" view; crops affected per pest = where to scout; works on
> a phone; Excel export; calendar reminder; share the same data to a coworker
> and update one device from another.

## What was proposed back, and decided

- **A standalone Nuxt app** on the SprayCast recipe (single page, localStorage
  state, static build for GitHub Pages), port 3009 so it runs beside the other
  apps and never near the farm server.
- **A layer-shaped `weather/` folder**: pure modules with no app imports (the
  engine, the source parsers), so the folder can be lifted into a shared
  weather layer later. Decision: layer-shaped now, a real layer only after the
  collaborator's review.
- **The pest data**: the Rutgers Nursery & Landscape Pest Scouting Guide
  (beta 2023, T. Waller), extracted from the PDF into `data/` — 232 pest-stage
  rows, 144 pests — not the Pesticide app's 14-row table. The guide's own
  caveat rides along ("for scouting purposes only"), and its request for
  observation reports is a link in the app.
- **The method**: simple average with a horizontal cutoff (base 50 °F, upper
  95 °F), the method the thresholds were built on. °C is display only.
- **Default weather source**: Open-Meteo, worldwide and account-free. NEWA,
  NWS and a LI-COR token as options.
- **Public repo holds only the built app** (deploy-repo pattern); the source
  stays in the farm's private repo. °F/°C and English/Spanish toggles.

## Why it is worth building at all

The general tools (NEWA's own pages, extension calculators) give you a number.
A grower needs the number turned into "go look at the boxwood in house 5 this
week", from the weather at *their* place, on a phone, for the pests *they*
grow. That last mile is the app.
