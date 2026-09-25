# How this app was built — the prompts

Degree Days was built in one day (2026-09-25) as the first worked example for
a workshop on building your own nursery tools with an AI coding assistant
(Claude Code). This folder is the part of the build you cannot see in the
code: **what was asked, in the words it was asked in**, and what came back.

Read it in order. Each file is one step or one review round: the ask, the
decisions taken, what was built, and what went wrong on the way (the
interesting part). The commit history of the source repo carries the code.

| File | What it covers |
|---|---|
| [00-brief.md](00-brief.md) | The original brief and the decisions taken before any code |
| [01-model-engine-seed.md](01-model-engine-seed.md) | Step 1: the pest model, the degree-day engine, the Rutgers seed, the first screens |
| [02-weather-sources.md](02-weather-sources.md) | Step 2: Open-Meteo, NEWA, NWS, LI-COR, CSV, the precedence rule, the scorecard |
| [03-review-rounds.md](03-review-rounds.md) | Six review rounds with the grower, ask by ask |
| [04-backup-share-excel.md](04-backup-share-excel.md) | Backup, restore, share links with a QR code, Excel, the token rule |
| [05-phone-pwa-offline.md](05-phone-pwa-offline.md) | Step 3: phone layout, install to home screen, offline, and the bug only the built site showed |
| [06-guide-deploy.md](06-guide-deploy.md) | The guide page, this folder, the deploy script |
| [07-final-review-per-pest-bases.md](07-final-review-per-pest-bases.md) | The final review (ten defects behind green probes) and a pest read on its own base |
| [HOW-TO-CUSTOMIZE.md](HOW-TO-CUSTOMIZE.md) | For the workshop: make it yours on a branch, live |

## The habits that mattered

- **Tests for the rules, probes for the screens.** Every rule that could be
  wrong in a way you would not notice (the degree-day method, which source
  wins a day, what a share link carries) has a plain-node test. Every screen
  is driven in a real browser by a probe that reads what rendered. Both run
  before anything ships.
- **Mutation-test a new test.** A test that cannot fail proves nothing. The
  merge rule's tests were checked by breaking the rule and watching them go red.
- **Probe the built site, not only the dev server.** Two bugs on this app
  existed only in the generated site. See 05.
- **Say what you don't know.** The app says "estimated" on a date it guessed,
  "forecast" on a day that has not happened, "stale" on data it could not
  refresh, and "for scouting purposes only" on the pest thresholds.
