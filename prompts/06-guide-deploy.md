# 06 · The guide, this folder, the deploy

## What was built

- `app/pages/guide.vue`: the 📖 guide as its own prerendered route (offline
  once visited), in English and Spanish with a toggle, written for someone
  handed a link: what it is for, two minutes to running, each tab, where the
  numbers come from, the limits, the Rutgers credit and caveat.
- `prompts/`: this folder, copied into the public repo on every deploy so the
  history teaches, not just serves.
- `scripts/generate_pages.mjs` (static build under `/degreedays/`),
  `scripts/probe_built.mjs` (serves the build under that base and runs the
  PWA, backup/share and guide probes against it), `scripts/deploy_pages.mjs`
  (the gate: suites, build, built-site probes; then replace the deploy repo's
  contents, write `.nojekyll`, stamp the service-worker cache name, commit,
  push). Nothing reaches the public repo unless every check passed against the
  exact build being shipped.

## First deploy

1. Create a public repo `degreedays` on GitHub and enable Pages (main / root).
2. `git clone https://github.com/carynamichel-hue/degreedays.git C:\Users\caryn\dev\degreedays-pages`
3. `npm run deploy:pages` — live at https://carynamichel-hue.github.io/degreedays/ a minute later.
