# Evolve — v2.0 Pre-Release

Private, offline-first gym & nutrition tracker. Runs entirely as a PWA — no accounts, no servers, no ads.

## What's in 2.0

### Design overhaul
- Pure `#080808` black — no dark navy, no gradients
- Playfair Display 900-weight serif for all display headings
- Single accent: `#F0EDE8` bone white throughout
- Zero border-radius on every element — hard rectangles everywhere
- Navigation is a flat bar with a top border, not a floating pill
- All section labels uppercase at 9px/0.28em tracking

### Train screen
- Muscle groups are now a vertical list with coloured accent bars (per GROUP_GLOW colours)
- Preset sessions show muscle descriptions and exercise count badge
- Exercise picker: scrolling filter tabs, exercises listed as uppercase rows
- Each exercise row: `?` (form guide), `☆` (star), `+` (add)

### Live session
- Sticky header with session name, sets progress, and live session clock (MM:SS)
- Done sets collapse to one line — tap to undo
- Active set has full-width `LOG SET` button (bone white, Playfair)
- RIR is hidden by default — one tap to expand
- Mid-session PR alerts: multi-buzz haptic + toast when you beat a previous best
- PR badge appears inline on done set rows

### Session summary
- Full debrief on finish: total load, minutes, sets logged, new PRs
- Complete set-by-set log — every exercise, every weight × reps
- `REPEAT THIS SESSION` rebuilds the exact session for next time
- Share card redesigned: pure black, Playfair Display, no orange/teal gradients

### Home screen
- Completed sessions section now navigable by day (← → arrows)
- Tap VIEW on any session to see the full set log and repeat it

## Files

| File | Purpose |
|---|---|
| `index.html` | App shell HTML |
| `app.js` | All app logic |
| `styles.css` | All styles (brutal design system) |
| `data.js` | Exercise, cardio, food databases |
| `food-packs.js` | UK supermarket food packs |
| `sw.js` | Service worker — cache: `evolve-v3-71` |
| `manifest.json` | PWA manifest |

## Deploy

Drop all files into the repo root, push. The service worker cache key is `evolve-v3-71` — existing users get the update automatically on next open.

## Design tokens

```css
--ink: #080808        /* page background */
--text: #F0EDE8       /* primary text + single accent */
--muted: #909090      /* secondary text */
--surface: #141414    /* card backgrounds */
--line: #282828       /* borders */
--font-disp: "Playfair Display" 900  /* all headings */
--r: 0px              /* zero border-radius everywhere */
```
