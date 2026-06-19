# Security

## Model

Evolve is a static, offline-first PWA. There is no Evolve app server, no account system, no central database, and no payment surface in this build. The main trust boundaries are:

- Browser storage (`localStorage`, `sessionStorage`, IndexedDB)
- Backup/import text and encrypted backup files
- CSV exports opened by spreadsheet software
- Optional food-pack downloads from same-origin `food-db/`
- Optional AI Coach requests sent directly from the browser to OpenRouter when the user enables Coach and provides a key
- Service-worker cache storage

## Data handling

Personal app data is stored on the user's device. Profile photos, progress photos, and the OpenRouter key are deliberately kept outside backup exports. Encrypted backups use PBKDF2-SHA256 with 600,000 iterations and AES-GCM with a random salt and IV per export. The iteration count is recorded inside each backup envelope, so the cost can be raised in future without locking users out of older backups; backups written by earlier builds (210,000 iterations) still decrypt.

## 2026-06-19 audit changes

| Severity | Area | Finding | Change |
|---|---|---|---|
| Medium | CSV export | User-controlled workout/food names could be exported as spreadsheet formulas if they began with `=`, `+`, `-`, `@`, or whitespace-prefixed variants. | Added `_csvSafeForSpreadsheet()` and routed all CSV cells through it before quoting. |
| Medium | AI Coach | Generated-workout prompts called `gymPoolNames()` without a group, producing an empty allowed exercise list. | Made `coachExercisePool(groups)` return the full exercise library or a group-filtered library. |
| Low | Validation tooling | `tools/validate-food-db.js` failed clean checkouts that had only `food-db/README.md`, even though generated packs are optional. | Validator now skips with a clear message when no generated manifest or shop JSON files exist, but still fails if shop JSON exists without a manifest. |
| Low | Versioning/cache | Runtime/docs disagreed on cache key/version (`evolve-v3-71` docs vs `evolve-v3-73` service worker). | Bumped and aligned runtime/docs to `evolve-v3-74` and manifest `2.0.0-audit.1`. |
| Low | Modal accessibility | Dialogs had labels but did not reliably move/trap focus. | Added focus capture/restore, first-focus placement, Escape close, and Tab wrapping for open modals. |
| Info | Framing protection | `frame-ancestors 'none'` appears in a meta CSP. Browsers require this directive as an HTTP header, so GitHub Pages cannot enforce it from the app file alone. | Documented as a hosting limitation. Use a host/CDN that can send CSP headers if strong anti-framing is required. |

## Checks that were already positive

- The app shell has a restrictive CSP meta policy for scripts, objects, base URI, form action, images, fonts, worker source, and connections.
- OpenRouter requests use `credentials: "omit"` and `referrerPolicy: "no-referrer"`.
- Backup import uses size limits and JSON sanitisation before merging known data keys.
- Service-worker caching is scoped to same-origin static assets and Google Fonts origins only.
- Optional food packs are validated before IndexedDB storage, including numeric kcal/macro limits.

## Operational notes

GitHub Pages does not let this static app set arbitrary HTTP security headers. For deployments behind Cloudflare, Netlify, a custom server, or another host that can set headers, deliver CSP as an HTTP header and include `frame-ancestors 'none'` there.
