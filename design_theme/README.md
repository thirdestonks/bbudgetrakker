# design_theme: BBudgeTrakker design spec

Written from the design canvas **BBudgeTrakker**
(https://claude.ai/code/artifact/8cc7f248-7ae3-4688-b015-75729ae41795) on 2026-10-23.
The canvas is the visual source of truth. These files are the build-ready translation of it.
If the canvas changes, update these files in the same change.

| File | What's in it |
|---|---|
| [tokens.md](tokens.md) | Color tokens (light and dark), typography, spacing, radii, with a ready-to-paste `tokens.css` |
| [components.md](components.md) | Reusable UI pieces with exact sizes and styles, plus suggested Vue component names |
| [screens.md](screens.md) | All app screens (mobile and desktop), routes, layout, content, and links between them |
| [domain.md](domain.md) | Cutoffs, safe-to-spend math, budget states, wallets, QR bank, reminders, and the data model |
| [brand.md](brand.md) | Logo, voice and copy rules, marketing showcase and banner |

## Canvas map (24 artboards)

| Group | Artboards |
|---|---|
| Design system | DS-Light, DS-Dark (700×1180) |
| Home and Quick add | Home (Main), QuickAdd1 Keypad, QuickAdd2 Chosen, QuickAdd3 Saved |
| Core screens | Entries, Budgets, Wallets, Reminders, Settings |
| Onboarding and misc | SignIn, FirstRun (5 steps), States (empty / offline), QRBank, Personal |
| Desktop (fluid, 1280 wide) | DesktopHome, DesktopEntries, DesktopBudgets |
| Brand | Logo directions, Showcase 1–3 (900×1900), GitHub Banner (1280×640) |

Mobile artboards are 390×844 (iPhone 14-class). Desktop artboards are fluid pages designed at 1280.

## The design in one paragraph

Warm paper background (#FAF6EE), white cards with hairline beige borders, one deep-teal
accent (#1D6F5F). Fraunces (serif) for screen titles and the big money number. Figtree (sans)
for everything else, with tabular numerals. Three budget states: On track (teal-green),
Near limit (amber), Over (brick red). Each pairs an icon and a label with its color.
Mobile uses a 6-column bottom tab bar with a raised round "+" in the middle. Desktop uses a
232px left sidebar.
