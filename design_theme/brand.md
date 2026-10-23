# Brand

## Name and tagline
- **BBudgeTrakker** (one word, capital B-B-T). Allow a line break as `BBudge<wbr>Trakker`.
- Tagline: **"What can you safely spend before the next payday?"**
- Positioning lines (showcase): "Know what you can safely spend" · "Paydays, not calendar months" ·
  "Log expenses in seconds" · "Two taps after the amount" · "Stay on budget, every cutoff" ·
  "An icon and a label, not just color".

## Logo: BB monogram
A 100×100 rounded square (rx 24) in ink `#26211C`, with two Fraunces 600 "B"s (font-size 58, baseline y=71, centred at x=33 and x=67).
The first B is paper `#FAF6EE`, the second teal `#5FC4AB`.

```svg
<svg role="img" aria-label="BBudgeTrakker logo" viewBox="0 0 100 100">
  <rect width="100" height="100" rx="24" fill="#26211C"/>
  <text x="33" y="71" text-anchor="middle" font-family="Fraunces, Georgia, serif" font-size="58" font-weight="600" fill="#FAF6EE">B</text>
  <text x="67" y="71" text-anchor="middle" font-family="Fraunces, Georgia, serif" font-size="58" font-weight="600" fill="#5FC4AB">B</text>
</svg>
```
Versions on the Logo artboard: **Primary · on ink**, **Light · on paper**, **Single color · browser tab** (favicon).
For app icons and favicons, convert the text to paths (outline the glyphs) so they don't depend on the font loading.
Capacitor icon and splash: generate from this with `@capacitor/assets`.

## Voice and copy rules (observed across every screen)
- Plain, calm, second person: "So your budget is saved and stays yours." No exclamation marks, no emoji.
- Sentence case everywhere ("Add expense", "Copy last cutoff").
- Numbers are always exact and in ₱, with no decimals unless typed: "₱5,070", "about ₱630 a day".
- Use "·" (middle dot, spaced) as the separator in meta lines: "Food · GCash · Yesterday".
- Every state has one clear next action ("No entries yet" → "Add expense"; offline → "Retry").
- Honest about data: "Your data is encrypted and stays yours. No bank linking." / "Last loaded figure. It may be out of date…"

## Marketing artboards (for the README, store listing, social)
- **Showcase 1–3** (900×1900, forest `#14463C` bg with `#1B5A4D` circles): a big Fraunces 92 headline in paper,
  34px subline in `#DDEEE8`, a phone mockup (radius 72, bezel 12px `#0E2822`), and a rotated teal ribbon callout.
- **GitHub banner** (1280×640): logo 96, "BBudgeTrakker" Fraunces 84, the tagline, tech tags
  **Nuxt · Laravel · MySQL · AWS**, and a phone with the hero card plus a Fun near-limit card.
Export these from the canvas as PNG when needed. They aren't part of the app build.
