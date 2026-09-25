# 07 · The final review, then a pest on its own base

## The asks (Caryn, 2026-09-25 evening)

> lets do a final in depth review checking for errors, issues, usability and
> any simple improvements that could be made before we consider this project done

then, on hearing that per-pest base temperatures had been editable but unread:

> how easily can we add the per pest bases feature? i believe it would be
> useful so if we can add it today i'd like to

## The review

Screenshots of every screen at phone and desktop width were read first; the
usability changes were small (Now's "Later" list folds, pest rows stay
collapsed until tapped, Settings moved up under Locations) and two hardening
items were added (share links have size caps and refuse a deflate bomb;
calendar lines fold by UTF-8 octets so accented names stay valid).

A separate correctness review of the whole folder then found ten real defects
that ten green browser probes could not see, because each only bites over
days, on a second device, or after a setting changes: the seed JSON was
git-ignored by a repo-root rule; "today" froze on the day the tab opened; a
restore never restored settings; per-pest base/upper were editable but nothing
read them; a station never back-filled when the biofix moved earlier; NWS
observations were cut by the API's 500-record cap; switching a source off left
its forecast rows; a typed biofix like `3-1` silently zeroed the season; two
records made in one millisecond shared an id; calendar files went through the
phone share sheet against the code's own comment. All ten are fixed and
tested. The lesson worth keeping: a probe checks what you thought to probe; a
review reads for what the code promises and does not do.

## Per-pest bases

The engine already took a base and an upper cutoff per call, so the work was
in what reads the one accumulation:

- `methodOf(pest)` in `weather/dd.js`: the pest's own base / cutoff, or the
  guide's 50 / 95 °F; `upper: null` means no cutoff. `pestStatus`,
  `seasonStatus` and `eventDates` take an `accumOf(pest)` resolver, so each
  pest is read against the accumulation under ITS method. Bases are never
  mixed.
- `accumsFor(loc, settings, today, pests)` in `useDdLog`: one accumulation per
  distinct method among the visible pests (150 pests on one base is still one
  accumulation), `main` being the guide's.
- Now: the headline stays the guide's total; each other base gets its own line
  under it; a pest on its own base wears a 🌡 chip. Season: a dotted line in
  the location's colour with a label, events dated from the pest's own curve.
  Pests: the chip on the row; the editor's base / cutoff fields are back, typed
  in the user's unit (°C shows 4.4 for 40 °F and an untouched field keeps the
  stored value exactly — the probe caught 40 → 39.9). Calendar files say
  "(base 40°F)" in the description.
- Tests: engine 51 (base 40 vs 50, no cutoff, methodOf, the same threshold
  active on one base and coming on the other, event dates per pest), ics 15.
  Probe `probes/bases.mjs` adds a base-40 pest on the sample farm and reads
  every screen.
