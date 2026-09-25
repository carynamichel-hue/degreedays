# 04 · Backup, share, Excel, and the token rule

## What was built

- `app/utils/backup.js` (pure, 33 tests): `buildPack` (everything the browser
  knows that cannot be refetched), `validatePack` (whitelists and caps, a
  reason on refusal), `mergePack` (locations by id, pests newer-wins, logs day
  by day under the precedence rule, settings fill-only), `sharePayload` (the
  setup subset: locations, edited or added pests, categories), `encodeShare`
  / `decodeShare` (deflate + base64url in the URL fragment).
- `useBackup` + a Setup card: download, restore by file or paste, a link
  with a QR code, a share file, and an accept banner that shows what would
  arrive before anything lands. A boot plugin takes `#s=` off the URL.
- `app/utils/xlsx.js`: SheetJS loaded on demand; daily log, pest list +
  events, everything, and the multi-source comparison.
- The forecast check, expanded: every source (model, station, file, the log,
  each forecast lead) paired against the truth, over 30/90 days or the season,
  a day-by-day table, and the Excel export. The forecast book keeps 400 days.

## The token rule

The LI-COR API token lives in its own storage key that no backup or share
builder reads. That is stronger than "strip it on the way out": there is no
way out. The test plants a token on a station record and asserts it never
appears; the browser probe plants one in storage and checks the real link,
the backup file, the share file, and a fresh browser that accepts the link.

## What went wrong

The share link worked when pasted into the same browser and did nothing in a
fresh one. The boot plugin decodes the link asynchronously; the page read the
stash once at mount, before it existed. Fix: watch the stash. Caught by the
probe's second, fresh-browser half — the reason it has one.
