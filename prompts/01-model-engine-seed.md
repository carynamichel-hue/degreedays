# 01 · Step 1 — model, engine, seed, first screens

## The ask

> Build step 1: the pest model, the degree-day engine, the Rutgers seed, the
> status lists, locations, pasted temperatures, and tests — then verify it
> renders.

## What was built

- `weather/dd.js`: `dayDD(high, low)`, `accumulate(rows, {biofix, today})`
  → confirmed / forecast / missing / gaps, `rateFrom` (mean of the forecast
  days, else the last 7 confirmed), `eventState` (coming → active → passed;
  an open-ended stage stays active for 300 DD), `pestStatus`, `seasonStatus`,
  `parseTempLines` (pasted "date high low" in any common format).
- `data/rutgers_gdd_2023.json` + `app/utils/seed.js`: the guide's rows
  grouped into pests with ordered events, every row keeping its reference.
- Composables on the SprayCast pattern: `useLocalState` (SSR-safe, persists
  through a detached effect scope), `useLocations` (Open-Meteo geocoder
  search with the state peeled off the query), `usePests`, `useDdLog`,
  `useSettings` (units, language, biofix, "coming soon" distance).
- Three tabs: 📊 Now, 🐛 Pests (list + editor), ⚙ Setup. `?sample=1` adds a
  synthetic farm so the page can be tried with no weather at all.

## Verified

`npm test` — engine 33, seed 13. Rendered headless at 1100 px and 390 px
with the sample farm; late September → 143 passed, 1 active (fall webworm),
which is what the season should say.

## What to notice

- The engine works in °F throughout because every published threshold is in
  °F degree-days. A degree-day converts to °C by ×5/9 with no offset — the
  test pins that, because it is the kind of thing that gets "fixed" wrong.
- The status test `beyond the DD window but within 14 days → coming` is there
  because the two limits are an OR, and a later edit could quietly make them
  an AND.
