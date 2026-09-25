# 02 · Step 2 — weather sources and the scorecard

## The ask

> Step 2: the weather sources lifted from SprayCast — Open-Meteo history and
> forecast by coordinates, NEWA, NWS, a LI-COR token (browser-only), CSV —
> and the scorecard.

## What was built

- `weather/sources.js` (pure, 43 tests): Open-Meteo daily rows (forecast API
  for the last 92 days + 14 ahead, the archive back to the biofix), the NEWA
  station list (the worker URL; `id` already carries the network) and hourly
  parser (string values, "M"/"NaN", station-local timestamps read off the
  string, DST repeats), LI-COR device scan and readings on the farm's clock,
  NWS observations and the daily forecast (a night's low belongs to the date
  it ends on), CSV (daily max/min or hourly), `pointsToDaily` (a day counts
  only with 20+ distinct hours, never today), **`mergeRows` — the one
  precedence rule**: typed > file > LI-COR > NEWA > NWS > model; a confirmed
  day beats a forecast; no forecast on or before today.
- `useWeather`: the refresh (model → archive → station incrementally from
  its last complete day → NWS forecast → file → merge), caches per location,
  the LI-COR token in its own localStorage key.
- The scorecard: forecasts are **booked the day they are made** (per source,
  per lead of 1/3/7 days) because the log overwrites a forecast the moment
  the day is confirmed; then graded against confirmed days. Plus model vs
  station over the season.

## Verified

Live node probe against the real services for Bridgeton NJ: 207 archive +
74 recent days, 3,725 DD since 1 January; NEWA Upper Deerfield Township at
2.8 mi, 24 September days; NWS forecast 6 days; model vs station +19 DD over
24 days. Browser probe: search → 268 days → attach NEWA → 267 station days
replace the model's, token never on the location record.

## What went wrong

The composable was "not defined" at server render. Nuxt's export scanner
stops reading a file at an `export const X = {…}` line and never saw the
function below it. Fix: don't export the object. Found by a one-line
headless dump of the page; the unit tests could not see it.
