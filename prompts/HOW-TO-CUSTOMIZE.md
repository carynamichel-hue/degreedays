# How to make it yours — on a branch, live

The workshop format: the built app is public and installable. To change it
you need the source. This is the twenty-minute path.

## What you need

A GitHub account, Node 20 or newer, and an AI coding assistant that can run
commands (Claude Code was used here). No other installs.

## Steps

1. **Get the source** (ask for it; the source repo is private to the farm) and
   open the `degreeday-nuxt` folder in your assistant.
2. **Run it**: `npm install`, then `npm run dev` → http://localhost:3009. Try
   `?sample=1` for a farm with synthetic weather.
3. **Make a branch**: `git checkout -b my-nursery`.
4. **Ask for the change in your words.** Real asks from this build are in
   [03-review-rounds.md](03-review-rounds.md). Good first ones:
   - "Add my nursery's pests: [list]. Base 50, upper 95, these stages and
     degree-day ranges: […]."
   - "Rename the categories to match my crops: […]."
   - "Default the language to Spanish and the units to °C."
   - "Add a 'block' field to every pest and show it on the Now screen."
5. **Insist on the checks**: "run npm test and the probe for that screen
   before you say it's done." If a rule changed, "add a test that would have
   failed before."
6. **Build and probe the built site**: `npm run generate:pages` then
   `npm run probe:built`. This is the step that catches what the dev server
   hides (see 05).
7. **Deploy your own copy**: create your own public `degreedays` repo, change
   the two repo paths at the top of `scripts/deploy_pages.mjs`, then
   `npm run deploy:pages`.

## What to keep

- The pure modules stay pure: `weather/*.js` and `app/utils/*.js` import no
  app code. That is what makes them testable in plain node, and liftable.
- One source of truth per rule: which source wins a day (`mergeRows`), what a
  share carries (`sharePayload`), what "coming soon" means (`pestStatus`).
  Change the rule in the one place and the test beside it.
- Honesty on screen: estimated, forecast, stale, "for scouting purposes only".
