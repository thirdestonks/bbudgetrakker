# Tokens

All values are copied exactly from the design's CSS. Components must use the variables, never raw hex.

## Color

| Token | Light | Dark | Use |
|---|---|---|---|
| `--bg` | `#FAF6EE` | `#1A1714` | Page background ("Paper") |
| `--surface` | `#FFFFFF` | `#25211D` | Cards, tab bar, inputs, chips |
| `--surface2` | `#F1EADC` | `#312B25` | Progress tracks, icon tiles, disabled button, segmented-control track |
| `--ink` | `#26211C` | `#F3ECE0` | Primary text |
| `--ink2` | `#5E564D` | `#BDB3A5` | Secondary text, captions, inactive tabs |
| `--line` | `#E4DCCD` | `#3A342D` | Borders and dividers (1px) |
| `--accent` | `#1D6F5F` | `#5FC4AB` | Primary buttons, active tab, links, progress fill |
| `--on-accent` | `#FFFFFF` | `#0E2822` | Text and icons on accent |
| `--ok` | `#2E8B76` | `#6FCFB6` | On-track bar fill |
| `--ok-ink` | `#17594B` | `#7FD6BF` | On-track pill text, success icon |
| `--ok-bg` | `#DDEEE8` | `#1F3A33` | On-track pill bg, success circle, QR-bank banner |
| `--near` | `#D99A1E` | `#F0B84A` | Near-limit bar fill |
| `--near-ink` | `#7A4E00` | `#F0B84A` | Near-limit pill text, offline alert text, Retry button bg |
| `--near-bg` | `#FBEBC8` | `#3D2F12` | Near-limit pill bg, offline alert bg |
| `--over` | `#B4382A` | `#FF8F7C` | Over bar fill |
| `--over-ink` | `#9A2B1E` | `#FF9C8A` | Over pill text |
| `--over-bg` | `#F9DAD2` | `#402018` | Over pill bg |

Marketing-only colors (showcase and banner, not used in the app): forest `#14463C`, deco circles `#1B5A4D`,
phone bezel `#0E2822`, tag border `#3F7E70`.

FAB shadow (light): `0 6px 16px rgba(29,111,95,.35), 0 0 0 5px var(--bg)`. The second ring cuts the FAB out of the tab bar.

## Typography

Fonts (Google Fonts):
```
https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,500;9..144,600&family=Figtree:wght@400;500;600;700&display=swap
```
For Capacitor/offline, self-host both (e.g. `@nuxt/fonts` or files in `public/fonts`).

| Role | Font | Size / line / weight | Notes |
|---|---|---|---|
| Hero amount | Fraunces | 64 / 1 / 600, `letter-spacing: -0.02em` | ₱ prefix: Figtree 600 30px in `--ink2`. Desktop: 84px, prefix 36px |
| Screen title | Fraunces | 32 / 1.1 / 600 | Sub-pages (QR bank, Personal, Reminders) use 28px |
| Success title | Fraunces | 34 / 1.1 / 600 | "Saved", "You are set" (32) |
| Sign-in wordmark | Fraunces | 40 / 1.05 / 600 | |
| Section heading | Figtree | 16 / 1.2 / 700 | "Closest to limit", "Recent" |
| Group label | Figtree | 13 / 1.2 / 700, `--ink2` | Settings groups, date headers in Entries |
| Body / row title | Figtree | 15 / 1.3 / 600 | |
| Row meta / caption | Figtree | 13 / 1.3 / 400, `--ink2` | "Food · Cash · Today" |
| Button | Figtree | 16 / 1 / 700 | |
| Tab label | Figtree | 11 / 1 / 600 (active 700) | |
| Pill | Figtree | 12 / 1.3 / 700 | |
| Eyebrow | Figtree | 12 / 1 / 700, uppercase, `letter-spacing: .06em` | DS sheets only |

All numbers use `font-variant-numeric: tabular-nums lining-nums` (class `.num`).

## Spacing

Scale: **4 · 8 · 12 · 16 · 24**. Screen side gutter is 16px (card margins). Headers are padded 20px.
Gap between stacked cards is 8px; between sections, 18–22px.

## Radius

**12** (small buttons, icon tiles, amount fields) · **16** (cards, primary buttons, keypad keys, list groups) ·
**20–24** (hero card 24, summary cards 20, wallet cards 20) · **pill** 999 (status pills, chips are 22 = height/2).

## Ready-to-paste `tokens.css`

```css
:root, .theme-light {
  --bg:#FAF6EE; --surface:#FFFFFF; --surface2:#F1EADC;
  --ink:#26211C; --ink2:#5E564D; --line:#E4DCCD;
  --accent:#1D6F5F; --on-accent:#FFFFFF;
  --ok:#2E8B76; --ok-ink:#17594B; --ok-bg:#DDEEE8;
  --near:#D99A1E; --near-ink:#7A4E00; --near-bg:#FBEBC8;
  --over:#B4382A; --over-ink:#9A2B1E; --over-bg:#F9DAD2;
  --font-sans:'Figtree',system-ui,sans-serif;
  --font-display:'Fraunces',Georgia,serif;
  color-scheme: light;
}
.theme-dark {
  --bg:#1A1714; --surface:#25211D; --surface2:#312B25;
  --ink:#F3ECE0; --ink2:#BDB3A5; --line:#3A342D;
  --accent:#5FC4AB; --on-accent:#0E2822;
  --ok:#6FCFB6; --ok-ink:#7FD6BF; --ok-bg:#1F3A33;
  --near:#F0B84A; --near-ink:#F0B84A; --near-bg:#3D2F12;
  --over:#FF8F7C; --over-ink:#FF9C8A; --over-bg:#402018;
  color-scheme: dark;
}
@media (prefers-color-scheme: dark) {
  :root:not(.theme-light) { /* "Match phone": same values as .theme-dark */ }
}
body { margin:0; background:var(--bg); color:var(--ink); font-family:var(--font-sans); }
*, *::before, *::after { box-sizing:border-box; }
.num  { font-variant-numeric: tabular-nums lining-nums; }
.disp { font-family: var(--font-display); }
```
Implement "Match phone" by toggling `.theme-dark` on `<html>` from `matchMedia('(prefers-color-scheme: dark)')`
when the setting is `system`. That's simpler than duplicating the dark block inside the media query.
