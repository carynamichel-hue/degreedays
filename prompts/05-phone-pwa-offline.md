# 05 · Step 3 — phone, install, offline, and the built-site bug

## What was built

- A manifest, the app's own icon (rasterised to PNG for iOS through the dev
  server with headless Chrome), a service worker on SprayCast's pattern:
  navigations network-first, the cached shell only as the offline fallback,
  hashed assets cache-first, only this app's caches swept, the cache name
  stamped per deploy. A 📴 chip and bar when offline. Safe-area padding.
- An all-locations summary on Now.
- `probes/serve_built.mjs` (a Pages-like static server), `probes/pwa.mjs`
  (manifest, worker registered and controlling, shell + assets cached, QR and
  snapshot under the production CSP), `probes/builterr.mjs` (a script injected
  before the page's own so console errors, window errors and Nuxt's state
  store can be read on the built site).

## The bug only the built site showed

`?sample=1`, `?tab=season` and `?asof=2026-05-15` did nothing on the
generated site and everything on the dev server. No error anywhere. Checkpoint
logs in the boot proved that **`window.location.search` is empty at the moment
the page mounts** on the prerendered build, and comes back a few seconds
later. (The first suspect, the sample module's dynamic import, was innocent;
the comment in the code says so.)

Fix: a client plugin captures the query at boot into state, the same reason
SprayCast reads its share hash in a plugin. Rule kept: **read the URL in a
plugin, never in `onMounted`, and probe the built site before shipping.**

A second built-only artefact: the probe driver's storage-seeding hop lands on
the prerendered 404 page, which logs one Nuxt app error. Expected, filtered.

## Verified on the build

Manifest served, worker controlling, shell + 11 hashed assets in the app's
cache, QR and snapshot under the CSP, all-locations card, backup and share
including a fresh browser accepting a link with no token, Excel, deep links.
