# Changelog

## 2.0.0 — 2026-06-19 (final release)

Evolve 2.0 is the full release of the redesigned, private, offline-first gym &
nutrition tracker. It consolidates the redesign and the audit-hardening work below.

### Highlights
- Full "brutal" redesign (pure-black editorial theme), live session clock, mid-session
  PR alerts, set-by-set session summaries, and date-navigable home history.
- Stronger backup encryption: PBKDF2-SHA256 at **600,000 iterations** (older 210,000
  backups still restore).
- Spreadsheet-safe CSV exports; AI Coach workout generation with a real exercise
  allow-list.
- Accessibility: dialog semantics + focus management on modals/live session, labelled
  icon buttons, hidden decorative icons.

### Finalisation (from 2.0.0-audit.2)
- Version set to `2.0.0`; service-worker cache `evolve-v3-76`; manifest `2.0.0`.
- Replaced all "pre-release" / "test-build" wording with final-release copy.
- No feature or data-format changes; existing data and encrypted backups still work.

## 2.0.0-audit.2 — 2026-06-19

### Security
- Raised encrypted-backup key stretching from PBKDF2-SHA256 210,000 iterations to **600,000**. The iteration count is recorded in each backup envelope and honoured on decrypt, so backups written by earlier builds (210,000) still restore — no lockout.
- Verified the backup crypto dynamically (round-trip, wrong-password rejection, tamper rejection, random salt; plus legacy-backup decryption) rather than by static review alone.
- Bumped service-worker cache to `evolve-v3-75` and app/manifest version to `2.0.0-audit.2`.

## 2.0.0-audit.1 — 2026-06-19

### Security and correctness
- Hardened CSV exports against spreadsheet formula injection.
- Corrected AI Coach generated-workout exercise allow-list construction.
- Made optional food-pack validation pass clean source checkouts while preserving failure for inconsistent generated pack files.
- Aligned service-worker cache/version references to `evolve-v3-74`.

### Accessibility
- Added modal focus placement, focus restore, Escape close, and Tab focus wrapping for non-mandatory dialogs.

### Documentation
- Added `SECURITY.md` and this `CHANGELOG.md`.
- Updated `README.md`, `EVOLVE_HANDOFF.txt`, and `food-db/README.md` for the audit build.
- Added standalone audit report: `EVOLVE_AUDIT_REPORT_2026-06-19.md`.

## 2.0 pre-release — previous package

- Brutal black/bone-white redesign.
- Live-session clock, PR alerts, session summary, and repeatable session history.
- Home date navigation and full set-log history views.
- Stricter backup/import and AI Coach key handling compared with the 1.0 live app.
