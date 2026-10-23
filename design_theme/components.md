# Components

Suggested Vue names in **bold**. Sizes are px. Every interactive element is a real `<button>`,
`<a>` (`NuxtLink`), or `<input>` with a `<label>`. Icon-only buttons get `aria-label`.

## Layout

**AppShell (mobile)**: 390-wide reference. `main` scrolls; bottom padding clears the tab bar (84px + 36px).

**BottomTabBar**: fixed bottom, height 84, `--surface`, top border `--line`, 6-column grid, padding `6px 6px 0`.
Tabs: Home · Entries · **(+ FAB)** · Budgets · Wallets · More. Each tab is an icon (24) over a label (11px),
min-height 52. Inactive: `--ink2`, stroke-width 1.8, weight 600. Active: `--accent`, stroke 2.2, weight 700, `aria-current="page"`.
The FAB is a 58×58 circle in `--accent`, `margin-top:-24px`, "+" icon 26 stroke 2.4, `aria-label="Add expense"`, opens Quick add.

**DesktopShell**: flex-wrap row. **Sidebar** `flex: 1 1 232px`, `--surface`, right border, padding `24px 16px`.
Wordmark Fraunces 22/600, then nav links (Home, Entries, Budgets, Wallets, More; active `.on`), then
a full-width "Add expense" primary button (52 high). Main: `flex: 999 1 560px`, padding `32px clamp(16px,4vw,48px)`.
Content grid: `repeat(auto-fit, minmax(min(380px,100%),1fr))`, gap 24. It collapses to one column on narrow widths.

**ScreenHeader**: Fraunces title 32 plus a 14px `--ink2` subtitle (e.g. "Nov 15 – 29 · 5 entries · ₱1,261"), padding `16px 20px 0`.
**SubPageHeader**: 44×44 back chevron plus Fraunces 28 title, height 56 (QR bank, Personal, Reminders).

**CutoffSwitcher** (Home header): ‹ prev button 44, then "Cutoff" (12/600 `--ink2`) over "Nov 15 – 29" (16/700), then › next button 44.
**ReminderBell**: 44×44 link, bell icon 24, badge (min-width 18, height 18, radius 9, `--accent` bg, 11px/700 count).
`aria-label="Reminders, 3 unread"`.

## Cards and lists

**Card**: `--surface`, 1px `--line`, radius 16.

**LeftToSpendCard** (hero): radius 24, padding `20px 20px 18px`, margin `8px 16px 0`.
"Left to spend" 14/600 `--ink2`, then ₱ + Fraunces 64 amount, then "8 days to payday · about ₱630 a day" 15/500,
then a divider (margin-top 18), then a row "Spent **₱5,930**" … "of ₱11,000 safe to spend" 13/500, then **ProgressBar** height 10 in `--accent`.
Progress bar has `role="img"` and `aria-label="54 percent of safe-to-spend used"`.

**ProgressBar**: track `--surface2`, radius h/2, overflow hidden. Fill width = percent (capped at 100). Heights: 10 (hero), 8 (budget rows).

**StatusPill**: inline-flex, gap 4, padding `3px 9px 3px 6px`, radius 999, 12/700, icon 14 stroke 2.4.

| State | bg / text | Icon | Label pattern |
|---|---|---|---|
| ok | `--ok-bg` / `--ok-ink` | circle + check | "On track" |
| near | `--near-bg` / `--near-ink` | triangle + ! | "Near limit · 92%" |
| over | `--over-bg` / `--over-ink` | rounded square + × | "Over by ₱100" |

**BudgetRow** (link card): radius 16, padding `14px 14px 12px` (Home uses `12px 14px`). Row: name 15/600 + StatusPill.
Then ProgressBar 8 (fill = state color `--ok`/`--near`/`--over`), then meta row 13/500 `--ink2`: "₱2,100 of ₱4,500" … "₱2,400 left".
Over state's right side reads "Edit limit". Home's variant omits the right-side text.

**EntryRow**: flex space-between, padding `10px 14px`, min-height 56 (60 in Entries). Title 15/600, meta 13/400 `--ink2`,
amount 15/600 `.num`. Rows are grouped in a `<ul>` card (radius 16, overflow hidden) with `border-top: 1px solid var(--line)` between rows.
Entries groups by day with a header row "Today · Nov 22" … "₱166" (13/700 `--ink2`).

**WalletCard**: radius 20, padding `14px 16px`, min-height 76, gap 14. **IconTile** 44×44 radius 14 `--surface2`.
Name 16/700, type 13 `--ink2` ("On hand", "E-wallet", "Savings account"), balance 20/700 `.num`.

**QrCard**: radius 20, padding 12, min-height 92. Thumb 68×68 radius 12 with dashed 2px `--line` border on `--surface2`.
Name 16/700, sub 13 ("My receiving QR", "Family · saved QR"). "Show" secondary small button.

**ReminderCard**: radius 20, padding `14px 16px`. Icon tile 40×40 radius 12 tinted by state (e.g. `--near-bg`/`--near-ink`).
Title 15/700, sub 13 `--ink2`, then "Mark read" and "Snooze" small secondary buttons (44 high).

**FormRow** (Personal, FirstRun): inside a list card, padding `8px 14px`, min-height 60, label 15–16/600 left,
**AmountField** right (width 120–130, height 44, radius 12, bg `--bg`, 16/600, right-aligned, tabular).

**EmptyState**: centered 72×72 tile (radius 22, `--surface2`), Fraunces 26 title, 15px `--ink2` body, primary button (52 high, padding 0 28).

**OfflineAlert**: `role="alert"`, `--near-bg`/`--near-ink`, radius 16, padding `12px 14px`. Wifi-off icon 24,
"No connection" 15/700 + "Nothing was saved. Check your signal and try again." 13/500. **Retry** button (44 high, bg `--near-ink`, text `--near-bg`).
While offline, show the last-loaded hero number at `opacity: .45` with "Last loaded figure. It may be out of date until you reconnect."

## Inputs and buttons

**Button / primary**: height 52 (54 on SignIn/FirstRun), radius 16, `--accent` bg, `--on-accent` text, 16/700.
**Button / secondary**: transparent, `box-shadow: inset 0 0 0 1px var(--line)` (or 1px border), same size.
**Button / small**: height 44, padding 0 14–16, radius 12, 1px `--line`, 14/600.
**Button / disabled**: `--surface2` bg, `--ink2` text, e.g. "Choose a category to save".
**Button / text**: 48 high, `--accent` 15/600 ("Create an account"), or `--ink2` ("Skip for now").

**Chip** (toggle): height 44, padding 0 16, radius 22, 1px `--line`, `--surface`, 15/600. Selected `.on` uses accent bg/border, `--on-accent` text,
a leading check icon (16, stroke 2.6), and `aria-pressed="true"`. An optional leading icon at 18 (wallet, calendar).
"Add note" chip: dashed border, `--ink2`. **FilterChip** (Entries): height 44, padding 0 14, 14/600, trailing chevron-down 14.

**Keypad**: 3-column grid, gap 8. **Key**: height 60 (52 in DS), radius 16, `--surface`, `inset 0 0 0 1px var(--line)`, 26/600.
Keys 1–9, ".", 0, and backspace (icon 26, `aria-label="Delete"`).

**TextField**: height 52, radius 14, 1px `--line`, `--surface`, padding 0 14, 16/500. Label above: 13/600 `--ink2`, margin `0 0 6px 2px`.
**SearchField**: height 48, radius 16, left search icon 20 at 14px, padding-left 42, visually hidden label.

**SegmentedControl** (Theme: Light / Dark / Match phone): 3-col grid, gap 4, padding 4, `--surface2` track, radius 14.

**StepIndicator** (FirstRun): 4 nodes (Account, Salary, Budgets, QR codes). Each is a 34px circle with a 12/600 label.
A 2px rail runs between node centres (12.5%–87.5%) with an accent fill growing per step.
Done = accent fill with check. Current = surface fill, accent border and number. Todo = `--surface2` fill, `--line` border.

**SuccessMark**: 88×88 circle `--ok-bg`/`--ok-ink`, check icon 44 stroke 2.4.

## Icons (inline SVG, 24 viewBox, round caps/joins)

home `M4 11l8-7 8 7v8a1 1 0 0 1-1 1h-4v-6h-6v6H5a1 1 0 0 1-1-1z` · list `M8 6h12M8 12h12M8 18h12M4 6h.01M4 12h.01M4 18h.01` ·
budgets `circle r8 + M12 4v8h8` · wallet `M4 7a2 2 0 0 1 2-2h11v4` + `rect 4,7 16×12 rx2` + `M16 13h.01` ·
more `M5 12h.01M12 12h.01M19 12h.01` (stroke 3) · plus `M12 5v14M5 12h14` · close `M6 6l12 12M18 6L6 18` ·
chevrons `M15 5l-7 7 7 7` / `M9 5l7 7-7 7` / `M6 9l6 6 6-6` · bell `M6 16V11a6 6 0 0 1 12 0v5l1.5 2h-15z M10 21h4` ·
check `M5 12.5l4.5 4.5L19 7.5` · ok `circle r9 + M8 12.5l3 3 5-6` · near `M12 4l9 16H3z M12 10v4M12 17h.01` ·
over `rect 4,4 16×16 rx3 + M9 9l6 6M15 9l-6 6` · cash `rect 3,7 18×10 rx2 + circle r2.5` · phone/e-wallet `rect 7,3 10×18 rx2 + M11 18h2` ·
bank `M3 10l9-6 9 6M5 10v8M9.5 10v8M14.5 10v8M19 10v8M3 20h18` · calendar `rect 4,5 16×15 rx2 + M4 10h16M9 3v4M15 3v4` ·
qr `rect 3,3 7×7 + rect 14,3 + rect 3,14 + M14 14h3v3h-3zM20 14v.01M14 20h3M20 17v4` · upload `M12 16V5M7 10l5-5 5 5M5 19h14` ·
transfer `M4 8h14l-3-3M20 16H6l3 3` · copy `rect 8,8 12×12 rx2 + M16 8V6a2 2 0 0 0-2-2H6a2 2 0 0 0-2 2v8a2 2 0 0 0 2 2h2` ·
search `circle 11,11 r6 + M20 20l-4.5-4.5` · backspace `M21 5H9l-6 7 6 7h12z M12 9l5 6M17 9l-5 6` ·
wifi-off `M3 3l18 18M8.5 16a5 5 0 0 1 7 0M5 12.5a10 10 0 0 1 3-2M12 20h.01M10 6.2A15 15 0 0 1 22 9M2 9a15 15 0 0 1 4-2.5`.

Put them in one `AppIcon.vue` (`<AppIcon name="wallet" :size="24" />`), with stroke width as a prop (1.8 default, 2.2 active).
